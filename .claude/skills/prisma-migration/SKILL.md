---
name: prisma-migration
description: Muda o schema Prisma do troco-api e cria a migração com segurança, incluindo SQL manual para índices parciais e CHECK. Use em qualquer mudança de tabela ou coluna.
---

# Mudança de schema

1. Edite `prisma/schema.prisma` seguindo `docs/data-model.md` e `.claude/rules/prisma.md`.
2. `pnpm prisma format && pnpm prisma validate`.
3. `pnpm prisma migrate dev --create-only --name <verbo_objeto>` (ex.: `add_seasonal_plans`).
4. Abra o SQL gerado e acrescente o que o Prisma não gera (índice único parcial, `CHECK`, `NULLS NOT DISTINCT`), com comentário.
5. `pnpm prisma migrate dev` para aplicar; `pnpm prisma generate`.
6. Coluna nova obrigatória em tabela com dados: crie com default ou em duas etapas (nullable → preencher → `NOT NULL`).
7. Escreva teste de integração para cada restrição nova.
8. Atualize `docs/data-model.md` no mesmo PR.
Nunca edite migração que já está no `main`.
