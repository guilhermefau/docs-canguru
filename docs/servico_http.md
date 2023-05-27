# HTTP Server

o Apache comumente conhecido como Apache, é um servidor web de código aberto amplamente utilizado em todo o mundo. Ele oferece um ambiente seguro e confiável para hospedar sites e aplicativos da web. Nesta documentação, forneceremos instruções passo a passo sobre como instalar e configurar o Apache em um sistema Linux.

##**Passo 1: Instalação do Apache**

Atualize os repositórios do sistema:



    $ sudo apt update

Instale o Apache:

    $ sudo apt install apache2

Após a conclusão da instalação, o Apache estará em execução no seu sistema.

Para verificar se o Apache está em execução, você pode acessar o endereço IP do servidor no seu navegador. Se a página padrão do Apache for exibida, isso significa que a instalação foi bem-sucedida.

##**Passo 2: Configuração do Apache**

####**Arquivos de Configuração**

O arquivo principal de configuração do Apache é o "apache2.conf", localizado em "/etc/apache2/apache2.conf". Você pode editar esse arquivo para fazer configurações gerais do servidor.

As configurações específicas de cada site são definidas nos arquivos de configuração localizados em "/etc/apache2/sites-available". Cada site possui um arquivo de configuração separado.

####**Diretório de DocumentRoot**

O diretório de DocumentRoot é o local onde os arquivos do seu site serão armazenados. O diretório padrão é "/var/www/html".

Você pode editar o arquivo de configuração do site para alterar o diretório de DocumentRoot:

Abra o arquivo de configuração do site:

    $ sudo nano /etc/apache2/sites-available/seu_site.conf

Localize a diretiva "DocumentRoot" e altere o caminho para o diretório desejado.

Salve o arquivo e saia do editor.

Configurar nome de servidor virtual:

Crie um arquivo de configuração para o nome de servidor virtual:

    $ sudo nano /etc/apache2/sites-available/seu_nome_virtual.conf

Insira a configuração do nome de servidor virtual:


<VirtualHost *:80>
    ServerName seu_nome_virtual
    DocumentRoot /caminho/para/o/diretorio
</VirtualHost>

Ative o nome de servidor virtual:

    $ sudo a2ensite seu_nome_virtual.conf

####**Reinicie o Apache:**

    $ sudo systemctl restart apache2