# Skills e plugins de terceiros

Skills copiadas de repositórios públicos depois de auditadas (SKILL.md, referências, scripts e hooks lidos em busca de instruções maliciosas, envio de dados e comandos perigosos). Os arquivos estão **idênticos ao original** no commit indicado. Para atualizar, copie de novo a partir do repositório de origem e audite o diff antes do commit.

Auditoria feita em 2026-11-23.

## Skills copiadas para `.claude/skills/`

| Skill | Origem (commit) | Licença | Observações |
|---|---|---|---|
| `tlc-spec-driven` | [tech-leads-club/agent-skills](https://github.com/tech-leads-club/agent-skills) `d0c46bf`, pasta `packages/skills-catalog/skills/(development)/tlc-spec-driven` | MIT (catálogo) / CC-BY-4.0 (skill, autor Felipe Rodrigues) | Scripts Python locais de validação; `check_proofs.py` executa os comandos de prova escritos na própria spec. Sem rede. |
| `grill-me` e `grilling` | [mattpocock/skills](https://github.com/mattpocock/skills) `abeeaf9`, pastas `skills/productivity/grill-me` e `skills/productivity/grilling` | MIT | Só texto. `grill-me` só roda quando chamada (`/grill-me`) e carrega `grilling`. Ficou de fora `grill-with-docs`: ela usa a skill `domain-modeling`, que cria `GLOSSARY.md` na raiz e ADRs num formato próprio, em conflito com `docs/adr/` e o glossário de `docs/conventions.md`. |

Skills de design e frontend (impeccable, frontend-design, ip-as-logo e as do Emil Kowalski) ficaram só no troco-front, porque a API não tem interface.

## Plugins habilitados em `settings.json`

O Claude Code pergunta se você quer instalar estes plugins ao abrir o repositório.

| Plugin | Marketplace | Observações |
|---|---|---|
| `superpowers` | `claude-plugins-official` (aponta para [obra/superpowers](https://github.com/obra/superpowers) `22f0b46`) | Tem hook de início de sessão que injeta a skill `using-superpowers`. As regras do `CLAUDE.md`/`AGENTS.md` continuam valendo acima dela. |
| `claude-code-setup` | `claude-plugins-official` ([anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official)) | Skill `claude-automation-recommender`, só leitura. |
| `cartographer` | `cartographer-marketplace` ([kingbootoshi/cartographer](https://github.com/kingbootoshi/cartographer) `a62d169`) | Script Python local que conta tokens. Grava `docs/CODEBASE_MAP.md` e edita o `CLAUDE.md`: como `docs/` é espelhada no troco-api, rode só se quiser o mapa nos dois repos. |

O MCP do Playwright está só no troco-front (`.mcp.json`). O do Figma já está conectado na conta do claude.ai.
