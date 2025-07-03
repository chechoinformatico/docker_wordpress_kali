# Instalando WordPress en Kali Linux con Docker

Este repositorio contiene una configuración básica y funcional para levantar un entorno local de **WordPress + MariaDB** usando **Docker Compose**, ideal para pruebas de seguridad, desarrollo web o laboratorios de pentesting.

---

## 🧰 Requisitos previos

Asegúrate de tener instalado:

```bash
sudo apt update && sudo apt install docker.io docker-compose git -y📄 Archivo README.md – "Instalando WordPress en Kali Linux con Docker" 
markdown
 
 
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
⌄
⌄
⌄
⌄
# Instalación de WordPress en Kali Linux usando Docker

Guía paso a paso para instalar **WordPress + MariaDB** en **Kali Linux** usando **Docker Compose**. Ideal para pruebas de seguridad, desarrollo web o laboratorios de pentesting.

---

## 🧰 Objetivo

Crear un entorno local funcional de **WordPress** en **Kali Linux** usando contenedores Docker, sin afectar el sistema principal.

---

## 🛠️ Requisitos previos

Asegúrate de tener instalado:

```bash
sudo apt update && sudo apt install docker.io docker-compose git -y
 
 

    Docker : Para correr contenedores aislados.
    Docker Compose : Para definir múltiples servicios (WordPress + MariaDB).
    Git : Opcional, para respaldar/configurar este repositorio.
     

 
📁 Paso 1: Crear una carpeta del proyecto 

Crea y accede a la carpeta donde trabajarás: 
bash
 
 
1
2
mkdir ~/wordpress-docker
cd ~/wordpress-docker
 
 
 
📝 Paso 2: Crear el archivo docker-compose.yml 

Ejecuta: 
bash
 
 
1
nano docker-compose.yml
 
 

Y pega este contenido: 
yaml
 
 
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
⌄
⌄
⌄
⌄
⌄
⌄
⌄
⌄
⌄
⌄
version: '3'
services:
  wordpress-db:
    image: mariadb:latest
    container_name: wordpress-db
    environment:
      MYSQL_ROOT_PASSWORD: admin123
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wp123
    volumes:
      - db_data:/var/lib/mysql
    restart: no

  wordpress:
    image: wordpress:latest
    container_name: wordpress
    depends_on:
      - wordpress-db
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: wordpress-db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wp123
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wp_data:/var/www/html
    restart: no

volumes:
  db_data:
  wp_data:
 
 

Guarda el archivo con Ctrl + O, Enter → Ctrl + X. 
 
▶️ Paso 3: Levantar los contenedores 

Desde dentro de la carpeta: 
bash
 
 
1
docker-compose up -d
 
 

Esto descargará e iniciará dos contenedores: 

    MariaDB  (base de datos)
    WordPress 
     

Tu sitio estará disponible en: 
 
 
1
http://localhost:8000
 
 
 
🛑 Paso 4: Detener los contenedores 

Cuando termines, detén los contenedores con: 
bash
 
 
1
docker-compose down
 
 

    ⚠️ No uses docker-compose down -v si no quieres borrar tus datos. 
     

 
📦 Archivos incluidos 
docker-compose.yml
	
Configuración de WordPress + MariaDB
 
 
 
💡 Recomendaciones 

    Este entorno es ideal para pruebas locales o laboratorios de seguridad.
    Puedes duplicar esta estructura para crear múltiples sitios en distintos puertos.
    No expongas este entorno públicamente sin protección.
     

 
🤝 Créditos 

Creado por @chechoinformatico 
Para uso personal y educativo. 
 
 
1
2
3
4
5
6
7
8
9

---

## ✅ ¿Cómo usarlo?

1. Abre tu terminal y ve a tu carpeta:

```bash
cd ~/wordpress-docker
 
 

    Crea el archivo:
     

bash
 
 
1
nano README.md
 
 

    Pega todo el contenido de arriba  

    Guarda con: 
     

    Ctrl + O → Enter → Ctrl + X
     

    Añádelo al repositorio Git:
     

bash
 
 
1
2
3
git add README.md
git commit -m "Añadido README.md con guía completa"
git push -u origin master
