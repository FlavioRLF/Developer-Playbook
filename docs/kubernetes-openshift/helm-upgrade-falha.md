# Troubleshooting: falha em `helm upgrade`

## Sintomas

- `helm upgrade` retorna erro;
- a release fica em estado `failed` ou `pending-upgrade`;
- workloads não recebem a imagem ou os valores esperados.

## Diagnóstico

Confirme o contexto e o estado atual:

```bash
kubectl config current-context
helm status example-release --namespace example-namespace
helm history example-release --namespace example-namespace
```

Valide e renderize o chart antes de alterar o cluster:

```bash
helm lint path/to/chart
helm upgrade \
  example-release \
  path/to/chart \
  --namespace example-namespace \
  --dry-run=client \
  --debug \
  --hide-secret
```

`--dry-run --debug` pode exibir manifests, inclusive objetos `Secret`. Mantenha
`--hide-secret` e ainda assim não compartilhe a saída sem higienização.

Inspecione sinais do cluster:

```bash
kubectl get events \
  --namespace example-namespace \
  --sort-by='.metadata.creationTimestamp'
kubectl get pods --namespace example-namespace
```

## Solução

Corrija templates, valores, campos imutáveis, permissões ou readiness conforme
o diagnóstico. Após validar o render, uma atualização com reversão automática
pode ser executada:

```bash
helm upgrade \
  example-release \
  path/to/chart \
  --namespace example-namespace \
  --atomic \
  --timeout 10m
```

`--atomic` reverte as mudanças do upgrade quando a operação falha e implica
espera pelos recursos. Antes de usá-lo, confirme se hooks e migrações possuem
efeitos que o rollback do Helm não consegue desfazer.

## Validação

```bash
helm status example-release --namespace example-namespace
kubectl rollout status \
  deployment/example-service \
  --namespace example-namespace
```

Confirme também revisão, imagem, valores efetivos e sinais funcionais da
aplicação.

## Referência

- [Documentação oficial de `helm upgrade`](https://helm.sh/docs/helm/helm_upgrade/)
