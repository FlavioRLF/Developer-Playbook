# Rebase e squash

Rebase reaplica commits sobre outra base. É útil para atualizar uma branch ou
organizar commits locais antes da integração.

## Atualizar uma branch

```bash
git switch feature/example-change
git fetch origin
git rebase origin/main
```

Durante conflitos:

```bash
git status
# resolver e preparar os arquivos
git add path/to/resolved-file
git rebase --continue
```

Para abandonar a operação:

```bash
git rebase --abort
```

## Combinar commits

```bash
git rebase --interactive HEAD~3
```

No editor, mantenha o primeiro commit como `pick` e troque os seguintes por
`squash` ou `fixup`.

## Cuidados

- Não reescreva commits compartilhados sem coordenação.
- Crie uma referência de segurança quando houver dúvida:

```bash
git branch backup/before-rebase
```

- Se for necessário atualizar uma branch remota reescrita, prefira
  `git push --force-with-lease` a `--force`. O push continua exigindo
  autorização explícita.
