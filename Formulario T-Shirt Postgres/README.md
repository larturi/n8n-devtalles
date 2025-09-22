# Formulario T-Shirt con PostgreSQL

Este proyecto implementa un formulario para pedidos de camisetas personalizadas utilizando PostgreSQL como base de datos, configurado con Docker Compose.

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
cd "Formulario T-Shirt Postgres"
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

## 🔧 Comandos Útiles

### Docker Compose

```bash
# Levantar servicios
docker-compose up -d

# Parar servicios
docker-compose down

# Parar y eliminar volúmenes
docker-compose down -v

# Ver logs
docker-compose logs -f db

# Ejecutar comandos en el contenedor
docker-compose exec db psql -U n8n -d n8n_poc
```

### Base de Datos

```bash
# Conectar a PostgreSQL
docker-compose exec db psql -U n8n -d n8n_poc

# Crear tabla de inventario
CREATE TABLE inventory (
    id SERIAL PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    size VARCHAR(10) NOT NULL,
    stock INTEGER DEFAULT 1
);

# Insertar datos
INSERT INTO public.inventory
(product_name, "size", stock)
VALUES('Remera negra', 'S', 10);

INSERT INTO public.inventory
(product_name, "size", stock)
VALUES('Remera negra', 'M', 15);

INSERT INTO public.inventory
(product_name, "size", stock)
VALUES('Remera negra', 'L', 12);
```
