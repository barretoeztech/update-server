# Servidor privado de atualização EZTECH para o MUS

Primeiro clone o projeto em um diretorio qualquer. E siga os proximos passos.

O servidor foi contruido para examinar a pasta **./Packages** periódicamente com intervalos de 1 minuto e contruir novamente os arquivos de controle **Packages.gz** e **Packages.stamps** dentro da pasta **./Packges** e portanto nao é necessario parar ou reiniciar o servidor para publicar um novo pacote, basta executar novamente **buid-package** conforme abaixo.

*Obs: Para execução do servidor é necessario a pre instalação do Docker, Docker-compose*

## Construção do pacote de instalação para o MUS

Para entender a contrução do pacote precisamos primeiro explicar a estrutura do diretorio **ipk-build**. Dentro dessa estrutura temos o seguinte: 

```
ipk-build/
├── CONTROL
│   ├── control
│   ├── postinst
│   ├── postrm
│   ├── preinst
│   └── prerm
└── usr
    └── bin
        └── teste
```

O arquivo **control** deve ser editado antes de construir o pacote, contem informações para o utilitario de intalação OPKG que sera utilizado para atualizar o MUS, abaixo segue um exemplo.

~~~
Package: musgilbarco
Version: 1.23
Architecture: mipsel_24kc
Maintainer: Kelvin Ussher <krusher@eztech.ind.br>
Description: This is MUS Package for Gilgarco
Priority: optional
Depends: curl
~~~

O campo **Depends** informa ao instalador que esse pacote tem a lista de dependencias separadas por espaços

Os arquivos **preinst, postinst, prerm e postrm** são scripts que respectivamente serão executados na pre instalação, na pos instalação, na pre remoção e pos remoção, respectivamente.

O diretorio **usr/bin** trata-se apenas de um exemplo e deve ser criada a estrutura com os arquivos executaveis, scripts, texto ou todo o tipo com suas respectivas permissões, ja definidas.

Para contruir um novo pacote devemos executar o comando abaixo:

~~~
$ build-package
~~~

O pacote sera contruido gerando um arquivo com a terminação *.ipk* e copiado na pasta **./Packages** e sua publicação sera automatica.


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

