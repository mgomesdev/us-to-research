---
name: us-to-research-be
description: "Converte requisitos abstratos escritos por Product Owners em um research.md estruturado para desenvolvimento Backend. Documenta endpoints, schemas e integrações. Use esta skill quando receber uma User Story para desenvolvimento backend."
license: MIT
compatibility: opencode
metadata:
  version: 1.0.1
  user-invocable: true
  triggers:
    - "converter us em research backend"
    - "criar research backend"
    - "us-to-research-be"
---

# Skill: us-to-research-be

## Quando Usar

- Quando receber uma User Story para desenvolvimento **Backend**
- Quando precisar documentar o que o Backend **fornece** ao Frontend
- Deve ser usada ANTES de `sync-contracts`

## Regra Fundamental

**SIGA O REQUISITO ORIGINAL EXATAMENTE COMO FORNECIDO. NÃO INVENTE, NÃO ADICIONE E NÃO SUPONHA NADA QUE NÃO ESTEJA EXPRESSAMENTE DEFINIDO NA US.**

Se a US não menciona algo, não inclua no research. Se há ambiguidade,pergunte ao usuário antes de supor.

## Passo a Passo

### Etapa 1: Receber o requisito

Solicite ao usuário (se não fornecido):
- O **nome da feature** no formato `nome-da-feature-be`
- O **conteúdo do requisito** (texto do Notion, US, briefing, etc.)
- O **nome da feature de frontend** vinculada (ex: `nome-da-feature`)

Verifique se existe `backend/specs/features/[nome-da-feature]/research.md`. Se existir, leia-o antes de continuar.

### Etapa 2: Gerar e salvar o research.md

Gere o arquivo e salve em `backend/specs/features/[nome-da-feature]/research.md`.

## Estrutura do research.md (Backend)

O research.md deve incluir **todas as seções abaixo**, porém o conteúdo de cada seção deve ser extraído **APENAS** do que está expressamente definido na US. Se a US não mencionar uma informação específica, a seção deve indicar "A definir" ou listar como questão em aberto.

```markdown
# [Nome da Feature] - Backend

## 1. Visão Geral
Descrição em 2–4 linhas do que será construído no backend conforme US.

## 2. Stack Técnica
Se a US mencionar tecnologias específicas, liste-as:
- **Linguagem/Framework:** [informado na US ou "A definir"]
- **Banco de Dados:** [informado na US ou "A definir"]
- **Autenticação:** [informado na US ou "A definir"]

Se a US não mencionar, indique: "A definir com o time dev"

## 3. Integração com Frontend

### 3.1 Frontend Vinculado
Se a US mencionar frontend vinculado:
- **linked_fe:** `frontend/specs/features/[nome-fe]/research.md`

### 3.2 Contratos Fornecidos
Liste APENAS as APIs que a US mencionar explicitamente:
| ID | Endpoint | Método | Descrição | Auth | Status |
|----|----------|--------|-----------|------|--------|
| API-001 | /events/:id/checkout-config | GET | Configuração do checkout | - | ⏳ Pending |

## 4. Endpoints
Documente APENAS os endpoints explicitamente mencionados na US.

Para cada endpoint:
```markdown
### API-001: [MÉTODO] [Endpoint]

**Descrição:** [Descrição exatamente como na US]

**Request:**
[Descreva APENAS o que a US mencionar]

**Response:**
[Descreva APENAS os códigos de status que a US mencionar]

**Response 200/201:**
```json
{ /* schema se a US mencionar */ }
```
```

## 5. Data Models
Liste APENAS os models explicitamente mencionados na US.
Se a US não mencionar, não crie esta seção.

## 6. Validações
Liste APENAS as validações explicitamente mencionadas na US.
Se a US não mencionar, não crie esta seção.

## 7. Erros
Liste APENAS os erros explicitamente mencionados na US.
Se a US não mencionar, não crie esta seção.

## 8. Requisitos Funcionais
Liste APENAS os requisitos explicitamente mencionados na US:
- RF-01: [requisito exatamente como na US]

## 9. Requisitos Não-Funcionais
Liste APENAS os requisitos explicitamente mencionados na US:
- RNF-01: [requisito exatamente como na US]

## 10. Métricas de Sucesso
Se a US mencionar métricas, liste-as.
Se a US não mencionar, indique: "A definir com o Product Owner"

## 11. Fora do Escopo
Liste APENAS o que a US mencionar como fora do escopo.

## 12. Questões em Aberto
Liste:
- Questões que a US deixar em aberto explicitamente
- Tópicos que a US marcar como "A definir"
- Stack técnica não mencionada na US
```

## Regras

- **SIGA A US AO PÉ DA LETRA** — nenhuma adição, interpretação ou invenção
- **Todas as seções devem existir** — mas o conteúdo pode ser "A definir" ou "não mencionado na US"
- **Endpoints** — documente APENAS os explicitamente mencionados na US
- **Data Models** — crie APENAS se a US mencionar entidades/dados específicos
- **Validações e Erros** — liste APENAS os explicitamente citados na US

### Etapa 3: Gerar e salvar o gaps.md

Além do research.md, gere um segundo arquivo com os cenários e informações que faltaram ser especificadas na US. Este arquivo serve como base para conferência com o Product Owner e inspiração para o desenvolvedor no planejamento.

Gere o arquivo em `backend/specs/features/[nome-da-feature]/gaps.md`.

## Estrutura do gaps.md (Backend)

```markdown
# [Nome da Feature] - gaps & Planning

## 1. Informações Faltantes para Desenvolvimento

### 1.1 Stack Técnica
- Linguagem/Framework esperado:
- Banco de dados:
- Autenticação/Autorização:
- Provedor de pagamento (se aplicável):
- Outras tecnologias:

### 1.2 Integração com Frontend
- Nome da feature de frontend vinculada:
- Contratos/Endpoints necessários (a definir):
  - GET /events/:id/checkout-config
  - POST /checkout/validate-coupon
  - POST /checkout/process-payment
  - POST /checkout/create-account
  - GET /checkout/:id/status
  - (outros endpoints que o dev precisar definir)

### 1.3 Data Models Necessários
Liste os models que provavelmente serão necessários baseado na feature:
- Order/Checkout
- Participant
- Ticket
- Payment
- Coupon
- User (para conta automática)
- (outros que o dev identificar)

### 1.4 Validações Faltantes
Liste validações que a US menciona mas não detalha:
- Validação de campos customizados por ingresso:
- Regras de validação de pagamento:
- Outros:

### 1.5 Casos de Erro Não Detalhados
- Timeout de pagamento:
- Falha na criação automática de conta:
- Concorrência (mesmo ingresso comprado simultaneamente):
- Webhook de pagamento não recebido:
- Outros:

## 2. Cenários de Teste Suggestivos

### 2.1 Cenários Happy Path
- Checkout nominal pago com todos os campos válidos
- Checkout nominal gratuito
- Checkout não nominal pago
- Checkout não nominal gratuito (usuário logado)
- Aplicação de cupom válido
- Pagamento aprovado em cada método (cartão, Pix, Boleto)

### 2.2 Cenários de Erro
- Campos obrigatórios não preenchidos
- Cupom inválido/expirado
- Pagamento recusado (cartão)
- Tempo expirado durante checkout
- E-mail já existente (criar conta automática)
- Ingressos esgotados durante checkout

### 2.3 Cenários de Edge Case
- Múltiplos tipos de ingresso no mesmo pedido
- Campos customizados obrigatórios configurados pelo organizador
- Usuário logado com dados salvos vs usuário novo
- Checkout interruption e retorno
- Sessão expirada com pagamento pendente

## 3. Perguntas para o Product Owner

Liste todas as dúvidas que surgiram ao analisar a US:
- [ ] ...
- [ ] ...

## 4. Sugestões de Implementação

Liste pontos que o desenvolvedor deve considerar no planejamento:
- Ordem de implementação sugerida
- Dependências entre funcionalidades
- Possíveis refatorações necessárias
- Performance considerations
- Segurança a considerar
```

## Regras Adicionais gaps.md

- ** NÃO inventa respostas** — apenas lista as perguntas/informações que faltam
- Use o gaps.md como ferramenta de alinhamento com o PO
- O desenvolvedor deve usar este arquivo como base para planning poker

## Output

Ao final, apresente o resumo:

```
✅ research.md BE gerado em backend/specs/features/[nome]/research.md
✅ gaps.md BE gerado em backend/specs/features/[nome]/gaps.md

Resumo:
- Estrutura segue exatamente a US fornecida
- Endpoints documentados: [APENAS os mencionados na US]
- Stack Técnica: [A definir / informada na US]
- Frontend vinculado: [informado na US ou "A definir"]
- Gaps identificados: [quantidade de itens em cada seção]

⚠️ Status: [PRECISA CLARIFICAR / PROSSEGUIR]
- Se precisar clarificar: listar ambiguidades encontradas na US
- Seções com "A definir": [lista]
- Perguntas para o PO: [lista das dúvidas]
```
