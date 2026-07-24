# Docker

## Imagens e containers

```bash
docker image ls
docker container ls --all
docker build --tag example-service:local .
docker run --rm --publish 8080:8080 example-service:local
```

## Inspeção

```bash
docker logs --follow example-container
docker inspect example-container
docker stats --no-stream
docker exec -it example-container sh
```

## Diagnóstico de build

```bash
docker build --no-cache --progress=plain --tag example-service:debug .
docker history example-service:debug
```

## Boas práticas

- use imagens-base mínimas, específicas e mantidas;
- execute como usuário não privilegiado;
- copie primeiro arquivos de dependências para aproveitar cache;
- use `.dockerignore`;
- nunca inclua segredos em `ARG`, `ENV`, camadas ou arquivos copiados;
- adicione `HEALTHCHECK` somente quando houver um sinal confiável de saúde;
- fixe versões de produção conforme a política do projeto.

Comandos de limpeza como `docker system prune` removem recursos e devem ser
executados somente após inspeção explícita.
