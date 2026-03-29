# Diretrizes para Agentes

Este repositório contém a skill **us-to-research** do OpenCode para conversão de requisitos em research.md estruturado.

## Estrutura do Projeto

```
us-to-research/
├── README.md                    # Documentação principal
├── AGENTS.md                    # Diretrizes para agentes
├── opencode.json                # Configuração do OpenCode
├── specs/
│   └── features/
│       └── [feature-name]/
│           ├── prd.md           # Requisito original do PO
│           ├── research.md      # Documentação estruturada gerada
│           └── uc-*/            # Casos de uso separados
└── .opencode/
    ├── skills/
    │   └── us-to-research/
    │       ├── SKILL.md         # Skill principal
    │       ├── references/
    │       │   └── actor-and-uc.md    # Referência para atores e casos de uso
    │       └── assets/
    │           └── uc-spec-example.md # Exemplo de especificação de UC
    └── package.json             # Dependências do OpenCode
```

## Fluxo de Git

- Use commits convencionais: `feat:`, `fix:`, `docs:`, `chore:`
- Formato da mensagem de commit: `tipo(escopo): descrição`
- Exemplo: `feat: adicionar nova skill us-to-research`

## Documentação

- Mantenha o README.md atualizado com a documentação da skill
- Documente propósito, gatilhos e exemplos de uso no README.md
- O arquivo SKILL.md deve ser autocontido e bem estruturado
