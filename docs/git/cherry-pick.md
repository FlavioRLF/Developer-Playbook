# Cherry-pick

`cherry-pick` aplica a alteração introduzida por um commit em outra branch.

## Aplicar um commit

```bash
git switch target-branch
git cherry-pick <commit-id>
```

## Aplicar sem criar o commit imediatamente

```bash
git cherry-pick --no-commit <commit-id>
git diff --staged
```

Isso permite revisar e ajustar a alteração antes do commit.

## Resolver conflitos

```bash
git status
# editar os arquivos
git add path/to/resolved-file
git cherry-pick --continue
```

Para cancelar:

```bash
git cherry-pick --abort
```

Use o recurso para mudanças isoladas. Para sincronizar linhas inteiras de
desenvolvimento, merge ou rebase costuma expressar melhor a intenção.
