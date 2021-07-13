# Dicas de SSH

## Dica 1 - matar node do server

Se vc precisa stopar o node do server:

Descubra os processos q rodam na porta 3333 q vc tá usando:

deploy@deploy-bootcamp:~/gobarber$ `lsof -i :3333`

Se listar o node, pegue o PID e dê um kill:

deploy@deploy-bootcamp:~/gobarber$ `kill -9 <PID>`

## Dica 2 - Manter o SSH conectado sem cair

Por padrão, o SSH desconecta a cada 30s. Vc pode extender para no máximo 99999s.

Edite o `sshd_config` do server. Está no path `/etc/ssh/sshd_config`

deploy@deploy-bootcamp:/etc/ssh$ `sudo nano sshd_config`

### sshd_config

Procure pelas linhas abaixo, descomente e altere:

```diff
-#TCPKeepAlive
+TCPKeepAlive yes
-#ClientAliveInterval
+ClientAliveInterval 30
-#ClientAliveCountMax
+ClientAliveCountMax 99999
```

Restarta o sshd: `sudo service sshd restart`
