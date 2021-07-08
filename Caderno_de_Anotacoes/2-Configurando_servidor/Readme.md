# Configurando servidor

Acesse o terminal do servidor. P/ acessar o terminal do servidor:
`ssh root@<ip_servidor>`. Ex: `ssh root@172.28.164.14`

Atualize o servidor: `apt update && apt upgrade`

## Usuário admin

Com um usuário admin, vc vai poder fazer deploy via SSH de outras máquinas, sem
precisar trocar o usuário. O q faremos aqui é copiar a chave pública autorizada
do root do servidor e colar na pasta do usuário criado.

Crie um usuário admin: `adduser deploy`

> "deploy" é o nome do usuário. Vc poderia fazer deploy pelo root, mas aí qnd
> precisarem fazer conexão com o servidor via SSH, ia ter q trocar de usuário

Dê a esse usuário poderes admin: `usermod -aG sudo deploy`

Crie a pasta .ssh na pasta do usuário criado:

```
cd /home/deploy/
mkdir .ssh
cd .ssh/
```

Copie `authorized_keys` de .ssh do root pro .ssh do usuário:
`cp ~/.ssh/authorized_keys /home/deploy/.ssh`

> Se o terminal já estiver na pasta .ssh do usuário, basta digitar "ponto" q vai direto.

> Ex: root@deploy-bootcamp:/home/deploy/.ssh# `cp ~/.ssh/authorized_keys .`

Agora, o dono de `authorized_keys` copiada precisa ser trocado de root pro novo
usuário deploy:

root@deploy-bootcamp:/home/deploy/.ssh# `chown deploy:deploy authorized_keys`

Dê um `exit` e re-conecte com o novo usuário deploy. Em vez de
`ssh root@<ip_servidor>`, agora acesse com `ssh deploy@<ip_servidor>`. Logado
como usuário, lembre-se q agora precisará colocar `sudo` na frente do q quiser q
tenha poder admin ;)

## Ferramentas para instalar

Git:
Veja se já tem git. Se não tiver, instale. `git --version`

Node:
`sudo apt install nodejs`

NPM:

Não faz muita diferença usar npm ou yarn pra produção.

`sudo apt install npm`

Para verificar: `node -v` e `npm -v`.
