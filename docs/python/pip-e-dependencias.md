# Pip e dependências

## Instalar um pacote

```bash
python -m pip install package-name
```

## Instalar dependências declaradas

```bash
python -m pip install --requirement requirements.txt
```

## Inspecionar

```bash
python -m pip list
python -m pip show package-name
python -m pip check
```

`pip check` detecta incompatibilidades entre dependências instaladas.

## Gerar uma fotografia do ambiente

```bash
python -m pip freeze > requirements.lock.txt
```

`freeze` registra todo o ambiente, inclusive dependências transitivas. Para
projetos mantidos, prefira separar dependências diretas de um arquivo de lock
gerado por uma ferramenta adequada ao projeto.

## Diagnóstico de instalação

```bash
python -m pip install --verbose package-name
python -m pip cache info
```

Nunca grave tokens de índices privados no repositório. Use configuração local,
variáveis de ambiente ou o gerenciador de segredos do ambiente.
