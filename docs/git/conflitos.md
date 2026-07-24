# Resolução de conflitos

## Fluxo seguro

1. Identifique a operação em andamento:

   ```bash
   git status
   ```

2. Localize marcadores:

   ```bash
   rg --line-number '^(<<<<<<<|=======|>>>>>>>)'
   ```

3. Edite cada arquivo preservando o comportamento desejado.
4. Execute testes ou validações específicas.
5. Prepare os arquivos e continue:

   ```bash
   git add path/to/resolved-file
   git rebase --continue
   # ou: git merge --continue
   ```

## Escolher uma versão inteira

Durante um merge:

```bash
git checkout --ours path/to/file
git checkout --theirs path/to/file
```

Em um rebase, o significado de `ours` e `theirs` pode parecer invertido porque
a base recebe os commits reaplicados. Confirme sempre com:

```bash
git diff --ours path/to/file
git diff --theirs path/to/file
```

Não resolva conflitos escolhendo um lado inteiro sem entender quais mudanças
serão descartadas.
