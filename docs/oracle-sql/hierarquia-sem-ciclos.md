# Impedir ciclos na escolha do pai

## Sintoma

Uma operação de edição aceita o próprio nó ou um de seus descendentes como novo
pai, tornando a hierarquia cíclica.

## Diagnóstico

Liste a subárvore do nó que será movido:

```sql
SELECT id
FROM example_entity
START WITH id = :current_id
CONNECT BY NOCYCLE PRIOR id = parent_id;
```

Se `:candidate_parent_id` estiver nesse resultado, a escolha é inválida.

## Filtrar pais válidos

```sql
WITH descendants AS (
    SELECT id
    FROM example_entity
    START WITH id = :current_id
    CONNECT BY NOCYCLE PRIOR id = parent_id
)
SELECT candidate.id, candidate.name
FROM example_entity candidate
WHERE NOT EXISTS (
    SELECT 1
    FROM descendants descendant
    WHERE descendant.id = candidate.id
)
ORDER BY candidate.name, candidate.id;
```

A subconsulta exclui o nó atual e todos os seus descendentes. Confirme o plano e
o comportamento na versão do Oracle usada pela aplicação.

## Proteção em camadas

- filtre opções inválidas na interface;
- repita a validação no backend dentro da operação de escrita;
- execute leitura e atualização com controle transacional apropriado;
- adicione testes para autorreferência, filho direto e descendente profundo;
- monitore violações como eventos de domínio, sem registrar dados sensíveis.

Uma chave estrangeira garante que o pai existe, mas não impede ciclos
arbitrários no auto relacionamento.

## Validação

- o próprio nó não aparece como candidato;
- nenhum descendente aparece como candidato;
- um ancestral ou nó de outra árvore continua disponível quando permitido;
- uma tentativa direta contra o backend também é rejeitada.

Para exibir a árvore preservando sua ordem, consulte
[Ordenação de consultas hierárquicas](ordenacao-e-hierarquia.md).
