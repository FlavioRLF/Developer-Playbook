# Oracle SQL

## Identificar sessão e banco

```sql
SELECT
    SYS_CONTEXT('USERENV', 'SESSION_USER') AS session_user,
    SYS_CONTEXT('USERENV', 'SERVICE_NAME') AS service_name
FROM dual;
```

## Inspecionar estrutura

```sql
SELECT column_name, data_type, nullable
FROM user_tab_columns
WHERE table_name = UPPER('example_table')
ORDER BY column_id;
```

## Paginação determinística

```sql
SELECT id, created_at, status
FROM example_table
ORDER BY created_at DESC, id DESC
OFFSET 0 ROWS FETCH NEXT 50 ROWS ONLY;
```

Inclua um critério único no `ORDER BY` para evitar resultados instáveis.

## Plano de execução

```sql
EXPLAIN PLAN FOR
SELECT *
FROM example_table
WHERE status = :status;

SELECT *
FROM TABLE(DBMS_XPLAN.DISPLAY);
```

## Transações

```sql
SAVEPOINT before_change;

UPDATE example_table
SET status = :new_status
WHERE id = :id;

ROLLBACK TO before_change;
-- COMMIT somente após validar o resultado.
```

Sempre teste alterações com um filtro seletivo e valide a quantidade de linhas
afetadas. Não use dados reais nos exemplos.
