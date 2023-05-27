#**Visualização de Logs**
O comando **journalctl -f | ccze** é usado para exibir o log em tempo real do sistema, formatando-o com cores usando o programa ccze. Isso pode ajudar a tornar a leitura do log mais fácil e distinguir diferentes tipos de mensagens.

Os seguintes comandos podem ser usados para visualizar logs específicos com formatação colorida:

##Para visualizar o log do sistema:

**$ tail -f /var/log/syslog | ccze**

##Para visualizar o log de autenticação:

**$ tail -f /var/log/auth.log | ccze**

##Para visualizar o log de acesso do Apache:

**$ tail -f /var/log/apache2/access.log | ccze**

##Para visualizar o log de erros do Apache:

**$ tail -f /var/log/apache2/error.log | ccze**

Esses comandos exibirão as últimas linhas do arquivo de log especificado em tempo real, e a saída será formatada com cores usando o ccze. Isso tornará mais fácil identificar diferentes tipos de mensagens no log.

Lembre-se de que você precisa ter permissões de superusuário (ou usar sudo) para acessar os logs em alguns diretórios, como /var/log/auth.log e /var/log/apache2/.