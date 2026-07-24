# Developer Playbook

Documentação pessoal, prática e exclusivamente técnica sobre engenharia de
software. O repositório reúne comandos, conceitos, diagnósticos e soluções para
situações recorrentes, sempre com exemplos genéricos e reproduzíveis.

## Objetivos

- Reduzir o tempo gasto procurando comandos e procedimentos conhecidos.
- Registrar o raciocínio por trás de decisões e soluções técnicas.
- Transformar incidentes e dúvidas recorrentes em checklists reutilizáveis.
- Manter exemplos seguros, sem informações confidenciais.

## Conteúdo

| Área | Conteúdo inicial |
| --- | --- |
| [Git](docs/git/README.md) | Branches, reset, rebase, squash, cherry-pick, assinatura e conflitos |
| [Python](docs/python/README.md) | Ambientes virtuais, `pip` e dependências |
| [Java e Maven](docs/java-maven/README.md) | JDK, compilação, dependências e ciclo de build |
| [Quarkus](docs/quarkus/README.md) | Execução, configuração e empacotamento |
| [Spring](docs/spring/README.md) | Perfis, configuração e diagnóstico |
| [Oracle SQL](docs/oracle-sql/README.md) | Consultas, transações e diagnóstico |
| [Docker](docs/docker/README.md) | Imagens, containers e troubleshooting |
| [Kubernetes e OpenShift](docs/kubernetes-openshift/README.md) | Recursos, operação e diagnóstico |
| [Linux e WSL](docs/linux-wsl/README.md) | Comandos de sistema e integração |
| [Mensageria](docs/mensageria/README.md) | Entrega, idempotência e retentativas |
| [Observabilidade](docs/observabilidade/README.md) | Logs, métricas, traces e alertas |
| [Testes](docs/testes/README.md) | Estratégia e automação |
| [IA aplicada à engenharia](docs/ia-engenharia/README.md) | Uso responsável no desenvolvimento |
| [Arquitetura distribuída](docs/arquitetura-distribuida/README.md) | Resiliência, consistência e padrões |

Veja também o [índice completo](docs/README.md) e os
[modelos de documentação](docs/modelos/README.md).

## Princípios editoriais

1. **Somente engenharia de software:** cada nota deve ajudar a construir,
   operar, testar ou compreender sistemas.
2. **Segurança por padrão:** não registrar credenciais, tokens, chaves, nomes
   de clientes, projetos internos, URLs privadas ou dados reais.
3. **Exemplos genéricos:** usar nomes como `example-service`, `example.com`,
   `sample_user` e identificadores fictícios.
4. **Comandos explicados:** informar propósito, impacto, pré-condições e como
   validar o resultado.
5. **Ações destrutivas destacadas:** sinalizar comandos que reescrevem
   histórico, removem dados ou alteram ambientes.
6. **Conteúdo verificável:** preferir exemplos mínimos e indicar versões quando
   o comportamento depender delas.

## Convenções

- Idioma principal: português.
- Formato: Markdown compatível com GitHub.
- Um tema por arquivo; o `README.md` de cada área funciona como índice.
- Nomes de arquivos em `kebab-case`.
- Comandos usam valores fictícios e variáveis descritivas.
- Notas novas devem seguir um dos [modelos](docs/modelos/README.md).

## Fluxo de atualização

```bash
git switch -c docs/topico-tecnico
# editar e validar os arquivos
git diff --check
git diff
```

Antes de criar um commit, revise o diff completo e confirme que não há
informações confidenciais. Nenhum conteúdo deve ser enviado a um repositório
remoto sem autorização explícita.
