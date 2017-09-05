## Instalar wordpress en ubuntu 16.04

Correr primero este comando que actualiza todos los paquetes.

```bash
sudo apt-get update
```

#### Primero debes acceder al servidor:

reemplazas **[ip]** con la ip del servidor.

```bash
ssh root@[ip]
```

#### Luego se debes actualizar los paquetes:

```bash
sudo apt-get update
```

#### Instalar paquetes basicos:

```bash
sudo apt-get install curl wget git zip
```

#### Instalar nginx:

```bash
sudo apt-get install nginx -y
```

#### Instalar mysql:
En la instalación tienes que crear una contraseña. Tenla a mano y que sea segura.

```bash
sudo apt-get install mysql-server -y
```

#### Crear base de datos:

reemplazas [nombre] con el nombre que debe tener la base de datos.

reemplazas [contraseña] con la contraseña de mysql.
```bash
mysql --u root --p[contraseña]
mysql > create database [nombre]
```

#### Instalar PHP:

```bash
sudo apt-get install php-fpm php-mysql -y
```

#### Instalar wordpress:

```bash
curl -O https://wordpress.org/latest.zip
unzip latest
```

#### Ingresas a la carpeta que se descomprimio y copias el archivo de configuración:
```bash
  cd wordpress
  cp wp-config-sample.php wp-config.php
```

#### Editar el archivo de configuración con el editor nano:
```bash
  nano wp-config.php
```

Cierras el editor con ctrl + x y oprimes la tecla Y y luego enter para guardar los cambios.

#### Configurar nginx vhost:

```bash
  cd /etc/nginx/sites-available
  nano default
```

borras todo lo que tenga el archivos y lo reemplazas con esto:

Reemplazar [dominio] con el dominio que se necesite.

```bash
server {
    listen 80;

    root /var/www/wordpress/public;
    index index.php index.html index.htm;

    server_name [dominio] www.[dominio];

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        try_files $uri /index.php =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}

```

#### Reiniciar nginx:

```bash
  sudo service nginx
```

Y listo!
