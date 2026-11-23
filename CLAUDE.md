# CLAUDE.md: troco-api

@AGENTS.md

## Como trabalhar neste repo (Claude Code)

Você escreve praticamente todo o código; o João revisa os PRs. Ele lê em português.

### Fluxo de uma tarefa

Use a skill **`implement-task`** (`/implement-task API-07`). Resumo:

1. Leia a tarefa em `docs/plans/phase-1.md` e os docs/ADRs que ela cita. Releia os RFs do PRD envolvidos.
2. Se algo estiver ambíguo ou em conflito com um ADR, pare e pergunte antes de codar. Não invente regra de negócio.
3. Crie a branch, implemente em passos pequenos, com testes junto (TDD no motor de cálculo).
4. Rode `pnpm lint && pnpm typecheck && pnpm test && pnpm test:integration && pnpm build`.
5. Rode o subagente **`reviewer`** no diff antes de abrir o PR.
6. Abra o PR com o template, ligando a tarefa e os RFs, e explique em português no corpo como testar.

### Estrutura da pasta `.claude/`

| Caminho | Para quê |
|---|---|
| `settings.json` | Permissões (comandos liberados, arquivos bloqueados) e hooks |
| `hooks/format.sh` | Formata com Prettier cada arquivo editado |
| `rules/*.md` | Regras carregadas conforme o caminho do arquivo editado (dinheiro, Prisma, controllers, testes, cálculo) |
| `agents/reviewer.md` | Revisa o diff contra ADRs, PRD e convenções |
| `agents/test-writer.md` | Escreve testes a partir dos critérios de aceite e do PRD |
| `skills/implement-task/` | Passo a passo de uma tarefa do plano até o PR |
| `skills/new-api-module/` | Como criar um módulo de domínio no padrão do projeto |
| `skills/prisma-migration/` | Como mudar o schema e criar migração com segurança |

### Lembretes

- Prefira mudar pouco e certo. Refatoração fora do escopo vira tarefa separada (anote no PR).
- Ao terminar uma tarefa, marque-a como feita no plano (`docs/plans/phase-1.md`) no mesmo PR.
- Ponto não decidido vira "Pontos em aberto" no doc correspondente, nunca uma decisão silenciosa no código.
