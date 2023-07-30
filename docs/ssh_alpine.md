Para instalar um servidor SSH (OpenSSH) no Alpine Linux, você pode seguir os seguintes passos:

Abra um terminal ou acesse o console do seu sistema Alpine Linux.

Atualize o índice de pacotes para garantir que você esteja usando a lista mais atualizada dos pacotes disponíveis. Para isso, execute o seguinte comando como usuário root ou usando o sudo:

sql
Copy code
sudo apk update
Em seguida, instale o pacote OpenSSH-server usando o comando apk:
csharp
Copy code
sudo apk add openssh-server
O servidor SSH agora está instalado em seu sistema. Por padrão, o serviço SSH é habilitado automaticamente após a instalação. Para garantir que ele seja iniciado automaticamente ao iniciar o sistema, execute o seguinte comando:
sql
Copy code
sudo rc-update add sshd
Agora, inicie o servidor SSH imediatamente com o seguinte comando:
sql
Copy code
sudo service sshd start