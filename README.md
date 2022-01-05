# Servidor privado de atualização EZTECH para o MUS



O servidor foi contruido para examinar a pasta **./Packages** periódicamente com intervalos de 1 minuto e contruir novamente os arquivos de controle **Packages.gz** e **Packages.stamps**, baseado em seu conteudo. Todo arquivo de Pacote deve ser copiado para a pasta ./**Packages**

## Contrução do pacote de instalação para o MUS

A pasta **./ipk-build** contem uma estrutura de exemplo:

Para contruir um novo pacote devemos executar o comando abaixo:

~~~
$ build-package
~~~

O pacote sera contruido gerando um arquivo com a terminação *.ipk* e copiado na pasta **./Packages**



## Construção do container e execução


Para construir o container do servidor de atualização
execute o comando abaixo no diretorio **update-server**:
~~~ 
$ docker-compose build
~~~

Para iniciar o container execute o comando abaixo no mesmo diretorio:

~~~
$ docker-compose up -d
~~~

Para parar a execução do container execute o comando abaixo no mesmo diretorio:

~~~
$ docker-compose down
~~~

