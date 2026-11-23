---
paths:
  - "src/**/*.controller.ts"
  - "src/**/*.dto.ts"
  - "src/common/**"
---

# Controllers e DTOs

- Siga `docs/api-contracts.md`: prefixo `/v1`, recursos de conta em `/v1/ledgers/:ledgerId/...`, JSON em `camelCase`.
- Controller fino: valida (DTO com `class-validator`), chama o service, devolve. Sem regra de negócio no controller.
- Todo endpoint tem decorators do `@nestjs/swagger` (`@ApiOperation`, respostas e DTOs de saída) para o `openapi.json` sair completo.
- Erros de regra lançam `DomainError` com `code` estável (ex.: `PERIOD_ALREADY_OPEN`); o filtro global converte em problem+json. Código novo → adicionar em `docs/api-contracts.md`.
- Usuário sem acesso ao ledger recebe `404`, não `403`.
- Rotas públicas marcadas com `@Public()`; todo o resto exige sessão.
- Depois de mudar contrato: `pnpm openapi:generate` e commitar `openapi.json`.
