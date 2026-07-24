# Guia de contribuição

Este é um playbook pessoal, mas as regras abaixo mantêm a documentação
consistente e segura.

## Critérios para uma nota

Uma contribuição deve:

- tratar exclusivamente de engenharia de software;
- resolver uma dúvida ou situação técnica identificável;
- conter contexto suficiente para ser entendida no futuro;
- usar somente dados, hosts e nomes fictícios;
- indicar riscos de comandos destrutivos;
- incluir uma forma de validar o resultado, quando aplicável.

## Checklist de privacidade

Antes de salvar ou versionar uma alteração, procure por:

- credenciais, tokens, cookies, chaves e certificados;
- nomes de clientes, pessoas, equipes ou projetos internos;
- endereços de e-mail, números de chamados e identificadores reais;
- URLs, IPs, nomes de hosts, namespaces ou repositórios privados;
- trechos de logs com dados pessoais ou informações operacionais sensíveis.

Substitua qualquer referência contextual por valores como:

```text
example-service
example-namespace
registry.example.com
user@example.com
192.0.2.10
```

O bloco `192.0.2.0/24` é reservado para documentação.

## Validação antes do commit

```bash
git status --short
git diff --check
git diff
```

O diff completo deve ser apresentado e revisado antes de qualquer commit.
Pushes exigem autorização explícita.
