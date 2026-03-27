---
name: us-to-research-fe
description: "Converte requisitos abstratos escritos por Product Owners em um research.md estruturado para desenvolvimento Frontend. Gera contrato de integração com o Backend. Use esta skill quando receber uma User Story para desenvolvimento frontend."
license: MIT
compatibility: opencode
metadata:
  version: 1.0.0
  user-invocable: true
  triggers:
    - "converter us em research frontend"
    - "criar research frontend"
    - "us-to-research-fe"
---

# Skill: us-to-research-fe

## Quando Usar

- Quando receber uma User Story para desenvolvimento **Frontend**
- Quando precisar documentar o que o Frontend **consome** do Backend

## Passo a Passo

### Etapa 1: Receber o requisito

Solicite ao usuário (se não fornecido):
- O **nome da feature** no formato `nome-da-feature`
- O **conteúdo do requisito** (texto do Notion, US, briefing, etc.)

Verifique se existe `frontend/specs/features/[nome-da-feature]/research.md`. Se existir, leia-o antes de continuar.

### Etapa 2: Verificar dependências 

Quando a feature for uma **page, template ou organism** que contém componentes filhos:

1. Liste os componentes filhos mencionados (Button, Card, Header, etc.)
2. Para cada componente filho, verifique se já foi implementado:
   - Existe `frontend/specs/features/[nome-do-componente]/research.md`?
   - Existe `frontend/specs/features/[nome-do-componente]/plan.md`?
   - Existe `frontend/specs/features/[nome-do-componente]/*.feature`?
3. Classifique cada componente:
   - ✅ **Implementado:** possui research, plan e *.feature
   - ⚠️ **Parcialmente implementado:** possui research e/ou plan, sem *.feature completo
   - ❌ **Não implementado:** não existe ou está incompleto
4. Se algum filho está ❌ ou ⚠️:
   - Marcar como **BLOCKED por dependências**
   - Listar dependências faltantes no research
   - **NÃO criar *.feature** até dependências resolvidas

### Etapa 3: Perguntas de esclarecimento

Faça **3 a 5 perguntas essenciais** quando o requisito for ambíguo:

1. Esta feature altera uma tela existente ou cria uma nova?
2. Qual backend endpoint/API ela irá consumir?

Se o requisito já for claro, pule esta etapa.

### Etapa 4: Mapear APIs consumidas

Liste todas as APIs que o Frontend consumirá:

```markdown
### Contratos Consumidos (Backend)
| ID | Endpoint | Método | Descrição | Status |
|----|----------|--------|-----------|--------|
| API-001 | /users | GET | Lista usuários | ⏳ Pending contract |
| API-002 | /users/:id | GET | Detalhes usuário | ⏳ Pending contract |
```

### Etapa 5: Gerar e salvar o research.md

Gere o arquivo e salve em `frontend/specs/features/[nome-da-feature]/research.md`.

## Estrutura do research.md (Frontend)

```markdown
# [Nome da Feature] - Frontend

## 1. Visão Geral
Descrição em 2–4 linhas do que será construído no frontend e qual problema resolve.

## 2. Objetivos
- Objetivo específico e mensurável 1
- Objetivo específico e mensurável 2

## 3. Integração com Backend

### 3.1 Backend Vinculado
- **contract:** `specs/contracts/[nome]/contract.md`

### 3.2 Contratos Consumidos
| ID | Endpoint | Método | Descrição | Status |
|----|----------|--------|-----------|--------|
| API-001 | /users | GET | Lista usuários | ⏳ Pending |

### 3.3 Data Flow

```
[User Action] → [Frontend State] → [API Call: API-001] → [Backend] → [Response] → [UI Update]
```

### 3.4 Estados de Integração
| Estado | Comportamento UI |
|--------|-----------------|
| Loading | Skeleton/spinner no local |
| Success | Renderizar dados |
| Error | Toast/message com retry |
| Empty | Empty state designado |

## 4. Histórias de Usuário
Cada história deve ser pequena o suficiente para ser implementada em uma única sessão.

### US-001: [Título]
**Descrição:** Como [usuário], eu quero [ação] para que [benefício].
**Tela/Componente afetado:** [nome]
**APIs consumidas:** API-001, API-002
**Critérios de aceitação:**
- [ ] Critério visual verificável
- [ ] Critério de comportamento
- [ ] Critério de integração (API-XXX)

## 5. Dependências 
> ⚠️ **Seção obrigatória

| Componente | Tipo | Status | Caminho |
|------------|------|--------|---------|
| Button | atom | ✅ Implementado | specs/features/button/ |
| Card | molecule | ⚠️ Parcial | - |
| Header | organism | ❌ Não implementado | - |

## 6. Requisitos Funcionais
- RF-01: O sistema deve [comportamento]
- RF-02: Quando o usuário [ação], a interface deve [resposta]

## 7. Requisitos Não-Funcionais
- RNF-01: Componentes responsivos (mobile-first)
- RNF-02: Estados de loading durante chamadas API
- RNF-03: Erros de validação inline

## 8. Fora do Escopo
- Não inclui [funcionalidade X]
- Não altera [tela Y]

## 9. Referências Visuais
- Link Figma: [url ou "não disponível"]
- Componentes reutilizáveis: [lista]

## 10. Métricas de Sucesso
- Como será medido que a feature atingiu seu objetivo

## 11. Questões em Aberto
- [ ] [Dúvida a ser respondida]
```

## Regras

- **Escreva para um dev júnior ou agente de IA** — seja explícito
- **Critérios de aceitação são verificáveis**, não vagos
- **Não misture frontend e backend** — o critério é visual/comportamental
- **Integração é contrato** — documente o que consome, não como o backend implementa

## Output

Ao final, apresente o resumo:

```
✅ research.md FE gerado em frontend/specs/features/[nome]/research.md

Resumo:
- X histórias de usuário
- Principais telas/componentes: [lista]
- Contratos Consumidos: [lista de APIs]
- Backend vinculado: backend/specs/features/[nome-be]/research.md

⚠️ Status: [PROSSEGUIR / BLOQUEADO]
- Se BLOQUEADO: listar dependências necessárias
```
