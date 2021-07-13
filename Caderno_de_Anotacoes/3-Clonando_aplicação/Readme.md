# Clonando aplicação

É hora de colocar o backend no servidor! Eu vou inserir um projeto do github no
servidor. Lembrando q se o projeto tiver em um repo privado, tem antes q logar
no github pelo servidor pra clonar.

> O professor prefere clonar na pasta home do usuário. Pra acessar home direto:
> `cd ~`

> Dica a toa: se quiser listar no terminal, e tb listar pasta vazia, use a flag
> `-la`: `ls -la`.

1- Clone o backend no home (home é o root do usuário). Customize um nome como
segundo parâmetro:
`git clone https://github.com/victortrindade1/rocketseat-backend.git gobarber`

2- Acesse a pasta do app e dê um `npm install`.

3- Configure as variáveis de ambiente `arquivo .env`:
Copie o arquivo .env.example pra já tetificar:
_deploy@deploy-bootcamp:~/gobarber$>>>_ `cp .env.example .env`

Edite .env:
_deploy@deploy-bootcamp:~/gobarber$>>>_ `vim .env`

> É importante ter um APP_SECRET bem complexo no servidor

```diff
-APP_URL=http://localhost:3333
+APP_URL=http://67.205.159.48:3333
-NODE_ENV=development
+NODE_ENV=production

# Auth
-APP_SECRET=
+APP_SECRET=eb8f7b80ca95741e6d69c8905a64fa7e

# Database

DB_HOST=
DB_USER=
DB_PASS=
DB_NAME=

# Mongo

MONGO_URL=

# Redis

REDIS_HOST=127.0.0.1
REDIS_PORT=6379

# Mail

MAIL_HOST=
MAIL_PORT=
MAIL_USER=
MAIL_PASS=

# Sentry

SENTRY_DSN=
```
