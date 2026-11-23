---
paths:
  - "prisma/**"
  - "src/**/*.repository.ts"
  - "src/prisma/**"
---

# Prisma e banco

- O schema segue `docs/data-model.md`. Mudou o schema → atualize o doc no mesmo PR.
- Tabelas e colunas em `snake_case` com `@@map`/`@map`; modelos em `PascalCase`, campos em `camelCase`.
- Toda consulta de dado financeiro tem `where: { ledgerId }`. Nunca `findUnique({ where: { id } })` sozinho para dado de conta.
- Restrições que o Prisma não expressa (índice parcial, `CHECK`, `NULLS NOT DISTINCT`) vão em SQL dentro da migração, com comentário no schema.
- Nunca edite uma migração que já está no `main`; crie outra. Nunca use `db push` nem `migrate reset` fora do banco de teste.
- Operações que mexem em várias tabelas (virada do mês, exclusão de conta) usam `prisma.$transaction`.
- Acesso ao Prisma só em repositories; services não importam `PrismaService` direto.
