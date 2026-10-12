# minhas-agent-skills

Repositório central de gerenciamento, versionamento e desenvolvimento de **Agent Skills** (habilidades modulares para agentes de IA).

---

## 1. Visão Geral da Estrutura Atual

O repositório está configurado para suportar múltiplos agentes de IA (como Claude Code, Hermes Agent, Antigravity, etc.) mantendo uma fonte única de verdade:

* **Gerenciamento e Lockfile**:
  * `skills-lock.json`: Arquivo de controle de dependências que rastreia as skills instaladas (atualmente mapeia a skill oficial `skill-creator` vinda de `anthropics/skills`).
  * `README.md`: Documentação e guia do repositório.

* **Diretório Canônico de Skills**:
  * `.agents/skills/`: Onde residem as implementações originais das skills.
  * `.agents/skills/skill-creator/`: Skill completa para criação, iteração e avaliação de novas skills:
    * `SKILL.md`: Manual e diretrizes de desenvolvimento de skills.
    * `scripts/`: Utilitários de automação e validação (como `package_skill.py`, `quick_validate.py`, `run_loop.py`).
    * `agents/` e `eval-viewer/`: Avaliadores e visualizadores de benchmarks.

* **Compatibilidade entre Ambientes**:
  * `.claude/skills/` e `.hermes/skills/`: Pastas que contêm links simbólicos (*symlinks*) apontando para as skills em `.agents/skills/`, permitindo o compartilhamento das skills sem duplicação de arquivos.

---

## 2. Padrão de Arquitetura para Novas Skills

Ao criar uma nova skill, deve-se seguir a estrutura canônica:

```
.agents/skills/<nome-da-skill>/
├── SKILL.md                          # Instruções principais, gatilhos e fluxo de trabalho
└── references/                       # Guias complementares (carregados sob demanda)
    ├── frameworks.md                 # Frameworks conceituais
    └── templates.md                  # Templates e recursos práticos
```

Para garantir compatibilidade entre os agentes, symlinks correspondentes devem ser criados nos ambientes suportados:
* `.claude/skills/<nome-da-skill>` -> `../../.agents/skills/<nome-da-skill>`
* `.hermes/skills/<nome-da-skill>` -> `../../.agents/skills/<nome-da-skill>`