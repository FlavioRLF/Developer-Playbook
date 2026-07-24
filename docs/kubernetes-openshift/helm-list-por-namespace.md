# Inventário de releases Helm por namespace

## Objetivo

Listar releases e identificar versões implantadas dentro de um namespace.

## Pré-requisitos

- Helm 3 ou versão compatível.
- Contexto Kubernetes válido.
- Permissão de leitura no namespace.

Confirme o alvo antes da consulta:

```bash
kubectl config current-context
kubectl auth can-i get secrets --namespace example-namespace
```

## Procedimento

```bash
helm list --namespace example-namespace --max 50
```

Para uma saída adequada a scripts:

```bash
helm list \
  --namespace example-namespace \
  --max 50 \
  --output json
```

Filtros de status ajudam a reduzir o resultado:

```bash
helm list \
  --namespace example-namespace \
  --deployed \
  --failed
```

Use `--all-namespaces` somente quando a análise realmente exigir visão global e
a conta tiver as permissões correspondentes.

## Validação

```bash
helm status example-release --namespace example-namespace
helm history example-release --namespace example-namespace
```

`helm list` encerra com código zero mesmo quando não encontra releases. Em
automação, valide também se a saída possui itens.

## Referência

- [Documentação oficial de `helm list`](https://helm.sh/docs/helm/helm_list/)
