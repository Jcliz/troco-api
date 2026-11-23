---
paths:
  - "src/modules/calculation/**"
  - "src/modules/summary/**"
---

# Motor de cálculo

- A especificação é `docs/calculation.md`, que implementa a seção 8 do PRD. Leia os dois antes de mudar qualquer fórmula.
- `calculation` é puro: sem Prisma, sem NestJS, sem `Date` atual, sem I/O. Recebe dados, devolve resultado.
- Toda fórmula tem teste unitário; os "casos de teste obrigatórios" de `docs/calculation.md` não podem ser removidos.
- Cada função cita o requisito em comentário (`// PRD 8.4`, `// RF-76`).
- Fórmula diferente do documento = pare e pergunte. Nunca "corrija" a regra por conta própria.
