# Criação dos usuários no samba 
Envie o arquivo alunos.csv para a VM via ssh usando o comando:
    $ scp #VER EM SSH

 
Vamos filtrar o arquivo usando o comando abaixo:

    $ cut -d ‘,’ -f 2 alunos.csv | grep -i sobrenome |tail -n +2 | head -n 50 > sobrenome.txt

Onde tiver “sobrenome” voce substitui pelo sobrenome que procura e ele vai filtrar e redirecionar a saida para um arquivo.txt que vamos usar no script.

Fiz dois arquivos de 50 para cada sobrenome e usei o comando diff pra ver se eles nao se repetiam nos dois arquivos

Crie um arquivo.sh 

    $ nano userscript.sh

Dentro do nano é so colocar o script abaixo:

    #!/bin/sh

    # Arquivo de texto com os nomes completos dos usuários, um por linha (nome sobrenome)
    ARQUIVO_USUARIOS="teixeira.txt"

    # Loop para ler o arquivo de texto e criar os usuários
    while IFS= read -r linha
    do
        # Remove espaços em branco no início e no fim da linha
        linha=$(echo "$linha" | xargs)

        # Transforma o nome completo em letras minúsculas
        nome_completo=$(echo "$linha" | tr '[:upper:]' '[:lower:]')

        # Extrai o nome e sobrenome da linha
        nome=$(echo "$nome_completo" | cut -d' ' -f1)
        sobrenome=$(echo "$nome_completo" | cut -d' ' -f2)

        # Concatena o primeiro caractere do sobrenome ao nome de usuário
        primeiro_caractere_sobrenome=${sobrenome:0:1}
        usuario="$nome.$primeiro_caractere_sobrenome.teixeira"

        # Verifica se o usuário já existe
        contador=1
        while samba-tool user show "$usuario" &>/dev/null; do
            # Caso exista, adiciona outra inicial do sobrenome ao nome de usuário
            usuario="$nome.$primeiro_caractere_sobrenome${sobrenome:$contador:1}.teixeira"
            contador=$((contador + 1))
        done

        # Cria o usuário no Samba4 AD DC com senha Ifrn.2023
        samba-tool user create "$usuario" Ifrn.2023
        # Exibe os detalhes do usuário criado
        echo "Usuário criado: $usuario"
    done < "$ARQUIVO_USUARIOS"

Salve o arquivo.


comando para dar permissão de execução ao script:

    $ chmod +x nomedoscript.sh

depois so executar usando o comando:

    $ ./nomedoscript.sh

#Adicionando usuarios aos grupos

    for user in $(samba-tool user list | grep sobrenome); do
    samba-tool group addmembers nomedogrupo $user
    done
