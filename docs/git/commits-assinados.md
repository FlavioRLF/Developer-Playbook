# Commits assinados

Assinaturas permitem verificar a autoria criptográfica de commits e tags. Git
suporta, entre outras opções, OpenPGP e SSH.

## Assinatura com chave SSH

Configure uma chave pública dedicada ou existente:

```bash
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519.pub
git config --global commit.gpgsign true
```

Crie um commit assinado:

```bash
git commit -S -m "docs: add technical note"
```

Verifique localmente:

```bash
git log --show-signature -1
```

## Assinatura com OpenPGP

```bash
gpg --list-secret-keys --keyid-format=long
git config --global user.signingkey <key-id>
git config --global commit.gpgsign true
git commit -S -m "docs: add technical note"
```

Nunca versione chaves privadas. A plataforma remota pode exigir o cadastro da
chave pública para exibir a assinatura como verificada.
