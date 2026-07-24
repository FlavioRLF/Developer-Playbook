# Troubleshooting: `GROUP BY` inválido

## Sintoma

O Oracle retorna `ORA-00979: not a GROUP BY expression` em uma consulta
agregada.

## Causa

Uma expressão usada no `SELECT`, `HAVING` ou `ORDER BY` não faz parte do
agrupamento, não é constante e não está dentro de uma função agregadora.

Exemplo inválido:

```sql
SELECT category, description, SUM(amount) AS total_amount
FROM example_item
GROUP BY category;
```

`description` não possui um único valor definido para cada grupo de `category`.

## Soluções

Agrupe pela granularidade realmente desejada:

```sql
SELECT category, description, SUM(amount) AS total_amount
FROM example_item
GROUP BY category, description;
```

Ou, quando a regra de negócio define como consolidar a descrição, agregue-a
explicitamente:

```sql
SELECT
    category,
    MIN(description) AS first_description,
    SUM(amount) AS total_amount
FROM example_item
GROUP BY category;
```

Não adicione `MIN` ou `MAX` apenas para silenciar o erro; confirme que a escolha
representa a regra de negócio.

Para expressões extensas, calcule-as primeiro em uma CTE:

```sql
WITH prepared AS (
    SELECT
        CASE WHEN amount >= 100 THEN 'HIGH' ELSE 'STANDARD' END AS amount_band,
        amount
    FROM example_item
)
SELECT amount_band, SUM(amount) AS total_amount
FROM prepared
GROUP BY amount_band;
```

## Validação

- a consulta executa sem `ORA-00979`;
- a quantidade de grupos corresponde à chave escolhida;
- totais conferem com uma amostra independente;
- `ORDER BY` e `HAVING` usam somente expressões válidas no resultado agrupado.

## Referência

- [Explicação oficial do erro ORA-00979](https://docs.oracle.com/en/error-help/db/ora-00979/)
