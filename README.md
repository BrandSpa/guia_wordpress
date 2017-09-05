## Instalar wordpress en ubuntu 16.04
-----

Correr primero este comando que actualiza todos los paquetes.

Primero debes acceder al servidor:
```bash
ssh root@ip
```

Luego se debes actualizar los paquetes:

```bash
sudo apt-get update
```
Instalar paquetes basicos:

```bash
sudo apt-get install curl wget git zip
```

Instalar nginx:

```bash
sudo apt-get install nginx -y
```

Instalar mysql:

```bash
sudo apt-get install mysql-server -y
```

Crear base de datos:

reemplazas [nombre] con el nombre que debe tener la base de datos.

reemplazas [contraseña] con la contraseña de mysql.
```bash
mysql --u root --p[contraseña]
mysql > create database [nombre]
```

Instalar wordpress:

```bash
curl -O https://wordpress.org/latest.zip
unzip latest
```

Ingresas a la carpeta que se descomprimio y crear el copias el archivo de configuración:
```bash
  cd wordpress
  cp wp-config-sample.php wp-config.php
```

Editar el archivo de configuración con el editor nano:
```bash
  nano wp-config.php
```

Cierras el editor con ctrl + x y oprimes la tecla Y y luego enter para guardar los cambios.
