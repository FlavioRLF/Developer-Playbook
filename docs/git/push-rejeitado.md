# Troubleshooting: push rejeitado

## Sintomas

- o remoto rejeita o push como `non-fast-forward`;
- uma regra exige pull request, histórico linear ou commit assinado;
- autenticação, autorização ou um hook do servidor bloqueia a atualização.

## Diagnóstico

Confirme a branch e atualize apenas as referências remotas:

```bash
git status --short --branch
git fetch origin --prune
git branch --verbose --verbose
```

Compare os dois lados do histórico:

```bash
git log \
  --left-right \
  --graph \
  --oneline \
  HEAD...origin/feature/example-change
```

- linhas iniciadas por `<` existem somente na branch local;
- linhas iniciadas por `>` existem somente na branch remota;
- a mensagem do servidor identifica políticas de proteção ou assinatura.

## Solução

Se a branch remota avançou e os commits locais ainda podem ser reaplicados:

```bash
git rebase origin/feature/example-change
```

Resolva e valide eventuais conflitos conforme
[Resolução de conflitos](conflitos.md). Se a branch for protegida, publique a
mudança por uma branch permitida e pelo fluxo de revisão definido no
repositório. Para exigência de assinatura, consulte
[Commits assinados](commits-assinados.md).

Não use `--force` para contornar rejeições. Quando uma atualização forçada for
realmente prevista pelo fluxo, prefira `--force-with-lease`, depois de revisar o
histórico remoto. Qualquer push continua exigindo autorização explícita.

## Validação

```bash
git status --short --branch
git log --oneline --decorate -5
```

Confirme a árvore limpa e os commits esperados antes de tentar publicar.

## Referência

- [Documentação oficial de `git push`](https://git-scm.com/docs/git-push)
