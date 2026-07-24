# Busca de padrões em logs com `grep`

## Objetivo

Localizar mensagens relevantes em arquivos de log sem modificar o conteúdo.

## Busca recursiva com múltiplos padrões

```bash
grep \
  --recursive \
  --line-number \
  --binary-files=without-match \
  --extended-regexp \
  --include='*.log' \
  --color=never \
  -- 'Exception|ERROR|timeout' path/to/logs
```

`--extended-regexp` é necessário para que `|` represente alternância. O `--`
encerra as opções e evita interpretar como argumento um padrão iniciado por
hífen.

Forma curta equivalente em implementações compatíveis:

```bash
grep -RInE --include='*.log' \
  -- 'Exception|ERROR|timeout' path/to/logs
```

## Contexto e quantidade

```bash
grep -RInE -C 2 --include='*.log' -- 'ERROR' path/to/logs
grep -RIl --include='*.log' -- 'timeout' path/to/logs
grep -RIEc --include='*.log' -- 'Exception' path/to/logs
```

- `-C 2` inclui duas linhas antes e depois;
- `-l` mostra apenas os arquivos correspondentes;
- `-c` conta linhas correspondentes por arquivo.

## Validação e códigos de saída

```bash
grep -RIn --include='*.log' -- 'ERROR' path/to/logs
printf '%s\n' "$?"
```

- `0`: houve correspondência;
- `1`: nenhuma correspondência;
- valor maior que `1`: ocorreu erro.

Não compartilhe resultados sem remover tokens, dados pessoais, URLs privadas e
outros valores sensíveis. Para uma experiência mais simples no uso interativo,
consulte também o exemplo com `rg` no [índice de Linux e WSL](README.md).

## Referência

- [Manual oficial do GNU grep](https://www.gnu.org/software/grep/manual/grep.html)
