# Kubernetes e OpenShift

## Tópicos

- [Inventário de releases Helm por namespace](helm-list-por-namespace.md)
- [Troubleshooting: falha em `helm upgrade`](helm-upgrade-falha.md)

## Contexto atual

```bash
kubectl config current-context
kubectl config get-contexts
kubectl config view --minify
```

No OpenShift:

```bash
oc whoami
oc project
```

Confirme cluster e namespace antes de qualquer alteração.

## Inspecionar recursos

```bash
kubectl get pods --namespace example-namespace
kubectl describe pod example-pod --namespace example-namespace
kubectl logs example-pod --namespace example-namespace --all-containers
kubectl get events --namespace example-namespace \
  --sort-by='.metadata.creationTimestamp'
```

## Diagnóstico dentro do pod

```bash
kubectl exec --namespace example-namespace -it example-pod -- sh
```

## Rollout

```bash
kubectl rollout status deployment/example-service \
  --namespace example-namespace
kubectl rollout history deployment/example-service \
  --namespace example-namespace
```

## Checklist para pods indisponíveis

1. estado e `reason` do container;
2. eventos do pod;
3. logs atuais e anteriores com `--previous`;
4. requests, limits e quotas;
5. probes;
6. configuração, secrets e service accounts;
7. DNS, services, routes/ingresses e network policies.

Nunca copie o conteúdo de `Secret` para a documentação.
