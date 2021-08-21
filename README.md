# innova-pm2-discord

Módulo do PM2 para mandar eventos e logs do PM2 para o Discord. É um fork do repositório https://github.com/FranciscoG/pm2-discord com algumas melhorias implementadas pela Innova.

## Instalação

Para instalar e configurar, deve ser feito o clone desse repositório na máquina em que se deseja monitorar o pm2, em seguida executar comandos:

```
cd innova-pm2-discord
pm2 install .
pm2 set innova-pm2-discord:discord_url https://discord_url
```

#### `discord_url`
A url do Discord, é necessário configurar um webhook. Mais detalhes aqui: https://support.discordapp.com/hc/en-us/articles/228383668-Intro-to-Webhooks

## Configuração

Os seguintes eventos podem ser ativados/desativados:

- **log** - All standard out logs from your processes. `Default: true`
- **error** - All error logs from your processes. `Default: false`
- **kill** - Event fired when PM2 is killed. `Default: true`
- **exception** - Any exceptions from your processes. `Default: true`
- **restart** - Event fired when a process is restarted. `Default: false`
- **delete** - Event fired when a process is removed from PM2. `Default: false`
- **stop** - Event fired when a process is stopped. `Default: true`
- **restart overlimit** - Event fired when a process is reaches the max amount of times it can restart. `Default: true`
- **exit** - Event fired when a process is exited. `Default: false`
- **start** -  Event fired when a process is started. `Default: false`
- **online** - Event fired when a process is online. `Default: false`

É possível alterar os parâmetros utilizando o comando PM2 set.

```
pm2 set innova-pm2-discord:log true
pm2 set innova-pm2-discord:error false
...
```

## Opções

As seguintes opções estão disponíveis:

- **process_name** (string) When this is set, it will only output the logs of a specific named process `Default: NULL`
- **buffer** (bool) - Enable/Disable buffering of messages by timestamp. Messages that occur with the same timestamp (seconds) will be concatenated together and posted as a single discord message. `Default: true`
- **buffer_seconds** (int) - Duration in seconds to aggregate messages. Has no effect if buffer is set to false.  `Min: 1, Max: 5, Default: 1`
- **queue_max** (int) - Number of messages to keep queued before the queue will be truncated. When the queue exceeds this maximum, a rate limit message will be posted to discord. `Min: 10, Max: 100, Default: 100`

Essas opções são configuradas utilizando o comando PM2 set.

Exemplo: A seguinte configuração irá habilitar o buffering de mensagens, e setar o buffer para 2 segundos.  Todas as mensagens que ocorrerem dentro de 2 segundos entre uma e outra (no mesmo tipo de evento) serão concatenadas em uma mesma mensagem no discord.

```
pm2 set innova-pm2-discord:process_name myprocess
pm2 set innova-pm2-discord:buffer true
pm2 set innova-pm2-discord:buffer_seconds 2
pm2 set innova-pm2-discord:queue_max 50
```
