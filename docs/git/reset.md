# Reset

`git reset` move uma referência e, dependendo do modo, altera o índice e a
árvore de trabalho.

| Modo | Move `HEAD` | Altera o índice | Altera arquivos |
| --- | --- | --- | --- |
| `--soft` | Sim | Não | Não |
| `--mixed` | Sim | Sim | Não |
| `--hard` | Sim | Sim | Sim |

## Desfazer o último commit e manter tudo preparado

```bash
git reset --soft HEAD~1
```

## Retirar arquivos da área de stage

```bash
git reset
```

Alternativa mais explícita:

```bash
git restore --staged path/to/file
```

## Descartar commit e alterações

```bash
git reset --hard HEAD~1
```

> **Atenção:** `--hard` descarta alterações rastreadas. Inspecione
> `git status`, `git diff` e `git reflog` antes de usá-lo.

## Recuperar referência anterior

```bash
git reflog
git branch recovery/example <commit-id>
```

Crie primeiro uma branch de recuperação em vez de executar outro reset.
