# PostgreSQL + PpAdmin + DBeaver  | La herramineta perfecta para gestión de BBDD

Este entorno Dockerizado te permite levantar una base de datos PostgreSQL lista para usar, acompañada por una interfaz web PgAdmin4. También se recomienda el uso de **DBeaver** desde Windows para conectarse, gestionar y consultar la base de datos de forma gráfica.

---

## 📦 Servicios incluidos

- **PostgreSQL** (última versión)
- **PgAdmin4** (interfaz web para gestión de la base de datos)
- **DBeaver** (cliente de escritorio recomendado en Windows)

---

## ⚙️ docker-compose.yml

```yaml
services:
  postgres:
    image: postgres:latest
    container_name: postgres
    restart: always
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: admin
      POSTGRES_DB: midatabase
    ports:
      - "5433:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  pgadmin:
    image: dpage/pgadmin4:latest
    container_name: pgadmin
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: info@genbyte.info
      PGADMIN_DEFAULT_PASSWORD: password
    ports:
      - "8000:80"
    depends_on:
      - postgres

volumes:
  postgres_data:
```

---

## ▶️ Instrucciones de uso

### 1. Clonar o crear el archivo `docker-compose.yml`

Asegúrate de tener el archivo con el contenido mostrado arriba.

### 2. Levantar los servicios

```bash
docker-compose up -d
```

Esto iniciará:
- PostgreSQL escuchando en el puerto **5433**
- PgAdmin accesible desde `http://localhost:8000`

### 3. Acceder a PgAdmin

Abre el navegador y visita: [http://localhost:8000](http://localhost:8000)  
Credenciales:
- **Email**: `info@mail.info`
- **Password**: `password`

Una vez dentro, deberás **añadir manualmente la conexión al servidor PostgreSQL** con:
- **Host**: `postgres`
- **Puerto**: `5432`
- **Usuario**: `admin`
- **Contraseña**: `admin`

### 4. Acceder desde Windows con DBeaver

1. Descarga DBeaver: https://dbeaver.io/
2. Crea una nueva conexión PostgreSQL
3. Configura la conexión con estos datos:

```
Host: IP del servidor Ubuntu o localhost (si es WSL)
Puerto: 5433
Base de datos: midatabase
Usuario: admin
Contraseña: admin
```

4. ¡Conectado! Ahora puedes explorar, consultar y administrar tu base de datos desde una interfaz cómoda.

---

## 🖥️ Recomendación adicional

También puedes utilizar **DBeaver** en Windows para la gestión y administración de servidores SQL.  
DBeaver ofrece una interfaz moderna y soporte para múltiples motores de base de datos (PostgreSQL, MySQL, Oracle, SQLite, entre otros).

---

## 🧹 Comandos útiles

- Detener los contenedores:
- 
  ```bash
  docker compose down
  ```

- Ver logs de PostgreSQL:
- 
  ```bash
  docker logs postgres
  ```

- Ver logs de pgAdmin:
- 
  ```bash
  docker logs pgadmin
  ```

---

## 🧱 Volúmenes y persistencia

Los datos del contenedor PostgreSQL se guardan en el volumen `postgres_data`, lo que garantiza la persistencia incluso si los contenedores se eliminan.

---
