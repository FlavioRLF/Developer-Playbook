# Ambientes virtuais

## Criar

```bash
python -m venv .venv
```

## Ativar

Linux, macOS ou WSL:

```bash
source .venv/bin/activate
```

PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Prompt de comando do Windows:

```bat
.\.venv\Scripts\activate.bat
```

## Validar

```bash
python -c "import sys; print(sys.executable)"
python -m pip --version
```

O executável e o diretório de instalação devem apontar para `.venv`.

## Desativar

```bash
deactivate
```

O ambiente é descartável: não versione `.venv`; versione apenas a declaração de
dependências.
