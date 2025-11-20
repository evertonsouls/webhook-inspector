# Webhook Inspector

Proyecto monorepo (API + frontend) para capturar e inspeccionar webhooks. Incluye una API en Fastify con documentación Swagger/Scalar y una interfaz React con Vite.

## Requisitos
- Node.js 18+ y `pnpm` (usado con `pnpm@10.22.0`).
- Docker (opcional) para levantar PostgreSQL localmente.

## Instalación
1. Instala dependencias desde la raíz:
   ```bash
   pnpm install
   ```
2. Crea `api/.env` con la conexión a la base de datos:
   ```bash
   DATABASE_URL=postgresql://docker:docker@localhost:5432/webhooks
   PORT=3333
   NODE_ENV=development
   ```
3. (Opcional) Levanta PostgreSQL con Docker:
   ```bash
   cd api
   docker compose up -d
   ```

## Uso
1. Ejecuta las migraciones del backend:
   ```bash
   pnpm --filter api db:migrate
   ```
2. Inicia la API (http://localhost:3333 y docs en /docs):
   ```bash
   pnpm --filter api dev
   ```
3. Inicia el frontend (http://localhost:5173 por defecto):
   ```bash
   pnpm --filter web dev
   ```

## Tecnologías principales
- Fastify + Zod + Swagger/Scalar para la API.
- Drizzle ORM con PostgreSQL.
- React 19 + Vite + TypeScript para la web.
- Biome para formateo y linting.
