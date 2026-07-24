# Spring

## Executar uma aplicação Spring Boot

```bash
./mvnw spring-boot:run
```

Ou execute o artefato:

```bash
./mvnw clean package
java -jar target/example-service.jar
```

## Perfis

```bash
SPRING_PROFILES_ACTIVE=local ./mvnw spring-boot:run
```

Também é possível usar:

```bash
java -jar target/example-service.jar --spring.profiles.active=local
```

## Propriedades úteis para diagnóstico

```bash
./mvnw spring-boot:run \
  -Dspring-boot.run.arguments="--debug"
```

O relatório de condições ajuda a entender por que uma autoconfiguração foi ou
não aplicada.

## Checklist de configuração

- confirme a ordem das fontes de propriedades;
- valide o perfil realmente ativo;
- diferencie ausência de valor de valor vazio;
- não grave segredos em `application.properties`;
- use testes de contexto somente para configurações que exigem o container
  Spring completo.
