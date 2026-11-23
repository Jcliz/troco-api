---
paths:
  - "src/**/*.ts"
---

# Dinheiro e datas

- Dinheiro é `Prisma.Decimal` em todo lugar. Proibido `number`, `parseFloat`, `toFixed` para conta. Entrada e saída da API como string decimal (`"1234.56"`). Use o utilitário `src/common/money`.
- Arredonde só no resultado final (2 casas, `ROUND_HALF_UP`).
- Percentuais são frações em `Decimal` (`0.1000` = 10%).
- Datas de negócio (`date`, `startDate`, `expectedDate`) são strings `AAAA-MM-DD` na API e `@db.Date` no banco. Converta só com `src/common/calendar-date`.
- "Hoje" vem do `Clock` injetado, no fuso do usuário (`user.timezone`). Nunca `new Date()` direto em regra de negócio.
