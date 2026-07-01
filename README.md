# Minecraft For Honor Hispano

Servidor Minecraft comunitario de For Honor Hispano, dockerizado con itzg/minecraft-server y preparado para operar en produccion con configuracion persistente, RCON y despliegue sencillo.

<div align="center">

![Minecraft](https://img.shields.io/badge/Minecraft-Fabric%201.20.1-3CB371?style=for-the-badge&logo=minecraft&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Comunidad](https://img.shields.io/badge/Comunidad-For%20Honor%20Hispano-ff6b00?style=for-the-badge)

</div>

## Caracteristicas

✅ Servidor dedicado de la comunidad en `minecraft.forhonorhispano.com`  
✅ Stack Docker con persistencia completa en `./data/`  
✅ RCON habilitado para administracion remota  
✅ Configuracion public-safe con archivos `*.example`  
✅ Despliegue rapido con `docker compose`

## Inicio rapido

```bash
git clone https://github.com/joseangelalejo/forhonorhispanominecraft.git
cd forhonorhispanominecraft

cp .env.example .env
cp docker-compose.example.yml docker-compose.yml
cp data/.rcon-cli.env.example data/.rcon-cli.env
cp data/.rcon-cli.yaml.example data/.rcon-cli.yaml
cp data/server.properties.example data/server.properties

docker compose up -d
docker compose logs -f mc
```

## Datos del servidor

- IP: `minecraft.forhonorhispano.com`
- Puerto Java: `25565`
- RCON: `25575`

## Comunidad

### Unete a nuestra comunidad

- Discord (entra y participa): [Discord.gg/forhonorhispano](https://discord.gg/GYY89fHv75)
- Comunidad de Steam: [Steam Community](https://steamcommunity.com/groups/forhonorhispano)
- Web oficial: [For Honor Hispano](https://forhonorhispano.com)
- Directos en Twitch: [Twitch](https://twitch.tv/forhonorhispano)
- Canal de YouTube: [YouTube](https://www.youtube.com/@forhonorhispano)

### Torneos y competitivo

- Nuestro perfil en Battlefy: [Battle](https://battlefy.com/for-honor-hispano)
- 1er TORNEO (Forja del Primer Campeon): [Enlace al Torneo](https://battlefy.com/for-honor-hispano/forja-del-primer-campeon/6a3f16ab5e118000297e4f05/info?infoTab=details)

### Apoya los proyectos

Todo este ecosistema (web, servidores y dominios) se mantiene gracias a la comunidad.

- Bote de PayPal (mejoras del servidor): [SAI Battery](https://www.paypal.com/pool/9quGCGhQ8r?sr=wccr)

## GitHub Pages

Documentacion web del proyecto:

- [GitHub Pages](https://joseangelalejo.github.io/forhonorhispanominecraft/)

Archivos de la web en: `docs/`

## Estructura

```text
forhonorhispanominecraft/
├── docker-compose.example.yml
├── docker-compose.yml          # local, no versionar
├── data/
│   ├── mods/
│   ├── config/
│   └── ...
├── docs/
│   └── index.html
└── README.md
```

## Seguridad y publicacion

- No subas archivos reales con secretos (`.env`, `docker-compose.yml`, `.rcon-cli.*`, `server.properties`).
- Usa siempre las plantillas `*.example`.
- Si alguna credencial estuvo expuesta anteriormente, rotala antes de publicar, así como API keys, tokens y contraseñas de servicios externos.

## Hashtags

#ForHonor #ForHonorHispano #Gaming #Torneos #Minecraft #ComunidadGaming
