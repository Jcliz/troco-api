---
paths:
  - "**/*.spec.ts"
  - "**/*.int-spec.ts"
  - "test/**"
---

# Testes

- Unitários: `*.spec.ts` ao lado do código. Integração: `*.int-spec.ts` em `test/`, contra Postgres real, com banco limpo por teste.
- Nome do teste em inglês, descrevendo comportamento: `it('rejects turnover with a future salary date')`.
- Use o `Clock` falso; nada depende da data real nem da ordem dos testes.
- Teste de integração de rota de conta sempre inclui o caso "usuário de outro ledger recebe 404".
- Valores monetários nos testes como string (`'1900.00'`) comparados com `Decimal.equals`.
- Proibido `.skip`, `.only` commitado ou afrouxar asserção para passar.
