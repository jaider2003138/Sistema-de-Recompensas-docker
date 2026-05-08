# Docker

Este proyecto queda orquestado desde la carpeta raiz `sistema-Recompensa`.

## Servicios

- `db`: PostgreSQL 16 con esquema inicial automatico
- `backend`: API Node.js/Express
- `tests`: suite Playwright para la API

## Levantar backend + base de datos

```bash
docker compose up --build
```

La API quedara disponible en:

```text
http://localhost:3000
```

## Correr las pruebas automatizadas en Docker

```bash
docker compose --profile tests up --build --abort-on-container-exit tests
```

Ese comando:

- levanta `db`
- levanta `backend`
- espera a que `backend` este saludable
- ejecuta `tests`

## Detener y limpiar

```bash
docker compose down
```

Si tambien quieres borrar el volumen de PostgreSQL:

```bash
docker compose down -v
```

## Notas

- La base de datos se inicializa con `docker/postgres/init.sql`.
- El backend dentro de Docker usa estas credenciales:
  - `DB_HOST=db`
  - `DB_PORT=5432`
  - `DB_USER=postgres`
  - `DB_PASSWORD=postgres`
  - `DB_NAME=sistema_recompensas`
- Playwright toma la URL de la API desde `API_BASE_URL`.
