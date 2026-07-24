# Git

Referência para operações cotidianas e manutenção segura do histórico.

## Tópicos

- [Branches](branches.md)
- [Reset](reset.md)
- [Rebase e squash](rebase-e-squash.md)
- [Cherry-pick](cherry-pick.md)
- [Commits assinados](commits-assinados.md)
- [Resolução de conflitos](conflitos.md)

## Diagnóstico rápido

```bash
git status --short --branch
git log --oneline --decorate --graph --all -20
git diff
git diff --staged
```

Antes de reescrever histórico, confirme a branch atual, a existência de
alterações locais e se os commits já foram compartilhados.
