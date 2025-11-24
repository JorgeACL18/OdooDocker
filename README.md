# Instalación de Odoo con Docker
En esta tarea tenemos que prepara el IDE PyCharm para crear nuestro archivo .yml para poder hacer la instalación de Odoo.

## PyCharm
Una vez hayamos instalado el plugin de Docker en nuestro IDE, tenemos que crear el archivo `docker-compose.yml` para empezar a poner los servicios, los cuales quedarían así:
```
services:
  db:
    image: postgres:17
    container_name: odoo18_db
    environment:
      POSTGRES_DB: postgres
      POSTGRES_USER: odoousr
      POSTGRES_PASSWORD: odoopsswrd
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

  web:
    image: odoo:18.0
    container_name: odoo18_app
    depends_on:
      - db
    ports:
      - "8069:8069"
    environment:
      HOST: db
      USER: odoousr
      PASSWORD: odoopsswrd
      ODOO_MASTER_PASSWD: odoo
    volumes:
      - web_data:/var/lib/odoo
      - ./addons:/mnt/extra-addons
    restart: unless-stopped

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin4_odoo18
    depends_on:
      - db
    ports:
      - "5050:80"
    environment:
      PGADMIN_DEFAULT_EMAIL: jacl@gmail.com
      PGADMIN_DEFAULT_PASSWORD: admin
    volumes:
      - pgadmin_data:/var/lib/pgadmin
    restart: unless-stopped
volumes:
  postgres_data:
  web_data:
  pgadmin_data:
```
