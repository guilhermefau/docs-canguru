# Configurar Interfaces de Rede
#**Configuração das Interfaces de Rede com Netplan no Ubuntu Server**

O Netplan é o utilitário de configuração de rede padrão no Ubuntu a partir da versão 17.10. Ele substitui o arquivo de configuração de rede legado "/etc/network/interfaces" e permite configurar a rede de forma mais eficiente e flexível. O Netplan utiliza a sintaxe YAML para definir a configuração de rede.

##Passo 1: Criar/Editar o arquivo de configuração

Acesse o arquivo de configuração YAML no diretório "/etc/netplan".

    $ sudo vi /etc/netplan/50-cloud-init.yaml

Dentro do arquivo, você encontrará o seguinte conteúdo:

    network:
      version: 2
      ethernets:
        eth0:
          dhcp4: true

Pressione a tecla i para iniciar a edição do arquivo.

Atualize o arquivo de configuração com as seguintes informações, verificando sempre a identação correta:

    network:
      version: 2
      renderer: networkd
      ethernets:
        eth0: # interface de rede
          addresses:
            - 192.168.0.210/24 # seu endereço de IP estático/máscara
          nameservers:
            addresses: [8.8.8.8, 8.8.4.4] # DNS
          routes:
            - to: default
              via: 192.168.0.254 # Gateway

Aperte a tecla Esc e digite :wq! para salvar e sair do editor.

##Passo 2: Aplique as novas configurações de rede

Use o seguinte comando para aplicar as novas configurações de rede:

    $ sudo netplan apply

Se tudo estiver correto, o comando será executado sem retornar nada. Caso ocorra algum erro, o Netplan exibirá uma mensagem de erro indicando o problema.

##Passo 3: Verifique se o endereço IP foi atribuído corretamente usando o comando:

    $ ip -br -c a

##Passo 4: Teste a conexão com a Internet

Teste a conexão com a Internet usando o comando ping, por exemplo:


    $ ping google.com

Certifique-se de que a conexão com a Internet esteja funcionando corretamente.

#**Configuração das Interfaces de Rede no Debian**

A configuração das interfaces de rede no Debian é feita por meio do arquivo de configuração 
 /etc/network/interfaces. Neste arquivo, você pode definir as configurações de rede para cada interface de rede do sistema.

##Passo 1: Acessar o arquivo de configuração

Abra um terminal e acesse o arquivo de configuração /etc/network/interfaces usando um editor de texto, como o nano:


    $ sudo nano /etc/network/interfaces

##Passo 2: Configurar as interfaces de rede

Dentro do arquivo /etc/network/interfaces, você pode definir as configurações para cada interface de rede separadamente. Aqui está um exemplo de como configurar uma interface de rede usando DHCP:

    auto eth0
    iface eth0 inet dhcp

Nesse exemplo, a interface de rede eth0 está configurada para obter um endereço IP automaticamente por meio do DHCP.

Se você deseja configurar um endereço IP estático para a interface de rede, pode usar o seguinte exemplo:


    auto eth0
    iface eth0 inet static
        address 192.168.0.100
        netmask 255.255.255.0
        gateway 192.168.0.1

Nesse exemplo, a interface de rede eth0 está configurada com um endereço IP estático 192.168.0.100, uma máscara de rede 255.255.255.0 e um gateway padrão 192.168.0.1.

Você também pode adicionar configurações adicionais, como servidores DNS:


    auto eth0
    iface eth0 inet static
        address 192.168.0.100
        netmask 255.255.255.0
        gateway 192.168.0.1
        dns-nameservers 8.8.8.8 8.8.4.4

Nesse exemplo, os servidores DNS do Google 8.8.8.8 e 8.8.4.4 são configurados para a interface de rede eth0.

##Passo 3: Salvar e fechar o arquivo

Depois de fazer as alterações necessárias no arquivo /etc/network/interfaces, salve o arquivo e feche o editor de texto.

##Passo 4: Reiniciar o serviço de rede

Para que as alterações tenham efeito, você precisa reiniciar o serviço de rede. Use o seguinte comando para reiniciar o serviço networking:


    $ systemctl restart networking