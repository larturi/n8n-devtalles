## Cómo construir y correr el contenedor

```bash
docker build -t postgres-pgvector .
```

Luego, levantá el contenedor:

```bash
docker run --name pgvector-db \
  -e POSTGRES_PASSWORD=postgres \
  -v ./data:/var/lib/postgresql/data \
  -p 5432:5432 \
  -d postgres-pgvector
```

Conectate al contenedor:

```bash
docker exec -it pgvector-db psql -U postgres -c "CREATE DATABASE embeddings_db;

ALTER TABLE public.n8n_vectors ADD file_id varchar NULL;

CREATE TABLE IF NOT EXISTS ingested_files (
  file_id        text PRIMARY KEY,         -- Google Drive file id
  name           text,
  mime_type      text,
  md5_checksum   text,
  modified_time  timestamptz,
  last_ingested  timestamptz DEFAULT now()
);
"
```

Dentro de psql, activá la extensión:

```bash
CREATE EXTENSION vector;
```

Deberías ver algo como:
vector | 0.6.0 | public | vector data type and functions

En tu n8n, usás la URL:
postgres://postgres:postgres@localhost:5432/embeddings_db