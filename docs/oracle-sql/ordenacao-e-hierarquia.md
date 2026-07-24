# Ordenação de consultas hierárquicas

## Objetivo

Consultar uma árvore pai-filho com profundidade e ordenação previsível no
Oracle.

## Estrutura de exemplo

```text
example_entity(id, parent_id, name)
```

## Consulta

```sql
SELECT
    id,
    parent_id,
    name,
    LEVEL AS depth,
    SYS_CONNECT_BY_PATH(TO_CHAR(id), '/') AS path
FROM example_entity
START WITH id = :root_id
CONNECT BY NOCYCLE PRIOR id = parent_id
ORDER SIBLINGS BY name, id;
```

- `START WITH` define a raiz;
- `PRIOR id = parent_id` liga o pai aos filhos;
- `LEVEL` informa a profundidade, começando em `1`;
- `NOCYCLE` evita que dados cíclicos interrompam a consulta;
- `ORDER SIBLINGS BY` ordena irmãos sem desmontar a hierarquia.

`ORDER SIBLINGS BY name, id` usa `id` como desempate, tornando estável a ordem
entre nomes iguais.

## Detectar ciclos existentes

```sql
SELECT
    id,
    parent_id,
    CONNECT_BY_ISCYCLE AS is_cycle
FROM example_entity
START WITH id = :root_id
CONNECT BY NOCYCLE PRIOR id = parent_id;
```

`CONNECT_BY_ISCYCLE = 1` sinaliza uma relação que fecha um ciclo.

## Validação

- a raiz aparece com `depth = 1`;
- cada filho aparece depois do respectivo pai;
- irmãos estão ordenados por `name` e `id`;
- a consulta termina mesmo diante de dados cíclicos.

Para impedir a criação de novos ciclos, consulte
[Impedir ciclos na escolha do pai](hierarquia-sem-ciclos.md).

## Referência

- [Consultas hierárquicas no Oracle](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Hierarchical-Queries.html)
