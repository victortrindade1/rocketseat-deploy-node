# Rodando o servidor

## package.json

Altere o package.json do backend de desenvolvimento.

```diff
{
  "name": "gobarber-backend",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "dev": "nodemon src/server.js",
    "dev:debug": "nodemon --inspect src/server.js",
    "queue": "nodemon src/queue.js",
    "postgres": "docker start database",
    "mongodb": "docker start mongodatabase",
    "redis": "docker start redisbarber",
    "dev-start": "docker start redisbarber && docker start mongodatabase && docker start database && nodemon src/queue.js && nodemon src/server.js",
+    "build": "sucrase ./src -d ./dist --transforms imports",
+    "start": "node dist/server.js"
  },
  "dependencies": {
    "@sentry/node": "5.10.0",
    "bcryptjs": "^2.4.3",
    "bee-queue": "^1.2.2",
    "cors": "^2.8.5",
    "date-fns": "^2.0.0-beta.5",
    "dotenv": "^8.2.0",
    "express": "^4.17.1",
    "express-async-errors": "^3.1.1",
    "express-handlebars": "^3.1.0",
    "jsonwebtoken": "^8.5.1",
    "mongoose": "^5.7.11",
    "multer": "^1.4.2",
    "nodemailer": "^6.3.1",
    "nodemailer-express-handlebars": "^3.1.0",
    "pg": "^7.12.1",
    "pg-hstore": "^2.3.3",
    "sequelize": "^5.21.1",
    "youch": "^2.0.10",
    "yup": "^0.27.0"
  },
  "devDependencies": {
    "eslint": "^6.5.1",
    "eslint-config-airbnb-base": "^14.0.0",
    "eslint-config-prettier": "^6.4.0",
    "eslint-plugin-import": "^2.18.2",
    "eslint-plugin-prettier": "^3.1.1",
    "nodemon": "^1.19.4",
    "prettier": "^1.18.2",
    "sequelize-cli": "^5.5.1",
    "sucrase": "^3.10.1"
  }
}
```

O sucrase nesse caso está transformando apenas o import/export, mas ele tb
transforma jsx e typescript em js puro.

Dê um `yarn build` e depois um `yarn start`. Ainda não foi configurado nada do
Redis, então vai dar erro.

## .gitignore

Coloque a pasta dist no .gitignore. Esta pasta não vai pra produção.

```diff
node_modules
+dist
.env
```

## Suba o código e dê um build

Atualize o código do github: `git add . + commit + push`.

Pra atualizar o código do server, não precisa mais clonar, basta dar um
`git pull`.

deploy@deploy-bootcamp:~/gobarber$ `git pull`.

Como o server não tem o yarn, use o NPM pra dar o build:

deploy@deploy-bootcamp:~/gobarber$ `npm run build`.

Starta essa bagaça agora: deploy@deploy-bootcamp:~/gobarber$ `npm run start`.

## Testar server

Por enquanto algumas coisas estão sendo feitas na unha: usar IP com porta, rodar
migration na mão, npm install na mão... mas não desespere, mais a frente será
isso tudo automatizado.

### Liberar porta

Por enquanto temos o IP com a porta 3333, q logo sairão e darão lugar a uma URL.
Mas, por enquanto, vamos deixar a porta 3333 e permitir esta porta no Ubuntu do
server:

deploy@deploy-bootcamp:~/gobarber$ `sudo ufw allow 3333`

### Migrations

Como não tem o yarn, eu vou fazer o `db:migrate` pelo `npx`:

deploy@deploy-bootcamp:~/gobarber$ `npx sequelize db:migrate`

### Insomnia

Deixe o servidor rodando: deploy@deploy-bootcamp:~/gobarber$ `npm run start`

Teste pelo Insomnia. Para isso, é muito fácil! Basta mudar no Insomnia a
`base_url` para o IP do server.

No Manage Environments do Insomnia:

```diff
{
  ...
-  "base_url": "http://localhost:3333",
+  "base_url": "http://67.205.159.48:3333",
  ...
}
```

Agora, para testar, crie um usuário e tente logar pelo Insomnia.
