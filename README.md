
# 🚀 Instalación de WordPress en Kali Linux usando Docker

Guía paso a paso para instalar **WordPress + MariaDB** en **Kali Linux** usando Docker Compose. Ideal para pruebas de seguridad, desarrollo web o laboratorios de pentesting.

---

## 🎯 Objetivo

Crear un entorno local funcional de **WordPress** en **Kali Linux** utilizando contenedores Docker, sin afectar tu sistema principal.

---

## 🛠️ Requisitos previos

Asegúrate de tener instalado lo siguiente:

sudo apt update && sudo apt install docker.io docker-compose git -y

- Docker: Para ejecutar contenedores aislados.
- Docker Compose: Para definir múltiples servicios (WordPress + MariaDB).
- Git (opcional): Para clonar o versionar este repositorio.

---

## 📁 Paso 1: Crear carpeta del proyecto

mkdir ~/wordpress-docker
cd ~/wordpress-docker

---

## 📝 Paso 2: Crear el archivo docker-compose.yml

nano docker-compose.yml

Pega lo siguiente:

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

Guarda con Ctrl + O, luego Enter, y sal con Ctrl + X.

---

## ▶️ Paso 3: Levantar los contenedores

docker-compose up -d

Esto descargará e iniciará dos contenedores:
- wordpress-db (MariaDB)
- wordpress (sitio web)

Accede a tu sitio en:

http://localhost:8000

---

## 🛑 Paso 4: Detener los contenedores

docker-compose down

⚠️ No uses docker-compose down -v si deseas conservar la base de datos.

---

## 📦 Archivos incluidos

| Archivo               | Descripción                          |
|-----------------------|--------------------------------------|
| docker-compose.yml    | Configuración de WordPress + MariaDB |

---

## 💡 Recomendaciones

- Este entorno es ideal para pruebas locales o labs de seguridad.
- Puedes duplicar esta estructura para múltiples sitios cambiando el puerto.
- No expongas este entorno a internet sin protección.

---

## 📌 Uso con Git

cd ~/wordpress-docker

nano README.md

git add README.md
git commit -m "Añadido README.md con guía completa"
git push -u origin master

---

## 🤝 Créditos

Creado por @chechoinformatico  
Para uso personal y educativo.
