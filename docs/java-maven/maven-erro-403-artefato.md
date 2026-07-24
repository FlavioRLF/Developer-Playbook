# Troubleshooting: erro HTTP 403 ao resolver artefato Maven

## Sintomas

- o build falha durante a resolução de dependências ou plugins;
- a mensagem contém `Could not transfer artifact` e status HTTP `403`;
- o repositório respondeu, mas recusou a operação.

## Hipóteses

1. credencial ausente, expirada ou sem permissão;
2. o `id` do repositório não corresponde ao `<server>` do `settings.xml`;
3. mirror, profile ou proxy direciona a requisição ao repositório errado;
4. o repositório aplica política que bloqueia aquele caminho ou formato.

Versão inexistente normalmente produz `404` ou mensagem de artefato não
encontrado; não trate automaticamente todo `403` como versão ausente.

## Diagnóstico

```bash
mvn --show-version --errors dependency:resolve
mvn dependency:list-repositories
mvn help:effective-settings
mvn help:effective-pom -Dverbose
```

Confirme:

- coordenadas `groupId:artifactId:version`;
- repositório e mirror efetivamente selecionados;
- correspondência entre o `id` do repositório e o `<server>`;
- profile ativo e proxy configurado;
- validade e permissão da credencial fora do repositório Git.

Use `--debug` somente como último recurso. A saída pode revelar propriedades,
URLs e detalhes de autenticação; nunca a compartilhe sem higienização.

## Solução

Corrija a configuração local ou do ambiente de CI, sem colocar credenciais no
`pom.xml`:

```bash
mvn --update-snapshots clean verify
```

Não apague todo o repositório local como primeira tentativa: um `403` vem do
servidor e normalmente não é corrigido removendo `~/.m2/repository`.

## Validação

- o Maven resolve a dependência sem resposta `403`;
- o build ultrapassa a etapa de resolução;
- a mesma configuração funciona no ambiente que apresentou o erro;
- nenhum segredo foi adicionado ao repositório ou aos logs compartilhados.

## Referências

- [Configuração oficial do Maven](https://maven.apache.org/guides/mini/guide-configuring-maven.html)
- [Repositórios Maven](https://maven.apache.org/guides/introduction/introduction-to-repositories.html)
