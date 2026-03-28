# Checkout - Contrato de Integração Frontend ↔ Backend

## Visão Geral

Este documento define os contratos de API consumidos pelo frontend Checkout. Todos os endpoints devem seguir este contrato durante o desenvolvimento paralelo.

## Endpoints

### API-001: Configuração do Checkout

```
GET /events/:eventId/checkout-config
```

**Response:**
```json
{
  "eventId": "string",
  "ticketTypes": [
    {
      "id": "string",
      "name": "string",
      "price": 0,
      "isNominal": true,
      "customFields": [
        {
          "name": "string",
          "label": "string",
          "type": "text|number|cpf|cnpj",
          "required": true
        }
      ]
    }
  ],
  "paymentMethods": ["pix", "credit_card", "boleto"],
  "couponEnabled": true,
  "termsUrl": "string"
}
```

### API-002: Ingressos Selecionados

```
GET /events/:eventId/tickets/selected
```

**Response:**
```json
{
  "event": {
    "id": "string",
    "name": "string",
    "date": "2024-01-01T00:00:00Z"
  },
  "tickets": [
    {
      "id": "string",
      "typeId": "string",
      "typeName": "string",
      "price": 0,
      "quantity": 1
    }
  ],
  "subtotal": 0,
  "discount": 0,
  "total": 0
}
```

### API-003: Validar Cupom

```
POST /checkout/validate-coupon
```

**Request:**
```json
{
  "eventId": "string",
  "couponCode": "string"
}
```

**Response (sucesso):**
```json
{
  "valid": true,
  "couponCode": "string",
  "discountType": "percentage|fixed",
  "discountValue": 0,
  "discountAmount": 0
}
```

**Response (erro):**
```json
{
  "valid": false,
  "error": "COUPON_NOT_FOUND|COUPON_EXPIRED|COUPON_ALREADY_USED"
}
```

### API-004: Reservar Ingressos (Cria Countdown)

```
POST /checkout/reserve
```

**Request:**
```json
{
  "eventId": "string",
  "tickets": [
    {
      "typeId": "string",
      "quantity": 1
    }
  ]
}
```

**Response:**
```json
{
  "reservationId": "string",
  "expiresAt": "2024-01-01T00:15:00Z",
  "status": "reserved"
}
```

### API-005: Recalcular Total

```
GET /checkout/calculate?reservationId=string&couponCode=string
```

**Response:**
```json
{
  "subtotal": 0,
  "discount": 0,
  "total": 0
}
```

### API-006: Inicializar Pagamento

```
POST /checkout/payment/init
```

**Request:**
```json
{
  "reservationId": "string"
}
```

**Response:**
```json
{
  "sessionId": "string",
  "savedCard": {
    "cardId": "string",
    "last4": "string",
    "brand": "string"
  } | null
}
```

### API-007: Pagamento Pix

```
POST /checkout/payment/pix
```

**Request:**
```json
{
  "sessionId": "string",
  "ticketHolder": {
    "name": "string",
    "email": "string",
    "phone": "string"
  },
  "buyer": {
    "name": "string",
    "email": "string",
    "document": "string",
    "phone": "string"
  }
}
```

**Response:**
```json
{
  "paymentId": "string",
  "qrCode": "base64",
  "qrCodeText": "string",
  "expiresAt": "2024-01-01T00:30:00Z"
}
```

### API-008: Pagamento Cartão

```
POST /checkout/payment/card
```

**Request:**
```json
{
  "sessionId": "string",
  "cardId": "string",
  "cvv": "string",
  "ticketHolder": {
    "name": "string",
    "email": "string",
    "phone": "string"
  },
  "buyer": {
    "name": "string",
    "email": "string",
    "document": "string",
    "phone": "string"
  }
}
```

**Response:**
```json
{
  "paymentId": "string",
  "status": "approved|declined",
  "declineReason": "string | null"
}
```

### API-009: Pagamento Boleto

```
POST /checkout/payment/boleto
```

**Request:** (mesmo formato de Pix)

**Response:**
```json
{
  "paymentId": "string",
  "boletoUrl": "string",
  "boletoBarcode": "string",
  "expiresAt": "2024-01-05T00:00:00Z"
}
```

### API-010: Status Pagamento (Polling)

```
GET /checkout/payment/:paymentId/status
```

**Response:**
```json
{
  "paymentId": "string",
  "status": "pending|confirmed|expired|failed",
  "confirmedAt": "2024-01-01T00:00:00Z | null"
}
```

### API-011: Dados Confirmação

```
GET /checkout/confirmation/:paymentId
```

**Response:**
```json
{
  "confirmationId": "string",
  "event": {
    "name": "string",
    "date": "string",
    "location": "string"
  },
  "tickets": [
    {
      "name": "string",
      "type": "string",
      "quantity": 1
    }
  ],
  "payment": {
    "method": "pix|credit_card|boleto",
    "amount": 0,
    "status": "confirmed",
    "date": "string"
  }
}
```

### API-012: Buscar Dados Salvos

```
GET /users/me/saved-data
```

**Response:**
```json
{
  "name": "string",
  "email": "string",
  "document": "string",
  "phone": "string",
  "savedCards": [
    {
      "cardId": "string",
      "last4": "string",
      "brand": "string"
    }
  ]
}
```

### API-013: Salvar Dados

```
PUT /users/me/saved-data
```

**Request:**
```json
{
  "name": "string",
  "email": "string",
  "document": "string",
  "phone": "string",
  "saveForFuture": true
}
```

### API-014: Verificar E-mail Existente

```
POST /users/check-email
```

**Request:**
```json
{
  "email": "string"
}
```

**Response:**
```json
{
  "exists": true | false
}
```

## Estados de Reserva

```
reserved → confirmed → completed
    ↓
  expired (15min)
```

## Códigos de Erro

| Código | Descrição |
|--------|-----------|
| RESERVATION_EXPIRED | Tempo de reserva esgotado |
| COUPON_NOT_FOUND | Cupom não encontrado |
| COUPON_EXPIRED | Cupom expirado |
| PAYMENT_DECLINED | Cartão recusado |
| PAYMENT_PENDING | Aguardando confirmação |
