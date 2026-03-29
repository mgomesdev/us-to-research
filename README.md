# us-to-research

Skill do OpenCode que converte requisitos abstratos escritos por Product Owners em um `research.md` estruturado para desenvolvimento.

## O que faz

Quando você (dev) recebe uma **User Story** do Product Owner, usa esta skill para:

1. **Criar** um novo `research.md` a partir de requisitos vagos
2. **Atualizar** um `research.md` existente quando os requisitos mudam

A skill segue o princípio: *"Siga o requisito original exatamente como fornecido. Não invente, não adicione e não assuma nada que não esteja expressamente definido na US."*

## Quando usar

Use esta skill sempre que:
- Receber uma nova User Story para implementar
- Precisar criar a documentação de pesquisa de uma feature
- Os requisitos de uma feature existente forem atualizados

## Como usar

### 1. Inicie a skill

No OpenCode, invoque a skill `us-to-research`.

### 2. Forneça o nome da feature

Digite o nome da feature em formato **kebab-case** (ex: `checkout`, `user-login`, `payment-flow`).

### 3. A skill verifica se a feature existe

- **Se não existir**: A skill cria a pasta da feature e um arquivo `prd.md` para você copiar o requisito do Product Owner.
- **Se existir**: A skill detecta que é para atualizar e solicita que você atualize o `prd.md` com as mudanças.

### 4. Adicione o conteúdo do requisito

Abra o arquivo `prd.md` criado e cole o requisito escrito pelo Product Owner.

### 5. Continue o processo

Retorne ao terminal e escolha a opção de continuar. A skill:
- Lê o conteúdo do `prd.md`
- Se houver ambiguidades, faz perguntas para esclarecer
- Gera o `research.md` estruturado com casos de uso separados

## Estrutura de arquivos

```
specs/
└── features/
    └── [nome-da-feature]/
        ├── prd.md       # Requisito original do Product Owner
        ├── research.md  # Documentação estruturada gerada
        └── uc-*/        # Casos de uso separados
            ├── uc-01/
            │   └── uc-01.md
            └── uc-02/
                └── uc-02.md
```

## Fluxo completo

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  User Story     │────▶│  us-to-research │────▶│  research.md    │
│  (PO)           │     │  (Skill)        │     │  + UCs         │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

1. **PO escreve** a User Story de forma abstrata
2. **Skill cria** a estrutura e solicita o conteúdo
3. **Dev copia** o requisito para `prd.md`
4. **Skill gera** o `research.md` com documentação técnica

## O que contém o research.md

O arquivo `research.md` inclui:

- **Atores** do sistema
- **Casos de Uso** identificados
- **Associações** entre casos de uso
- **Generalização/Especialização** quando aplicável
- **Inclusão** e **Extensão** de casos de uso
- **Restrições** e **Pontos de Extensão**
- **Multiplicidade** nas relações
- **Fronteira do Sistema**

## Regras importantes

- **Não invente**: Se a US não menciona algo, não inclua no research
- **Pergunte**: Se houver ambiguidade, tire dúvida com o usuário antes de supor
- **Mantenha sincronizado**: Ao atualizar, não remova conteúdo aprovado, apenas adicione o novo

## Configuração

Esta skill está configurada no arquivo `opencode.json` na raiz do projeto.

## Referências

- [SKILL.md](./.opencode/skills/us-to-research/SKILL.md) - Documentação técnica da skill
- [actor-and-uc.md](./.opencode/skills/us-to-research/references/actor-and-uc.md) - Referência para modelagem de atores e casos de uso
- [uc-spec-example.md](./.opencode/skills/us-to-research/assets/uc-spec-example.md) - Exemplo de especificação de caso de uso
