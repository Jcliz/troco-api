# AGENTS.md: troco-api

Instruções para qualquer agente de código neste repositório. (O Claude Code lê este arquivo pelo `CLAUDE.md`.)

## O que é

API do **troco**, sistema web de finanças pessoais: o usuário registra rendas e gastos e o sistema calcula quanto pode gastar no mês (margem) e quanto deve guardar (reserva). Toda regra de negócio e todo cálculo ficam aqui; o front (`troco-front`) só exibe.

## Stack

Node 24 LTS · pnpm · TypeScript strict · NestJS · Prisma · PostgreSQL 17 · Vitest · Supertest · nestjs-pino · @nestjs/swagger. Deploy na Vercel (serverless), banco no Neon.

## Comandos

```bash
docker compose up -d          # Postgres (5432) e Mailpit (UI em 8025)
pnpm install
pnpm start:dev                # API em http://localhost:4000
pnpm lint                     # ESLint
pnpm typecheck                # tsc --noEmit
pnpm test                     # unitários
pnpm test:integration         # integração (precisa do Postgres do Docker)
pnpm prisma migrate dev --name <nome>   # nova migração
pnpm openapi:generate         # regenera openapi.json (commitar o resultado)
pnpm build
```

> Até a tarefa API-01 do plano, o projeto ainda não existe: estes comandos são o alvo da tarefa.

## Onde está cada coisa

- `docs/PRD.md`: produto (requisitos RF-xx e RNF-xx). **A seção 8 tem as fórmulas.**
- `docs/plans/phase-1.md`: tarefas com critérios de aceite. Toda tarefa começa aqui.
- `docs/architecture.md`, `docs/data-model.md`, `docs/calculation.md`, `docs/api-contracts.md`.
- `docs/adr/`: decisões técnicas. Não contrarie um ADR sem propor um novo.
- `docs/conventions.md`: código, Git, testes e **glossário PT → EN** (use os nomes de lá).
- `src/modules/<dominio>/`: um módulo NestJS por domínio (controller → service → repository).
- `src/modules/calculation/`: motor de cálculo **puro**, sem Prisma nem NestJS.
- `prisma/schema.prisma` e `prisma/migrations/`.
- `openapi.json`: contrato gerado, consumido pelo front.

## Regras que não podem ser quebradas

1. **Dinheiro nunca é `number`.** Use `Prisma.Decimal`; na API, valores trafegam como string `"1234.56"` (ADR-0006).
2. **Datas de negócio são `date` (`AAAA-MM-DD`)**, nunca `new Date('AAAA-MM-DD')`. "Hoje" é no fuso do usuário (ADR-0008).
3. **Toda consulta de dado financeiro filtra por `ledgerId`** e toda rota de conta passa pelo `LedgerAccessGuard` (ADR-0011).
4. **Nada calculado é salvo** (margem, sobra, saldo remanescente): o motor recalcula (ADR-0007).
5. Erros em `application/problem+json` com `code` estável (ADR-0009). Novo código de erro vai em `docs/api-contracts.md`.
6. Nunca logar senha, token, e-mail completo ou valor de lançamento.
7. Nunca commitar `.env`, segredos ou dados reais.
8. Nunca pular, desativar ou enfraquecer teste para o CI passar.
9. Mudou contrato → `pnpm openapi:generate` e commit do `openapi.json`. Mudou o schema → migração nova (nunca editar migração já no `main`).
10. Mudou algo descrito em `docs/` → atualize o doc no mesmo PR **e** abra o PR irmão no `troco-front` (a pasta `docs/` é idêntica nos dois).

## Git

Branch por tarefa (`feat/api-07-period-turnover`), Conventional Commits em inglês, PR pequeno com o template, squash merge após CI verde e revisão do João.

## Idioma

Código, commits e PRs em inglês. Documentação e textos para o usuário em português.
