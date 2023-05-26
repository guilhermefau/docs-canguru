#**Arquivos de Configuração e Chaves SSH**

##**No servidor SSH:**

/etc/ssh/sshd_config: Este é o arquivo de configuração do servidor SSH. Ele contém várias opções de configuração, como portas, autenticação, permissões de acesso, entre outras. É necessário ter privilégios de superusuário para editar este arquivo.

##**No cliente SSH:**

~/.ssh/config: Este é o arquivo de configuração do cliente SSH, localizado no diretório home do usuário. Ele permite configurar opções específicas para conexões SSH, como aliases de host, identidades de chave, opções de autenticação, entre outras.

##**Arquivos de chave SSH:**

##**id_rsa e id_rsa.pub:**

Esses são os arquivos da chave privada e pública, respectivamente. A chave privada (id_rsa) é mantida no cliente e é usada para autenticar a conexão SSH. A chave pública (id_rsa.pub) é copiada para o servidor SSH e adicionada ao arquivo authorized_keys para permitir a autenticação com a chave correspondente.

##**authorized_keys:**

Este arquivo está localizado no diretório ~/.ssh do usuário no servidor SSH. Ele contém as chaves públicas autorizadas para autenticação com o servidor. Cada chave pública autorizada é adicionada em uma nova linha neste arquivo.

##**known_hosts:**

Este arquivo é criado automaticamente pelo cliente SSH quando se conecta a um novo servidor SSH. Ele armazena as chaves públicas dos servidores aos quais você já se conectou, a fim de verificar a autenticidade desses servidores em conexões futuras.
Esses arquivos e configurações são importantes para a configuração e autenticação segura de conexões SSH. Ao configurar o SSH, é essencial garantir que as permissões corretas sejam aplicadas aos arquivos de chave (por exemplo, id_rsa deve ter permissões restritas somente para o usuário) e que as configurações de segurança apropriadas sejam definidas nos arquivos de configuração (por exemplo, no sshd_config do servidor).