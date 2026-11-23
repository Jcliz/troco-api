---
name: implement-task
description: Implementa uma tarefa do plano de fase do troco-api (ex. API-07) do início ao PR, seguindo docs, ADRs e definição de pronto. Use quando pedirem para fazer uma tarefa do plano.
---

# Implementar uma tarefa do plano

Argumento: o ID da tarefa (ex.: `API-07`).

1. **Entender**
   - Ache a tarefa em `docs/plans/phase-*.md`. Confira se as dependências ("Depende de") já estão no `main`. Se não estiverem, pare e avise.
   - Leia os docs e ADRs citados e os RFs do PRD envolvidos.
   - Liste para si os critérios de aceite. Ambiguidade ou conflito com ADR → pergunte ao João antes de codar.
2. **Preparar**
   - `git switch main && git pull && git switch -c feat/<id-minúsculo>-<resumo-em-inglês>`.
   - `docker compose up -d` se a tarefa envolve banco.
3. **Implementar**
   - Comece pelos testes dos critérios de aceite (use o subagente `test-writer` se ajudar).
   - Siga as regras de `.claude/rules/` e o padrão da skill `new-api-module` para módulos novos; `prisma-migration` para schema.
   - Commits pequenos em Conventional Commits.
4. **Verificar**
   - `pnpm lint && pnpm typecheck && pnpm test && pnpm test:integration && pnpm build`.
   - Contrato mudou: `pnpm openapi:generate` e commit.
   - Rode o subagente `reviewer` e corrija o que for "Bloqueia".
5. **Documentar**
   - Atualize `docs/` se algo descrito mudou e marque a tarefa como feita no plano (`✅` no título). Mudou `docs/`? Anote no PR que precisa do PR irmão no troco-front.
6. **Abrir o PR**
   - Título em Conventional Commits. Corpo pelo template, em português: tarefa, RFs, o que mudou, como testar, pontos de atenção.
