# SSH
#**Instalação do SSH**
    
    $ sudo apt update # atualiza o catálogo de pacotes

    $ sudo apt install ssh # instala o pacote do SSH

#**Arquivos de Configuração e Chaves SSH**

##**No servidor SSH:**

/etc/ssh/sshd_config: Este é o arquivo de configuração do servidor SSH. Ele contém várias opções de configuração, como portas, autenticação, permissões de acesso, entre outras. É necessário ter privilégios de superusuário para editar este arquivo.

##**No cliente SSH:**

~/.ssh/config: Este é o arquivo de configuração do cliente SSH, localizado no diretório home do usuário. Ele permite configurar opções específicas para conexões SSH, como aliases de host, identidades de chave, opções de autenticação, entre outras.

#**Arquivo ~/.ssh/config**
    
    Host #NOME DE SUA ESCOLHA
        HostName #ENDEREÇO_IP_HOST
        User #NOME DO USUARIO
        Port #PORTA DO SSH CASO TENHA CONFIGURADO UMA DIFERENTE DA PADRÃO


##**Arquivos de chave SSH:**

####**id_rsa e id_rsa.pub:**

Esses são os arquivos da chave privada e pública, respectivamente. A chave privada (id_rsa) é mantida no cliente e é usada para autenticar a conexão SSH. A chave pública (id_rsa.pub) é copiada para o servidor SSH e adicionada ao arquivo authorized_keys para permitir a autenticação com a chave correspondente.

####**authorized_keys:**

Este arquivo está localizado no diretório ~/.ssh do usuário no servidor SSH. Ele contém as chaves públicas autorizadas para autenticação com o servidor. Cada chave pública autorizada é adicionada em uma nova linha neste arquivo.

####**known_hosts:**

Este arquivo é criado automaticamente pelo cliente SSH quando se conecta a um novo servidor SSH. Ele armazena as chaves públicas dos servidores aos quais você já se conectou, a fim de verificar a autenticidade desses servidores em conexões futuras.
Esses arquivos e configurações são importantes para a configuração e autenticação segura de conexões SSH. Ao configurar o SSH, é essencial garantir que as permissões corretas sejam aplicadas aos arquivos de chave (por exemplo, id_rsa deve ter permissões restritas somente para o usuário) e que as configurações de segurança apropriadas sejam definidas nos arquivos de configuração (por exemplo, no sshd_config do servidor).

#**Gerando chaves SSH**

    $ ssh-keygen -t ed25519

#**Copiando as chaves**
	
    $ sh-copy-id USUARIO@ENDEREÇO_IP

Copiando as chaves para o host você pode acessá-lo sem a necessidade de senhas(apenas na primeira vez será solicitado a senha, pois ele irá se conectar ao host e copiar as chaves públicas do ssh).

#**Copiando um arquivo local para um servidor remoto:**

    $ scp /caminho/do/arquivo.txt usuario@servidor:/caminho/destino/

#**Copiando um arquivo remoto para o seu computador local:**

	$ scp usuario@servidor:/caminho/do/arquivo.txt /caminho/destino/

#**Copiando um diretório local para um servidor remoto (use a opção "-r" para transferir recursivamente):**

    $ scp -r /caminho/do/diretorio usuario@servidor:/caminho/destino/

#**Copiando um diretório remoto para o seu computador local (uso da opção "-r"):**

    $ scp -r usuario@servidor:/caminho/do/diretorio /caminho/destino/

