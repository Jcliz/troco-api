---
name: new-api-module
description: Cria um módulo de domínio NestJS no padrão do troco-api (controller, service, repository, DTOs, testes). Use ao começar um domínio novo como periods, entries ou categories.
---

# Novo módulo de domínio

Estrutura em `src/modules/<dominio>/` (nome no plural, em inglês, conforme o glossário de `docs/conventions.md`):

```
<dominio>.module.ts
<dominio>.controller.ts        # rotas, DTOs, swagger; sem regra de negócio
<dominio>.service.ts           # regras; lança DomainError com code
<dominio>.repository.ts        # único lugar com Prisma; sempre filtra por ledgerId
dto/
  create-<entidade>.dto.ts
  update-<entidade>.dto.ts
  <entidade>.response.ts       # formato de saída (dinheiro como string)
<dominio>.service.spec.ts      # unitário das regras
test/<dominio>.int-spec.ts     # integração das rotas (na pasta test/)
```

Checklist:
- Registrar o módulo no `AppModule`.
- Rotas de conta: `@Controller('ledgers/:ledgerId/<recurso>')` + `LedgerAccessGuard`.
- Mapear entidade Prisma → response DTO (nunca devolver o objeto do Prisma direto).
- Swagger completo e `pnpm openapi:generate`.
- Códigos de erro novos em `docs/api-contracts.md`.
