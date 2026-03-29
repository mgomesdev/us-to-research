# Checkout - Research

## 1. Atores

| Ator | Descrição | Estéreo tipo |
|------|-----------|--------------|
| Participante | Usuário que está realizando a compra de-ingressos em um evento | |
| Organizador | Usuário que cria e configura o evento e-ingressos | |
| Sistema de Pagamento | Sistema externo que processa os pagamentos (Pix, Cartão, Boleto) | <system> |

## 2. Casos de Uso

| UC | Nome | Ator Principal | Tipo |
|----|------|----------------|------|
| UC01 | Preencher dados dos participantes | Participante | Primário |
| UC02 | Selecionar responsável pelosingressos | Participante | Primário |
| UC03 | Selecionar método de pagamento | Participante | Primário |
| UC04 | Preencher dados do comprador | Participante | Primário |
| UC05 | Aplicar cupom de desconto | Participante | Secundário |
| UC06 | Finalizar compra | Participante | Primário |
| UC07 | Criar conta automaticamente | Participante | Primário |
| UC08 | Processar pagamento via cartão | Participante | Primário |
| UC09 | Processar pagamento via Pix | Participante | Primário |
| UC10 | Processar pagamento via boleto | Participante | Primário |
| UC11 | Exibir tela de confirmação | Participante | Primário |

## 3. Documentação dos Casos de Uso

Consulte os arquivos individuais na pasta `./uc/` para detalhamento de cada caso de uso.

### 3.1 Casos de Uso Gerados

- [UC01 - Preencher dados dos participantes](./uc/uc-01/uc-01.md)
- [UC02 - Selecionar responsável pelosingressos](./uc/uc-02/uc-02.md)
- [UC03 - Selecionar método de pagamento](./uc/uc-03/uc-03.md)
- [UC04 - Preencher dados do comprador](./uc/uc-04/uc-04.md)
- [UC05 - Aplicar cupom de desconto](./uc/uc-05/uc-05.md)
- [UC06 - Finalizar compra](./uc/uc-06/uc-06.md)
- [UC07 - Criar conta automaticamente](./uc/uc-07/uc-07.md)
- [UC08 - Processar pagamento via cartão](./uc/uc-08/uc-08.md)
- [UC09 - Processar pagamento via Pix](./uc/uc-09/uc-09.md)
- [UC10 - Processar pagamento via boleto](./uc/uc-10/uc-10.md)
- [UC11 - Exibir tela de confirmação](./uc/uc-11/uc-11.md)

### 3.2 Associações entre Casos de Uso

#### 3.2.1 Inclusão

| Caso de Uso | Include |
|-------------|---------|
| UC06 - Finalizar compra | UC07 - Criar conta automaticamente |
| UC06 - Finalizar compra | UC08 - Processar pagamento via cartão (quando método for cartão) |
| UC06 - Finalizar compra | UC09 - Processar pagamento via Pix (quando método for Pix) |
| UC06 - Finalizar compra | UC10 - Processar pagamento via boleto (quando método for boleto) |
| UC06 - Finalizar compra | UC11 - Exibir tela de confirmação |

#### 3.2.2 Extensão

| Caso de Uso | Extend | Condição |
|-------------|--------|----------|
| UC04 - Preencher dados do comprador | UC04 - Pré-preenchimento de dados | Quando usuário logado possui dados salvos |

#### 3.2.3 Generalização/Especialização

Não aplicável para esta feature.

### 3.3 Restrições em Associações de Extensão

- O caso de uso UC04 - Preencher dados do comprador pode ser estendido para pré-preencher dados quando o usuário logado possui dados salvos de compras anteriores

## 4. Associações

| Ator | Caso de Uso | Associação |
|------|--------------|------------|
| Participante | UC01 | |
| Participante | UC02 | |
| Participante | UC03 | |
| Participante | UC04 | |
| Participante | UC05 | |
| Participante | UC06 | |
| Participante | UC07 | |
| Participante | UC08 | |
| Participante | UC09 | |
| Participante | UC10 | |
| Participante | UC11 | |
| Organizador | UC01 | Fornece campos customizados |
| Sistema de Pagamento | UC08 | <include> |
| Sistema de Pagamento | UC09 | <include> |
| Sistema de Pagamento | UC10 | <include> |

## 5. Inclusão

Consulte a seção 3.2.1 para detalhamento das associações de inclusão entre casos de uso.

## 6. Extensão

Consulte a seção 3.2.2 para detalhamento das associações de extensão entre casos de uso.

## 7. Estereótipos

| Estereótipo | Descrição |
|-------------|-----------|
| <system> | Representa sistemas externos que interagem com o sistema (ex: Sistema de Pagamento) |

## 8. Restrições em Associações de Extensão

Consulte a seção 3.3 para detalhamento das restrições em associações de extensão.

## 9. Pontos de Extensão

Não aplicável para esta feature.

## 10. Multiplicidade

| Associação | Multiplicidade |
|------------|----------------|
| Participante -> UC01 a UC11 | 1:N |
| Sistema de Pagamento -> UC08, UC09, UC10 | 1:1 |

## 11. Fronteira de Sistema

A fronteira de sistema para esta feature engloba todos os casos de uso relacionados ao processo de checkout do Linka Eventos:

```
┌─────────────────────────────────────────────────────────────┐
│                    SISTEMA: LINKA EVENTOS                    │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              FRONTEIRA: CHECKOUT                     │    │
│  │                                                      │    │
│  │  UC01 - Preencher dados dos participantes          │    │
│  │  UC02 - Selecionar responsável pelosingressos      │    │
│  │  UC03 - Selecionar método de pagamento             │    │
│  │  UC04 - Preencher dados do comprador               │    │
│  │  UC05 - Aplicar cupom de desconto                  │    │
│  │  UC06 - Finalizar compra                           │    │
│  │  UC07 - Criar conta automaticamente                │    │
│  │  UC08 - Processar pagamento via cartão             │    │
│  │  UC09 - Processar pagamento via Pix                │    │
│  │  UC10 - Processar pagamento via boleto             │    │
│  │  UC11 - Exibir tela de confirmação                │    │
│  │                                                      │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
└─────────────────────────────────────────────────────────────┘

ATORES EXTERNOS:
- Participante
- Organizador
- Sistema de Pagamento (<system>)
```

## 12. Comportamentos por Tipo de Checkout

### 12.1 Checkout Nominal Pago

- Exibe Bloco 1 com campos por participante
- Exibe Bloco 2 com dropdown de responsável
- Exibe Bloco 3 com métodos de pagamento
- Cria conta automaticamente com dados do responsável pelosingressos ao concluir

### 12.2 Checkout Nominal Gratuito

- Exibe Bloco 1 com campos por participante
- Exibe Bloco 2 com dropdown de responsável
- Não exibe Bloco 3 com campos de pagamento
- Cria conta automaticamente com dados do responsável pelosingressos ao concluir

### 12.3 Checkout Não Nominal Pago

- Não exibe Bloco 1
- Exibe Bloco 2 com campos manuais (sem dropdown)
- Exibe Bloco 3 com métodos de pagamento
- Cria conta automaticamente com dados do responsável pelosingressos ao concluir

### 12.4 Checkout Não Nominal Gratuito

- Exige autenticação do participante antes de acessar o checkout
- Se não logado, redireciona para login/cadastro
- Após autenticação, retorna ao checkout
- Não exibe Bloco 1
- Exibe Bloco 2
- Não exibe Bloco 3
