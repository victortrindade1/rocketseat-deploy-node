# Utilizando PM2

A lib PM2 faz com q o app continue rodando mesmo se o ssh for fechado ou o server
reiniciar.

Instale PM2 de forma global no server:

deploy@deploy-bootcamp:~$ `sudo npm install -g pm2`

Dê um start no pm2:

deploy@deploy-bootcamp:~/gobarber$ `pm2 start dist/server.js`

Para listar todos os serviços pm2 da máquina: `pm2 list`

Configure pro PM2 reiniciar automático o app caso o server reinicie:

deploy@deploy-bootcamp:~/gobarber$ `pm2 startup systemd`

Vai aparecer um comando necessário pra variável de ambiente $PATH. O comando q
aparece é este:

`sudo env PATH=$PATH:/usr/bin /usr/local/lib/node_modules/pm2/bin/pm2 startup systemd -u deploy --hp /home/deploy`

Basta executá-lo.

Agora toda vez q eu executar um comando de configuração do pm2, tem q dar um
`pm2 save`.

O log de monitoramento do pm2 é bem legal: `pm2 monit`
