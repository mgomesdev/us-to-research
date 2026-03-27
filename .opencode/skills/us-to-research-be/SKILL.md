---
name: us-to-research-be
description: "Converte requisitos abstratos escritos por Product Owners em um research.md estruturado para desenvolvimento Backend. Documenta endpoints, schemas e integrações. Use esta skill quando receber uma User Story para desenvolvimento backend."
license: MIT
compatibility: opencode
metadata:
  version: 1.0.0
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

## Passo a Passo

### Etapa 1: Receber o requisito

Solicite ao usuário (se não fornecido):
- O **nome da feature** no formato `nome-da-feature-be`
- O **conteúdo do requisito** (texto do Notion, US, briefing, etc.)
- O **nome da feature de frontend** vinculada (ex: `nome-da-feature`)

Verifique se existe `backend/specs/features/[nome-da-feature]/research.md`. Se existir, leia-o antes de continuar.

### Etapa 2: Mapear APIs fornecidas

Liste todas as APIs que o Backend fornecerá:

```markdown
### Contratos Fornecidos (Backend)
| ID | Endpoint | Método | Descrição | Schema | Auth |
|----|----------|--------|-----------|--------|------|
| API-001 | /users | GET | Lista usuários | User[] | JWT |
| API-002 | /users | POST | Cria usuário | CreateUserDTO | JWT |
```

### Etapa 3: Perguntas de esclarecimento

Faça **3 a 5 perguntas essenciais** quando o requisito for ambíguo:

1. Qual tecnologia/framework backend? (Node.js, Python, Go, etc.)
2. Qual banco de dados? (PostgreSQL, MongoDB, etc.)
3. O frontend research já existe?

Se o requisito já for claro, pule esta etapa.

### Etapa 4: Documentar schemas de dados

Para cada endpoint, defina:

```markdown
### API-001: GET /users

**Request:**
- Headers: `Authorization: Bearer <token>`

**Response 200:**
```json
{
  "data": [
    { "id": "uuid", "email": "string", "name": "string" }
  ],
  "meta": { "total": 0, "page": 1, "perPage": 20 }
}
```

**Response 401:** Unauthorized
**Response 500:** Internal Server Error
```

### Etapa 5: Gerar e salvar o research.md

Gere o arquivo e salve em `backend/specs/features/[nome-da-feature]/research.md`.

## Estrutura do research.md (Backend)

```markdown
# [Nome da Feature] - Backend

## 1. Visão Geral
Descrição em 2–4 linhas do que será construído no backend e qual problema resolve.

## 2. Objetivos
- Objetivo específico e mensurável 1
- Objetivo específico e mensurável 2

## 3. Stack Técnica
- **Linguagem/Framework:** [Node.js/Express, Python/FastAPI, etc.]
- **Banco de Dados:** [PostgreSQL, MongoDB, etc.]
- **ORM/ODM:** [Prisma, TypeORM, Mongoose, etc.]
- **Autenticação:** [JWT, OAuth, sessão, etc.]

## 4. Integração com Frontend

### 4.1 Frontend Vinculado
- **linked_fe:** `frontend/specs/features/[nome-fe]/research.md`
- **contract:** `specs/contracts/[nome]/contract.md`

### 4.2 Contratos Fornecidos
| ID | Endpoint | Método | Descrição | Schema | Auth | Status |
|----|----------|--------|-----------|--------|------|--------|
| API-001 | /users | GET | Lista usuários | User[] | JWT | ⏳ Pending |
| API-002 | /users | POST | Cria usuário | CreateUserDTO | JWT | ⏳ Pending |

## 5. Endpoints

### API-001: GET /users

**Descrição:** Lista usuários com paginação.

**Request:**
- Headers: `Authorization: Bearer <token>`
- Query: `page`, `perPage`, `search`

**Response 200:**
```json
{
  "data": [
    {
      "id": "uuid",
      "email": "string",
      "name": "string",
      "createdAt": "ISO8601"
    }
  ],
  "meta": {
    "total": 0,
    "page": 1,
    "perPage": 20
  }
}
```

**Response 401:** Unauthorized
**Response 500:** Internal Server Error

### API-002: POST /users

**Descrição:** Cria um novo usuário.

**Request:**
```json
{
  "email": "string",
  "name": "string",
  "password": "string"
}
```

**Response 201:**
```json
{
  "id": "uuid",
  "email": "string",
  "name": "string",
  "createdAt": "ISO8601"
}
```

**Response 400:** Validation Error
**Response 409:** Conflict (email já existe)
**Response 500:** Internal Server Error

## 6. Data Models

### User
```typescript
interface User {
  id: string;        // UUID v4
  email: string;      // unique, valid email
  name: string;       // 2-100 chars
  password: string;   // hashed (bcrypt)
  createdAt: Date;
  updatedAt: Date;
}

interface CreateUserDTO {
  email: string;
  name: string;
  password: string;
}
```

## 7. Validações

| Campo | Regra |
|-------|-------|
| email | Formato válido, único no banco |
| name | Min 2, max 100 caracteres |
| password | Min 8 caracteres |

## 8. Erros

| Código | Mensagem | Causa |
|--------|----------|-------|
| 400 | Validation failed | Dados inválidos |
| 401 | Unauthorized | Token ausente/inválido |
| 409 | Conflict | Email duplicado |
| 500 | Internal Server Error | Erro interno |

## 9. Requisitos Funcionais
- RF-01: O backend deve validar todos os inputs
- RF-02: O backend deve retornar erros estruturados
- RF-03: O backend deve suportar paginação

## 10. Requisitos Não-Funcionais
- RNF-01: Tempo de resposta < 200ms para listagens
- RNF-02: Autenticação via JWT
- RNF-03: Logs de requisição

## 11. Fora do Escopo
- Não inclui [funcionalidade X]
- Não implementa [feature Y]

## 12. Questões em Aberto
- [ ] [Dúvida a ser respondida]
```

## Regras

- **Escreva para um dev júnior ou agente de IA** — seja explícito
- **Documentação completa de endpoints** — inclua schemas, erros, auth
- **Nomenclatura consistente** — siga REST conventions
- **Segurança primeiro** — documente auth, validações

## Output

Ao final, apresente o resumo:

```
✅ research.md BE gerado em backend/specs/features/[nome]/research.md

Resumo:
- X endpoints documentados
- Contratos Fornecidos: [lista de APIs]
- Schema de dados: [lista de models]
- Frontend vinculado: frontend/specs/features/[nome-fe]/research.md

⚠️ Status: [PROSSEGUIR / BLOQUEADO]

Próximos Passos:
- Se PROSSEGUIR: Executar 'sync-contracts' para gerar contrato
```
