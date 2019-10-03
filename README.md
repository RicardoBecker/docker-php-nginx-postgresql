# Descrição

Docker utilizando o composer, arquivo de configuração com variáveis de ambiente, criando um container nginx 1.17.4 e um container php 7.3.10-fpm ligados através de um link e criando um container postgres 11.5

# Configuração Container Nginx

1. Exposição de portas

	80 e 443

2. Volume (Obs: verificar se na configuração do docker os drivers estão compartilhados)

	Aplicação: htdocs -> /var/www/html
	
	Logs: nginx/logs -> /var/log/nginx
	
	Virtual Host: nginx/sites -> /etc/nginx/conf.d
	
3. Virtual Host

	Criação do vhost modelo http://api.dev (vhost modificável)

# Configuração Container Php

1. Exposição de portas

	9000

2. Volume (Obs: verificar se na configuração do docker os drivers estão compartilhados)

	Aplicação: htdocs -> /var/www/html
	
3. Bibliotecas

	Habilitação de bibliotecas do php através de arquivo de configuração. Ex: MBSTRING, GD, MCRYPT, PDO_MYSQL, etc.
	
# Configuração Container Postgresql

1. Exposição de portas

	5432

2. Volume (Obs: verificar se na configuração do docker os drivers estão compartilhados)

	Aplicação: postgresql/data -> /var/lib/postgresql/data

3. Configuração para conexão

	- POSTGRES_DB       = teste
	
    - POSTGRES_USER     = root
	
    - POSTGRES_PASSWORD = root
	
    - POSTGRES_PORT     = 5432
	
# Como utitilizar

1. Clonar o repositório usando o comando:

   git clone 

2. Entre na pasta php-nginx-postgresql e copie o arquivo env-example para .env

   cp env-example .env

3. Rode seu container:

   docker-compose up -d

4. Adicione os domínios no arquivo de hosts.

   127.0.0.1 localhost

   127.0.0.1 api.dev

5. Acessar o shell do container:
    
	docker exec -it nginx bash

	docker exec -it php-fpm bash
	
	docker exec -it postgresql bash
	
6. Abra no navegador

   http://localhost

7. Acessar o banco de dados dentro do container Postgresql

	psql default default

8. Comandos básicos para utilizar o banco de dados

	\l;

	CREATE DATABASE teste;
	
	\connect teste;
	
	\dt;
	
	CREATE TABLE pessoa (id serial primary key, nome varchar(60) not null);
	
	INSERT INTO pessoa(nome) VALUES ('maria');

	INSERT INTO pessoa(nome) VALUES ('joao');

	INSERT INTO pessoa(nome) VALUES ('julia');

	INSERT INTO pessoa(nome) VALUES ('pedro');