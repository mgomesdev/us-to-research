---
name: us-to-research-fe
description: "Converte requisitos abstratos escritos por Product Owners em um research.md estruturado para desenvolvimento Frontend. Gera contrato de integração com o Backend. Use esta skill quando receber uma User Story para desenvolvimento frontend."
license: MIT
compatibility: opencode
metadata:
  version: 1.0.1
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

## Regra Fundamental

**SIGA O REQUISITO ORIGINAL EXATAMENTE COMO FORNECIDO. NÃO INVENTE, NÃO ADICIONE E NÃO SUPONHA NADA QUE NÃO ESTEJA EXPRESSAMENTE DEFINIDO NA US.**

Se a US não menciona algo, não inclua no research. Se há ambiguidade,pergunte ao usuário antes de supor.

## Passo a Passo

### Etapa 1: Receber o requisito

Solicite ao usuário (se não fornecido):
- O **nome da feature** no formato `nome-da-feature`
- O **conteúdo do requisito** (texto do Notion, US, briefing, etc.)

Verifique se existe `frontend/specs/features/[nome-da-feature]/research.md`. Se existir, leia-o antes de continuar.

### Etapa 2: Gerar e salvar o research.md

Gere o arquivo e salve em `frontend/specs/features/[nome-da-feature]/research.md`.

## Estrutura do research.md (Frontend)

O research.md deve incluir **todas as seções abaixo**, porém o conteúdo de cada seção deve ser extraído **APENAS** do que está expressamente definido na US. Se a US não mencionar uma informação específica, a seção deve indicar "A definir" ou listar como questão em aberto.

```markdown
# [Nome da Feature] - Frontend

## 1. Visão Geral
Descrição em 2–4 linhas do que será construído no frontend conforme US.

## 2. Estrutura
Inclua todas as subseções que a US definir (ex: "Estrutura Geral do Checkout", "Bloco 1", "Bloco 2", etc.)
Se a US não definir subseções, não crie.

## 3. [Seções Adicionais da US]
Inclua todas as seções/tópicos adicionais que a US mencionar (ex: "Criação Automática de Conta", "Cupom de Desconto", etc.)

## 4. Requisitos Funcionais
Liste APENAS os requisitos explicitamente mencionados na US:
- RF-01: [requisito exatamente como na US]
(continue numeração sequencial)

## 5. Requisitos Não-Funcionais
Liste APENAS os requisitos explicitamente mencionados na US:
- RNF-01: [requisito exatamente como na US]

## 6. Métricas de Sucesso
Se a US mencionar métricas, liste-as.
Se a US não mencionar, indique: "A definir com o Product Owner" e liste as métricas genéricas que poderiam ser sugeridas.

## 7. Fora do Escopo
Liste APENAS o que a US mencionar como fora do escopo.

## 8. Questões em Aberto
Liste:
- Questões que a US deixar em aberto explicitamente
- Tópicos que a US marcar como "A definir"
- Seções opcionais que a US não mencionar (ex: proteção e segurança, etc.)
```

## Regras

- **SIGA A US AO PÉ DA LETRA** — nenhuma adição, interpretação ou invenção
- **Todas as seções devem existir** — mas o conteúdo pode ser "A definir" ou "não mencionado na US"
- **Seção "Integração com Backend"** — inclua APENAS as APIs que a US mencionar explicitamente
- **Seção "Dependências"** — inclua apenas se a US mencionar dependências
- **Seção "Histórias de Usuário"** — inclua APENAS se a US fornecer histórias detalhadas
- **Seção "Referências Visuais"** — inclua APENAS o que a US fornecer (ex: protótipo mencionado)

### Etapa 3: Gerar e salvar o gaps.md

Além do research.md, gere um segundo arquivo com os cenários e informações que faltaram ser especificadas na US. Este arquivo serve como base para conferência com o Product Owner e inspiração para o desenvolvedor no planejamento.

Gere o arquivo em `frontend/specs/features/[nome-da-feature]/gaps.md`.

## Estrutura do gaps.md (Frontend)

```markdown
# [Nome da Feature] - gaps & Planning

## 1. Informações Faltantes para Desenvolvimento

### 1.1 Contratos de API Necessários
Liste os endpoints que o frontend provavelmente precisará consumir:
- GET /events/:id/checkout-config - para obter configuração do checkout
- POST /checkout/validate-coupon - para validar cupom de desconto
- POST /checkout/process-payment - para processar pagamento
- POST /checkout/create-account - para criar conta automática
- GET /checkout/:id/status - para verificar status do pagamento
- (outros endpoints que o dev precisar definir baseado nos fluxos)

### 1.2 Estados de Loading/Error Não Detalhados
- Loading ao carregar configuração do evento:
- Loading ao validar cupom:
- Loading ao processar pagamento:
- Loading ao criar conta:
- Tratamento de erros de rede:
- Tratamento de timeouts:

### 1.3 Componentes UI Não Especificados
- Componentes de formulários necessários:
- Componentes de display de erros:
- Componentes de loading:
- Componentes de resumo do pedido:
- Outros componentes:

### 1.4 edge Cases de UX Não Detalhados
- O que acontece se o usuário fecha a aba durante checkout:
- O que acontece se o usuário atualiza a página:
- Persistência de dados do formulário entre sessões:
- Validação em tempo real vs validação no submit:
- Ordenação de validações de campos:

## 2. Cenários de Teste Suggestivos

### 2.1 Cenários Happy Path
- Fluxo completo de checkout nominal pago
- Fluxo completo de checkout nominal gratuito
- Fluxo completo de checkout não nominal pago
- Fluxo completo de checkout não nominal gratuito (logado)
- Aplicação de cupom válido com sucesso
- Remoção de cupom aplicado

### 2.2 Cenários de Interrupção
- Usuário fecha navegador durante checkout
- Usuário clica em "voltar" do navegador
- Sessão expira durante checkout
- Tempo expirado (15 min)

### 2.3 Cenários de Erro
- Campos obrigatórios não preenchidos
- CPF/CNPJ inválido
- E-mail em formato inválido
- Celular em formato inválido
- Cupom inválido/expirado
- Pagamento recusado
- Timeout de comunicação com servidor

### 2.4 Cenários de Usuário Logado
- Usuário com dados salvos vs sem dados salvos
- Usuário altera dados salvos
- Usuário desmarca "salvar dados"
- Usuário com cartão salvo

## 3. Fluxos de Navegação Não Especificados

- Rota para tela de checkout:
- Rota para tela de sucesso:
- Rota para tela de "Aguardando pagamento" (boleto):
- Comportamento do botão "voltar" entre blocos:
- Redirecionamento após expiração de tempo:
- Retorno ao checkout após login (checkout não nominal gratuito):

## 4. Casos de edge Case Visuais

- Como exibir muitos participantes (scroll):
- Como exibir muitos tipos de ingresso:
- Como exibir campos customizados longos:
- Responsividade em mobile:
- Orientação landscape em mobile:

## 5. Perguntas para o Product Owner

Liste todas as dúvidas que surgiram ao analisar a US:
- [ ] ...
- [ ] ...

## 6. Sugestões de Implementação

Liste pontos que o desenvolvedor deve considerar no planejamento:
- Componentização sugerida
- Gerenciamento de estado (formulário, checkout session)
- Integração com provider de pagamento
- Tratamento de concorrência de estoque
- Accessibility considerations
- Internacionalização
```

## Regras Adicionais gaps.md

- ** NÃO inventa respostas** — apenas lista as perguntas/informações que faltam
- Use o gaps.md como ferramenta de alinhamento com o PO
- O desenvolvedor deve usar este arquivo como base para planning poker

## Output

Ao final, apresente o resumo:

```
✅ research.md FE gerado em frontend/specs/features/[nome]/research.md
✅ gaps.md FE gerado em frontend/specs/features/[nome]/gaps.md

Resumo:
- Estrutura segue exatamente a US fornecida
- Seções incluídas: Visão Geral, Estrutura, RFs, RNFs, Métricas, Fora do Escopo, Questões em Aberto
- Contratos Consumidos: [APENAS os mencionados na US]
- Gaps identificados: [quantidade de itens em cada seção]

⚠️ Status: [PRECISA CLARIFICAR / PROSSEGUIR]
- Se precisar clarificar: listar ambiguidades encontradas na US
- Seções com "A definir": [lista]
- Perguntas para o PO: [lista das dúvidas]
```
