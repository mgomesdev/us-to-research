# Checkout - Backend

## 1. Visão Geral
Refatoração do checkout do Linka Eventos para tela única organizada em três blocos sequenciais: dados dos participantes, recebimento do ingresso, e pagamento/dados do comprador. Inclui criação automática de conta para checkouts que permitem compra sem login.

## 2. Stack Técnica
- **Linguagem/Framework:** A definir com o time dev
- **Banco de Dados:** A definir com o time dev
- **Autenticação:** A definir com o time dev

## 3. Integração com Frontend

### 3.1 Frontend Vinculado
A definir - não mencionado na US

### 3.2 Contratos Fornecidos
não mencionado na US

## 4. Endpoints
não mencionado na US

## 5. Data Models
não mencionado na US

## 6. Validações
A US menciona as seguintes validações:
- **Bloco 1 - Dados dos participantes:** Campos obrigatórios: nome, e-mail, celular (com DDI)
- **Campos customizados:** CPF, empresa, cargo ou outros configurados pelo organizador com obrigatoriedade definida
- **Bloco 2 - Responsável pelosingressos:** Quando selecionado "Outro": nome completo, e-mail, celular obrigatórios
- **Termos e condições:**Checkbox obrigatórios para avanço

## 7. Erros
A US menciona os seguintes erros:
- **Cupom:** inválido, expirado ou não encontrado - exibir mensagem abaixo do campo
- **Pagamento cartão recusado:** retornar ao bloco de pagamento mantendo dados, exibir mensagem de erro

## 8. Requisitos Funcionais
A US menciona as seguintes regras de comportamento:
- RF-01: Checkout nominal pago - exibe Bloco 1 com campos por participante, Bloco 2 com dropdown de responsável, Bloco 3 com métodos de pagamento, cria conta automaticamente
- RF-02: Checkout nominal gratuito - exibe Bloco 1, Bloco 2 com dropdown, não exibe Bloco 3 de pagamento, cria conta automaticamente
- RF-03: Checkout não nominal pago - não exibe Bloco 1, Bloco 2 sem dropdown, Bloco 3 com métodos de pagamento, cria conta automaticamente
- RF-04: Checkout não nominal gratuito - exige autenticação antes de acessar checkout, não exibe Bloco 1, exibe Bloco 2, não exibe Bloco 3
- RF-05: Criação automática de conta com dados do responsável pelosingressos ao concluir checkout
- RF-06: Se e-mail já existe, usar conta existente sem criar duplicada
- RF-07: Cupom de desconto - validar ao clicar "Adicionar", apenas um cupom por pedido
- RF-08: Reservar ingressos por 15 minutos com contador regressivo
- RF-09: Ao expirar tempo, redirecionar para página do evento com inúmerosingressos liberados
- RF-10: Processamento de pagamento via cartão, Pix e Boleto
- RF-11: Enviar e-mail de boas-vindas com link de criação de senha após criação automática de conta
- RF-12: Enviar e-mail com ingressoss após confirmação do pagamento

## 9. Requisitos Não-Funcionais
A US menciona:
- RNF-01: Tempo de expiração do checkout: 15 minutos

## 10. Métricas de Sucesso
A definir com o Product Owner

## 11. Fora do Escopo
Tópico 10 - Proteção e segurança do checkout: "A definir com o time dev"

## 12. Questões em Aberto
- Nome da feature de frontend vinculada para integração
- Endpoints necessários para comunicação Frontend-Backend
- Data Models necessários para支撑 o checkout
- Stack técnica completa
- Implementação de proteção e segurança do checkout
- Quaisquer outras APIs necessárias para integração
