
# IMPLEMENTAÇÃO DE UM PROXY REVERSO PARA APLICAÇÕES WEB BASEADAS EM CONTEINÊRES USANDO NGINX E DOCKER.

Escopo:

** 1. Instalar o NGINX na Máquina Local **
Criar 3 Virtualhosts no NGINX para os domínios abaixo, implementando, para os contêineres do
passo 2, via proxy_pass os seguintes domínios:

´´´app1.4linux.local.com.br;
app2.4linux.local.com.br;
app3.4linux.local.com.br;

** 2. Instalar o Docker na Maquina Local **
Criar 3 contêineres com os seguintes nomes:
´´´
app1
app2
app3
´´´
Cada container deve ser criado com a implementação de um Wordpress
Avalie todas as necessidades para que o Wordpress fique ativo no ambiente.
Cada container deve ter uma um Tema do Wordpress diferente para diferenciar cada aplicação.

Vamos utilizar a distribuição Debian 10 (Buster) no projeto.

Ok, já temos o escopo do projeto, então, vamos preparar o ambiente para receber as configurações.

Primeiramente vamos atualizar o nosso sistema

 ```apt update -y´´´

Vamos instalar o Nginx

´´´apt install nginx -y´´´

**Configuração do Certificado SSL para as aplicações
´´´openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/cert.key -out /etc/nginx/cert.crt´´´

/etc/nginx/sites-available/app1.conf


´´´.server {
        listen 80;
        server_name app1.4linux.local.com.br;
        root /opt/docker/app1;
        index index.php index.html index.htm;

        access_log /var/log/nginx/app1-access.log;
        error_log /var/log/nginx/app1-error.log;

        location / {
                proxy_pass http://app1.4linux.local.com.br;
               }

}
´´´
