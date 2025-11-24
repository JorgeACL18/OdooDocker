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

## PgAdmin
Ahora que tenemos ejecutando nuestro docker compose, tenemos que entrar a `localhost:5050` para acceder a la página de PgAdmin. En esta página tendremos que crear un servidor que servirá como base de datos para Odoo, en mi caso lo hice así:

<img width="1625" height="1441" alt="Captura de pantalla 2025-11-24 162000" src="https://github.com/user-attachments/assets/26b2dc82-9c7f-4852-83f6-7f773dc8a866" />
<img width="1625" height="1441" alt="Captura de pantalla 2025-11-24 161945" src="https://github.com/user-attachments/assets/c51cf581-aeb2-434e-a263-a4019da4fd8e" />
<img width="2082" height="1527" alt="Captura de pantalla 2025-11-24 162025" src="https://github.com/user-attachments/assets/73358335-b85e-423c-ab8f-832e38fdc69c" />






