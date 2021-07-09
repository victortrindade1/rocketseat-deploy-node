# Criando serviços

Antes de configurar o banco de dados, vou configurar o server pra usar o docker sem precisar do `sudo`, pois o 
usuário `deploy` é admin. Na documentação do docker: https://docs.docker.com/engine/install/linux-postinstall/

No server:
`sudo groupadd docker`

`sudo usermod -aG docker $USER` (não é pra trocar o USER, é pra deixar assim)

Feche o terminal do server `exit` e reabra `ssh deploy@67.205.159.48`.

Pra testar, use o docker sem sudo: `docker ps`.

## Container docker postgres

Crie o container do postgres:

`docker run --name postgres -e POSTGRES_PASSWORD=bootcampdeploy -p 5432:5432 -d -t postgres`

## Container docker MongoDB

Crie o container do Mongo:

`docker run --name mongo -p 27017:27017 -d -t mongo`

## Container docker Redis

Crie o container do Redis:

`docker run --name redis -p 6379:6379 -d -t redis:alpine`

Para verificar: `docker ps -a`

## Edite o .env do server

deploy@deploy-bootcamp:~/gobarber$ `vim .env`

> O Mongo cria sozinho o seu banco qnd a gnt configura a MONGO_URL

```diff
APP_URL=http://67.205.159.48:3333
NODE_ENV=production

# Auth
APP_SECRET=eb8f7b80ca95741e6d69c8905a64fa7e

# Database

-DB_HOST=
-DB_USER=
-DB_PASS=
-DB_NAME=
+DB_HOST=localhost
+DB_USER=postgres
+DB_PASS=bootcampdeploy
+DB_NAME=bootcampnodejs

# Mongo

-MONGO_URL=
+MONGO_URL=mongodb://localhost:27017/bootcampnodejs

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

Pra salvar no vim: Esc + `:wq`

## Crie o banco no postgres

Para criar o banco no server, vou fazer via CLI. Pra isso, preciso acessar o `psql`, q é a CLI do postgres.

Pra acessar o `psql` do server:

1. Acesse o `bash` do postgres. No server: 
deploy@deploy-bootcamp:~/gobarber$  `docker exec -i -t postgres /bin/sh`

2. No bash do postgres, troque para o usuário postgres:
$ `su postgres`

3. Acesse o psql:
postgres=# `psql`

4. Crie o banco:
postgres=# `CREATE DATABASE bootcampnodejs;`

5. Saia:
postgres=# `\q` > exit > exit
