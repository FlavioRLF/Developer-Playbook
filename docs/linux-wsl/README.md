# Linux e WSL

## Tópicos

- [Busca de padrões em logs com `grep`](busca-em-logs-com-grep.md)

## Sistema e recursos

```bash
uname -a
cat /etc/os-release
df -h
du -sh path/to/directory
free -h
ps aux
```

## Portas e processos

```bash
ss -lntp
lsof -i :8080
ps -fp <pid>
```

## Arquivos e texto

```bash
find path/to/search -type f -name '*.log'
rg --line-number 'error|exception' path/to/logs
tail -n 200 --follow path/to/application.log
```

## Permissões

```bash
id
namei -l path/to/file
stat path/to/file
chmod u+x path/to/script
```

Evite `chmod 777`; corrija proprietário, grupo e permissões mínimas necessárias.

## WSL

No PowerShell:

```powershell
wsl --status
wsl --list --verbose
wsl --shutdown
```

Para melhor desempenho, mantenha projetos Linux no filesystem da distribuição
WSL, e não em um diretório montado do Windows, quando a ferramenta fizer muitas
operações de I/O.
