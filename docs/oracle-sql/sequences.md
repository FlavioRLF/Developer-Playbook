# Sequences e `NEXTVAL`

## Objetivo

Gerar identificadores numéricos de forma concorrente sem usar estratégias
inseguras como `MAX(id) + 1`.

## Gerar e inserir

```sql
SELECT example_entity_seq.NEXTVAL
FROM dual;
```

O uso direto no `INSERT` evita uma ida adicional ao banco:

```sql
INSERT INTO example_entity (id, name)
VALUES (example_entity_seq.NEXTVAL, :name);
```

Quando a aplicação precisa receber o valor criado:

```sql
INSERT INTO example_entity (id, name)
VALUES (example_entity_seq.NEXTVAL, :name)
RETURNING id INTO :generated_id;
```

## `CURRVAL`

Depois que a mesma sessão chamou `NEXTVAL`, ela pode consultar o último valor
obtido:

```sql
SELECT example_entity_seq.CURRVAL
FROM dual;
```

`CURRVAL` é específico da sessão; ele não representa o maior identificador da
tabela nem o valor mais recente gerado por outras sessões.

## Validação

Valide o identificador retornado pelo próprio `INSERT` e a existência da linha:

```sql
SELECT id, name
FROM example_entity
WHERE id = :generated_id;
```

Não use `MAX(id)` para confirmar um insert concorrente.

## Comportamento esperado

- rollbacks não devolvem valores consumidos;
- cache, falhas e concorrência podem produzir lacunas;
- sequência garante geração, não numeração contígua;
- não use o valor para inferir ordem de negócio sem um campo próprio para isso.

## Referência

- [Pseudocolunas de sequence no Oracle](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Sequence-Pseudocolumns.html)
