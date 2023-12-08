# Docker + PHP + Nginx + Adianti

### Comandos para criar e utilizar um container Docker:

### Estando no diretório onde se encontra o Dockerfile, usar esse comando para criar a imagem:

docker build -t dockerlocal .

esse dockerlocal será o nome dado a imagem

### Caso seja alterado algo do arquivo de texto Dockerfile é necessário usar o comando novamente para atualizar a imagem:

docker build -t dockerlocal .

### Para ver se a imagem foi criada:

docker images

### Para inicializar o container a partir da imagem:

docker run -d --network=host -p 8080:8080 -v /var/www/html/template/:/var/www/html/template dockerlocal

Sendo o comando network=host para puxar o banco de dados da máquina local, o -p 880:880 sendo a porta que o nginx vai utilizar, o -v é o volume que foi criado especificando o diretório da máquina local que vai ser incluída no diretório do container e esse dockerlocal é o nome da imagem que foi criada a partir do arquivo Dockerfile

### Para ver se o container existe:

docker ps -a

### Para ver se o container foi inicializado:

docker ps

### Para ver as logs do container:

docker logs 637d5c0aace8

esses números representa o id do container

### Caso precise dar permissão para algum arquivo ou diretório de dentro do docker:

docker exec -it eeebbe2f3aa5 chmod 777 -R /var/www/html/teste.php

nessa parte onde tem vários números é o id do container

### Para reiniciar o servidor nginx e php do container:

docker exec -it eeebbe2f3aa5 service php7.4-fpm restart

docker exec -it eeebbe2f3aa5 nginx -s restart

### Porém reiniciando o servidor nginx ele vai finalizar o container, para reiniciar o container é necessário fazer o comando:

docker start eeebbe2f3aa5

docker start id_do_container

### Para acessar o terminal em si do sistema operacional que foi instalado no container:

docker exec -it 2be0c92e0df3 /bin/bash

### Ver os logs do nginx após entrar no terminal do sistema operacional do container:

cd /var/log/nginx

tail -f error.log

### Para reiniciar o servidor nginx e o php no próprio terminal do sistema operacional do container:

service php7.4-fpm restart

service nginx restart

### Para sair do terminal do sistema operacional do container:

exit

## Uma dica importante relacionada a volume e a extensão docker no vs code:
Eu tive um problema com a extensão do docker, onde qualquer alteração que eu fizesse em algum arquivo do container a partir da extensão, ele salvava como root mesmo eu especificando o usuario no dockerfile, acredito que deve haver alguma solução para isso, mas eu não consegui arrumar esse problema. Para isso utilizei a extensão Dev Container

Fazer teste para ver se está funcionando:

### docker exec -it 2be0c92e0df3 /bin/bash

esse 2be0c92e0df3 é o id do container

para entrar no terminal do container

poderá ir até o diretório /var/www/html/template que é o diretório que foi copiado como volume

### E fazer um touch teste como exemplo, ele irá criar um arquivo na máquina local a partir do terminal do container por conta do volume

e a pasta template é a pasta q foi puxada a partir do volume então é bom especificar o usuario e o grupo dela na maquina local para ter essas mesmas configurações no container, usar o comando: 

### sudo chown usuario:usuario /var/www/html/template

fazer esse comando antes de criar o container

### Exemplo de Docker com Adianti:

https://github.com/bjverde/formDocker/tree/master/adianti_debian11_php8.1

### Caso utilize o servidor apache ao invés do nginx deverá fazer isso:
 
ir no diretório do container etc/apache2/ports.conf e mudar a porta para a que foi especificada no container

### Comando para restartar o apache, estando dentro do terminal do sistema operacional do container usar o comando:

service apache2 restart

### d:) :v:
