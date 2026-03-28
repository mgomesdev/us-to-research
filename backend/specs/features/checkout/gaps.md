# Checkout - gaps & Planning

## 1. Informações Faltantes para Desenvolvimento

### 1.1 Stack Técnica
- Linguagem/Framework esperado: A definir com o time dev
- Banco de dados: A definir com o time dev
- Autenticação/Autorização: A definir com o time dev
- Provedor de pagamento (se aplicável): Pay (mencionado na US como "Pay")
- Outras tecnologias: A definir

### 1.2 Integração com Frontend
- Nome da feature de frontend vinculada: A definir
- Contratos/Endpoints necessários (a definir):
  - GET /events/:id/checkout-config - obter configuração do checkout
  - POST /checkout/participants - enviar dados dos participantes
  - POST /checkout/responsible - informar responsável pelos ingressos
  - POST /checkout/validate-coupon - validar cupom de desconto
  - POST /checkout/reserve - reservar ingressos (iniciar checkout)
  - POST /checkout/process-payment - processar pagamento
  - POST /checkout/create-account - criar conta automática
  - GET /checkout/:id/status - verificar status do pagamento
  - POST /checkout/confirm - confirmar compra
  - (outros endpoints que o dev precisar definir)

### 1.3 Data Models Necessários
Liste os models que provavelmente serão necessários baseado na feature:
- CheckoutSession - gerenciar sessão de checkout com tempo de 15min
- Order/Checkout - representar o pedido
- Participant - dados dos participantes (nome, email, celular, campos customizados)
- Ticket - configuração do ingresso
- TicketType - tipo (nominal vs não nominal)
- Payment - dados do pagamento
- Coupon - cupom de desconto
- User - para conta automática
- CheckoutFlow - tipo de checkout (nominal pago, nominal gratuito, etc.)
- (outros que o dev identificar)

### 1.4 Validações Faltantes
Liste validações que a US menciona mas não detalha:
- Validação de campos customizados por ingresso: Como validar tipos customizados?
- Regras de validação de pagamento: Quais campos do cartão validar?
- Formato de CPF/CNPJ/Passaporte: Quais formatos aceitar?
- DDI do celular: Quais países suportar?
--otherros: Quaisquer outras validações não especificadas

### 1.5 Casos de Erro Não Detalhados
- Timeout de pagamento: Quanto tempo esperar?
- Falha na criação automática de conta: Como notificar o usuário?
- Concorrência (mesmo ingresso comprado simultaneamente): Como resolver conflito?
- Webhook de pagamento não recebido: Como lidar com falta de confirmação?
- Erro de API externa (Pay): Como tratar falhas?
- othersros:

## 2. Cenários de Teste Suggestivos

### 2.1 Cenários Happy Path
- Checkout nominal pago com todos os campos válidos
- Checkout nominal gratuito
- Checkout não nominal pago
- Checkout não nominal gratuito (usuário logado)
- Aplicação de cupom válido
- Pagamento aprovado em cada método (cartão, Pix, Boleto)
- Criação automática de conta com novo e-mail
- Criação automática de conta com e-mail existente

### 2.2 Cenários de Erro
- Campos obrigatórios não preenchidos
- Cupom inválido/expirado
- Pagamento recusado (cartão)
- Tempo expirado durante checkout (15 min)
- E-mail já existente (criar conta automática)
- Ingressos esgotados durante checkout
- CPF duplicado (se aplicável)
- Timeout de comunicação

### 2.3 Cenários de Edge Case
- Múltiplos tipos de ingresso no mesmo pedido
- Campos customizados obrigatórios configurados pelo organizador
- Usuário logado com dados salvos vs usuário novo
- Checkout interruption e retorno
- Sessão expirada com pagamento pendente
- Ingressos com valores diferentes no mesmo pedido
- Checkout com muitos participantes (performance)
- Usuário tenta acessar checkout de evento inexistente

## 3. Perguntas para o Product Owner

- [ ] Qual a linguagem/framework do backend?
- [ ] Qual banco de dados será utilizado?
- [ ] Qual sistema de autenticação será usado?
- [ ] Quais são os endpoints necessários para integração com o frontend?
- [ ] Qual o tempo de timeout para processamento de pagamento?
- [ ] Como lidar com falha na criação automática de conta?
- [ ] Quais validações específicas para campos customizados?
- [ ] O sistema deve suportar concorrência de compra do mesmo ingresso?
- [ ] Quais campos obrigatórios para criação de conta automática?
- [ ] Como funciona a reserva de estoque durante o checkout?
- [ ] Qual o comportamento quando webhook de pagamento não chega?
- [ ] Quais métricas de sucesso devem ser acompanhadas?

## 4. Sugestões de Implementação

Liste pontos que o desenvolvedor deve considerar no planejamento:
- Implementar sistema de reserva de estoque com TTL de 15 minutos
- Criar endpoint de status de checkout para o frontend pollar
- Implementar retry logic para chamadas ao Pay
- Considerar idempotência em process-payment
- Planejar cache de configuração de eventos
- Implementar logs detalhados para debug de pagamentos
- Considerar circuit breaker para API de pagamento
- Implementar webhooks para todos os status de pagamento
- Criar lógica de cleanup de sessões expiradas
