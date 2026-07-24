# Java e Maven

## Tópicos

- [Troubleshooting: erro HTTP 403 ao resolver artefato](maven-erro-403-artefato.md)

## Verificar o ambiente

```bash
java -version
javac -version
mvn -version
```

`mvn -version` mostra qual JDK o Maven está usando. Isso ajuda a diagnosticar
diferenças entre `JAVA_HOME` e o executável `java` disponível no `PATH`.

## Ciclo de build

```bash
mvn clean verify
```

Fases comuns:

- `compile`: compila o código principal;
- `test`: executa testes unitários;
- `package`: gera o artefato;
- `verify`: executa verificações adicionais;
- `install`: publica no repositório Maven local.

## Dependências

```bash
mvn dependency:tree
mvn dependency:tree -Dincludes=group.example:artifact-example
mvn help:effective-pom
```

## Executar um teste específico

```bash
mvn -Dtest=ExampleServiceTest test
mvn -Dtest=ExampleServiceTest#shouldProcess test
```

## Diagnóstico

```bash
mvn --errors --show-version clean verify
mvn --debug validate
```

Evite `--debug` em logs compartilhados: a saída pode conter propriedades do
ambiente. Higienize qualquer trecho antes de documentá-lo.
