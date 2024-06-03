# Configurando meu primeiro servidor WSL

Estarei utilizando um sistema Windows + WSL
Apache2 + PHP + MariaDB + phpMyAdmin

Para este projeto escolhi a distro Ubuntu 22.04
[!versao](/media/version.png)

## Apache

Primeira coisa a se fazer é instalar o Apache2
```sh
sudo apt update && sudo apt upgrade
sudo apt install apache2 -y
```
O uso do `-y` é para não precisar realizar a confirmação e seguir diretamente

Em seguida habilitar o "mod_rewrite"
```sudo a2enmod rewrite```

E por fim iniciar o serviço
```sudo service apache2 start```

### Testando
Apartir de um navegador na barra de pesquisa, pesquise <a>localhost</a>

## PHP

Será apenas necessário instalar o pacote PHP
```sudo apt install php```
Caso seja necessário instalar outras dependências, consulte a documentação do necessário

## MariaDB

Utilizei o banco de dados MariaDB e inicia-lo diretamente
```sh
sudo apt install mariadb-server
sudo service mysql start
```

### Instalação segura

```sudo mysql_secure_installation```
Passando a configuração de senha, confirmei todas as perguntas após isso
```sudo mariadb -u root -p```
Digitei a senha que escrevi durante esta etapa e digitei no terminal `exit`

### Criando um novo usuário
````sudo mariadb```
```sh
GRANT ALL ON *.* TO 'admin'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
FLUSH PRIVILEGES;

exit
```
Novo usuário criado com todos os privilégios

## phpMyAdmin

Primeira coisa sempre, instalar o pacote
```sudo apt install phpmyadmin```
E ativamos o módulo mbstring para conseguir manipular strings de multibyte
```sudo phpenmod mbstring```
E fazer a adição do serviço phpMyAdmin no arquivo apache2.conf localizado
na pasta /etc/apache2/
````sudo nano /etc/apache/apache2.conf```
Adicionando a seguinte linha ao final do arquivo
[!include](/media/include-path.png)
Reiniciando o servidor web
```sudo systemctl apache2 restart```

Com um navegador da sua preferência, acesse o <a>'localhost/phpmyadmin'</a>

## Notas

Esse aprendizado me deixou muito contente, mesmo sendo simples. Esta é minha nota de aprendizado.
Tudo foi tirado a partir do [!Medium](https://marcelo-albuquerque.medium.com/instala%C3%A7%C3%A3o-e-configura%C3%A7%C3%A3o-de-servidor-web-no-wsl-2-ubuntu-20-04-cacefd1baee1)