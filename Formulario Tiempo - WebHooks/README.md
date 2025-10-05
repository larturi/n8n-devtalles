# Formulario T-Shirt con PostgreSQL

Este proyecto implementa un formulario de solicitud de tiempo libre a RRHH utilizando PostgreSQL como base de datos, configurado con Docker Compose.

## 🚀 Características

- Base de datos PostgreSQL 16 Alpine
- Configuración con Docker Compose
- Volúmenes persistentes para los datos

## 📋 Requisitos Previos

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 🛠️ Instalación y Configuración

### 1. Clonar el repositorio

```bash
git clone <url-del-repositorio>
```

### 2. Configurar la base de datos

El archivo `docker-compose.yaml` ya está configurado con:

- **Base de datos:** PostgreSQL 16 Alpine
- **Puerto:** 5432
- **Base de datos:** n8n_poc
- **Usuario:** n8n
- **Contraseña:** n8n

### 3. Inicializar scripts (opcional)

Si necesitas scripts de inicialización, colócalos en la carpeta `./initdb/` y serán ejecutados automáticamente al crear el contenedor.

### 4. Ejecutar el proyecto

```bash
# Levantar los servicios
docker-compose up -d

# Ver los logs
docker-compose logs -f

# Verificar el estado
docker-compose ps
```

## 🗄️ Configuración de la Base de Datos

### Conexión

- **Host:** localhost
- **Puerto:** 5432
- **Base de datos:** n8n_poc
- **Usuario:** n8n
- **Contraseña:** n8n

### Ejemplo de conexión con psql

```bash
psql -h localhost -p 5432 -U n8n -d n8n_poc
```

### Ejemplo de conexión con URL

```bash
postgresql://n8n:n8n@localhost:5432/n8n_poc
```

### Base de Datos

```bash
# Conectar a PostgreSQL
docker-compose exec db psql -U n8n -d n8n_poc

# Crear tabla de inventario
CREATE TABLE days_off (
    id SERIAL PRIMARY KEY,
    email VARCHAR(100) NOT NULL,
    vacation_days SMALLINT,
    sick_days SMALLINT
);

# Insertar datos
INSERT INTO public.days_off
(id, email, vacation_days, sick_days)
VALUES(nextval('days_off_id_seq'::regclass), 'youremail@gmail.com', 7, 5);
```
