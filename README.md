# forhonorhispanominecraft

Repositorio preparado para publicarse sin exponer secretos del servidor.

## Estado del repo (analizado)

- Rama actual: `main`
- Historial detectado: `1 commit`
- Último commit: `6bbfb64 - First commit`
- Riesgo detectado: había secretos en archivos locales (por ejemplo contraseñas RCON y `management-server-secret`) dentro de `docker-compose.yml`, `data/.rcon-cli.env`, `data/.rcon-cli.yaml` y `data/server.properties`.

## Archivos plantilla creados

- `.env.example`
- `docker-compose.example.yml`
- `data/.rcon-cli.env.example`
- `data/.rcon-cli.yaml.example`
- `data/.install-fabric.env.example`
- `data/server.properties.example`

## Uso local (sin exponer secretos)

1. Copia plantillas a archivos locales privados:

```bash
cp .env.example .env
cp docker-compose.example.yml docker-compose.yml
cp data/.rcon-cli.env.example data/.rcon-cli.env
cp data/.rcon-cli.yaml.example data/.rcon-cli.yaml
cp data/server.properties.example data/server.properties
```

2. Edita los valores sensibles:

- `RCON_PASSWORD`
- `MANAGEMENT_SERVER_SECRET`
- `rcon.password`
- cualquier dominio/host privado

3. Arranca el servidor:

```bash
docker compose up -d
```

## Reglas de seguridad aplicadas

El `.gitignore` ahora excluye:

- secretos (`.env`, llaves y certs)
- archivos docker locales (`docker-compose.yml`, overrides y backups)
- datos runtime del server (`data/forhonorhispano`, logs, crashes, cache, mods, libraries, versiones, etc.)
- archivos de admin y jugadores (`ops`, `whitelist`, `usercache`, `banned-*`, `server.properties`, `.rcon-cli.*`)

Y mantiene versionables los ejemplos (`*.example`).

## Importante antes de hacerlo público

Si algún secreto llegó a estar en commits anteriores, hay que rotarlo y limpiar historial.

1. Rotar secretos ya expuestos:

- Cambia `RCON_PASSWORD`
- Cambia `MANAGEMENT_SERVER_SECRET`
- Cambia cualquier token/clave adicional

2. Quitar del índice los archivos sensibles que ya estén trackeados:

```bash
git rm --cached docker-compose.yml data/.rcon-cli.env data/.rcon-cli.yaml data/server.properties data/ops.json data/whitelist.json data/banned-ips.json data/banned-players.json data/usercache.json data/usernamecache.json
```

3. Si esos secretos estuvieron en el historial y quieres publicación limpia, reescribe historial antes de publicar.

Ejemplo con `git filter-repo`:

```bash
# Instalar (si no lo tienes):
# pip install git-filter-repo

git filter-repo \
  --path docker-compose.yml --invert-paths
```

Luego vuelve a añadir la plantilla (`docker-compose.example.yml`) y configura tu archivo local privado.

## Alcance

Este ajuste no hace commits, no hace push y no publica el repositorio. Solo deja una base segura para que tú decidas cuándo publicarlo.
