# Histórico recente com `git log`

## Objetivo

Listar commits recentes para apoiar análise de mudanças e rastreabilidade.

## Pré-requisitos

- Git instalado.
- Diretório atual dentro de um repositório Git.
- Histórico local atualizado quando a análise incluir referências remotas.

## Procedimento

```bash
git --no-pager log \
  --since="7 days ago" \
  --oneline \
  --decorate
```

- `--no-pager` envia o resultado diretamente ao terminal;
- `--since` define o início do período;
- `--oneline` resume cada commit;
- `--decorate` mostra branches e tags apontando para os commits.

Por padrão, o comando percorre os commits alcançáveis a partir de `HEAD`. Para
incluir todas as referências locais conhecidas:

```bash
git --no-pager log \
  --all \
  --since="7 days ago" \
  --oneline \
  --decorate \
  --graph
```

Antes de analisar referências remotas, atualize-as sem alterar a árvore de
trabalho:

```bash
git fetch --all --prune
```

## Validação

```bash
git rev-parse --is-inside-work-tree
```

O resultado esperado é `true`. A consulta de log é somente leitura e pode
retornar vazia quando não houver commits no período.

## Referência

- [Documentação oficial de `git log`](https://git-scm.com/docs/git-log)
