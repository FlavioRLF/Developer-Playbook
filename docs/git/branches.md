# Branches

## Criar e trocar de branch

```bash
git switch main
git pull --ff-only
git switch -c feature/example-change
```

`--ff-only` impede que o `pull` crie um merge commit inesperado.

## Listar e inspecionar

```bash
git branch --verbose --verbose
git branch --all
git log --oneline --decorate --graph --all -20
```

## Renomear

```bash
git branch -m feature/old-name feature/new-name
```

Se a branch atual será renomeada:

```bash
git branch -m feature/new-name
```

## Remover branch local

```bash
git branch --delete feature/example-change
```

Use `--delete --force` somente após confirmar que os commits podem ser
descartados:

```bash
git log feature/example-change --not main
```
