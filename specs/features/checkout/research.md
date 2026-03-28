# Checkout - Research

## 1. Atores

| Ator | Descrição | Estéreotipo |
|------|-----------|-------------|
| Participante | Usuário que realiza a compra ou inscrição em um evento | - |
| Sistema de Pagamento | Sistema integrado que processa pagamentos (Pay, operadores de cartão) | system |
| Sistema Financeiro | Sistema que processa Pix e Boleto | system |

## 2. Casos de Uso

| UC | Nome | Ator Principal | Tipo |
|----|------|----------------|------|
| [UC01](./uc01/uc01.md) | Preencher Dados dos Participantes | Participante | Primário |
| [UC02](./uc02/uc02.md) | Selecionar Responsável pelos Ingressos | Participante | Primário |
| [UC03](./uc03/uc03.md) | Selecionar Método de Pagamento | Participante | Primário |
| [UC04](./uc04/uc04.md) | Preencher Dados do Comprador | Participante | Primário |
| [UC05](./uc05/uc05.md) | Aplicar Cupom de Desconto | Participante | Secundário |
| [UC06](./uc06/uc06.md) | Finalizar Checkout com Cartão de Crédito | Participante | Primário |
| [UC07](./uc07/uc07.md) | Finalizar Checkout com Pix | Participante | Primário |
| [UC08](./uc08/uc08.md) | Finalizar Checkout com Boleto | Participante | Primário |
| [UC09](./uc09/uc09.md) | Finalizar Checkout Gratuito | Participante | Primário |
| [UC10](./uc10/uc10.md) | Criar Conta Automaticamente | Participante | Secundário |
| [UC11](./uc11/uc11.md) | Exibir Tela de Confirmação | Participante | Primário |

## 3. Associações

| Ator | Caso de Uso | Tipo de Associação |
|------|-------------|-------------------|
| Participante | UC01 - Preencher Dados dos Participantes | - |
| Participante | UC02 - Selecionar Responsável pelos Ingressos | - |
| Participante | UC03 - Selecionar Método de Pagamento | - |
| Participante | UC04 - Preencher Dados do Comprador | - |
| Participante | UC05 - Aplicar Cupom de Desconto | - |
| Participante | UC06 - Finalizar Checkout com Cartão de Crédito | - |
| Participante | UC07 - Finalizar Checkout com Pix | - |
| Participante | UC08 - Finalizar Checkout com Boleto | - |
| Participante | UC09 - Finalizar Checkout Gratuito | - |
| Participante | UC10 - Criar Conta Automaticamente | - |
| Participante | UC11 - Exibir Tela de Confirmação | - |
| Sistema de Pagamento | UC06 - Finalizar Checkout com Cartão de Crédito | include |
| Sistema Financeiro | UC07 - Finalizar Checkout com Pix | include |
| Sistema Financeiro | UC08 - Finalizar Checkout com Boleto | include |

## 4. Regras de Comportamento por Tipo de Ingresso

### Checkout Nominal Pago
- Exibe Bloco 1 com campos por participante
- Exibe Bloco 2 com dropdown de responsável
- Exibe Bloco 3 com métodos de pagamento
- Cria conta automaticamente com dados do responsável pelos ingressos ao concluir

### Checkout Nominal Gratuito
- Exibe Bloco 1 com campos por participante
- Exibe Bloco 2 com dropdown de responsável
- Não exibe Bloco 3 com campos de pagamento
- Cria conta automaticamente com dados do responsável pelos ingressos ao concluir

### Checkout Não Nominal Pago
- Não exibe Bloco 1
- Exibe Bloco 2 sem dropdown
- Exibe Bloco 3 com métodos de pagamento
- Cria conta automaticamente com dados do responsável pelos ingressos ao concluir

### Checkout Não Nominal Gratuito
- Exige autenticação do participante antes de acessar o checkout
- Não exibe Bloco 1
- Exibe Bloco 2
- Não exibe Bloco 3
- Usa conta do usuário autenticado
