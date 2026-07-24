# Quarkus

## Modo de desenvolvimento

Com Maven Wrapper:

```bash
./mvnw quarkus:dev
```

Com Maven instalado:

```bash
mvn quarkus:dev
```

## Perfis e configuração

Arquivos comuns:

```text
src/main/resources/application.properties
src/main/resources/application-dev.properties
src/main/resources/application-test.properties
```

Ative um perfil:

```bash
./mvnw quarkus:dev -Dquarkus.profile=dev
```

Variáveis de ambiente sobrescrevem propriedades seguindo a conversão de pontos
e hífens para sublinhados, por exemplo:

```bash
QUARKUS_HTTP_PORT=8081 ./mvnw quarkus:dev
```

## Build

```bash
./mvnw clean verify
./mvnw package
java -jar target/quarkus-app/quarkus-run.jar
```

## Diagnóstico inicial

- confirme o perfil ativo;
- compare configuração efetiva e variáveis de ambiente;
- verifique conflitos de porta;
- confira extensões com `./mvnw quarkus:list-extensions`;
- execute testes antes de alterar configuração de produção.
