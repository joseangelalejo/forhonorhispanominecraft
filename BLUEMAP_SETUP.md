# BlueMapp 3D Map Setup

## Overview

BlueMapp generates a 3D isometric map visualization of your Minecraft world accessible via web interface.

**Access:** http://server-ip:8100

## Configuration

### Docker Service (docker-compose.yml)

The BlueMapp service is configured in `docker-compose.yml` with:
- **Image:** `ghcr.io/bluemap-minecraft/bluemap:latest`
- **Command flags:** `-r -u -w`
  - `-r`: Enable rendering
  - `-u`: Enable update watching
  - `-w`: Enable web server
- **Port:** 8100 (TCP)
- **Volumes:**
  - `./bluemap/config:/app/config` - Configuration files
  - `./data/forhonorhispano:/app/world` - Minecraft world data
  - `./bluemap/data:/app/data` - Render progress and cache
  - `./bluemap/web:/app/web` - Generated web tiles

### Initial Setup

1. **Start the container:**
   ```bash
   docker compose up -d bluemap
   ```

2. **Generate configuration:**
   ```bash
   docker run --rm -v "$(pwd)/bluemap/config:/app/config" \
     ghcr.io/bluemap-minecraft/bluemap:latest
   ```

3. **Critical: Enable Mojang Resources**
   Edit `bluemap/config/core.conf`:
   ```
   # MUST be set to true for rendering to work
   accept-download: true
   ```

4. **Fix file permissions:**
   ```bash
   sudo chown -R $(whoami):$(whoami) bluemap/config
   sudo chmod -R 755 bluemap/config
   sudo chmod 644 bluemap/config/*.conf
   sudo chmod 644 bluemap/config/maps/*.conf
   ```

5. **Restart BlueMapp:**
   ```bash
   docker compose restart bluemap
   ```

## Configuration Files Reference

### `core.conf` - Core Settings

- `accept-download: true` - **REQUIRED** - Enables Mojang resource downloads
- `data: "data"` - Render progress storage
- `render-thread-count: 1` - CPU threads (adjust based on server load)
- `scan-for-mod-resources: true` - Load modpack resources

### `webserver.conf` - Web Server Settings

- `enabled: true` - Enable web interface
- `port: 8100` - Web server port
- `webroot: "web"` - Output directory

### Map Configs (`maps/*.conf`)

Each dimension has a config file:
- `overworld.conf` - Main world
- `nether.conf` - Nether dimension
- `end.conf` - End dimension

**Important Path Setting:**
- `world: "world"` - Path relative to /app in container (where ./data/forhonorhispano is mounted)

## Monitoring Rendering

### Check logs:

```bash
docker compose logs bluemap -f
```

### Watch rendering progress:

```bash
watch "du -sh ./bluemap/web/maps/overworld/"
```

### Web tiles directory:

```bash
ls -la ./bluemap/web/maps/
```

## Storage Locations

```
bluemap/
├── config/          # Configuration files (tracked in template)
│   ├── *.conf      # Generated on first run
│   ├── maps/       # Dimension configs
│   └── storages/   # Storage backends
├── data/           # Render progress & cache (.gitignored)
└── web/            # Generated map tiles (.gitignored)
```

## Important Notes

- **First render:** Large worlds may take considerable time (hours)
- **No server restart needed:** BlueMapp runs independently
- **Live updates:** Watch flag (`-u`) monitors world changes during gameplay
- **Mod resources:** `scan-for-mod-resources: true` loads custom mod textures
- **Non-blocking:** Rendering doesn't impact active player gameplay

## Troubleshooting

### "There was an error trying to load this map!"

- Rendering still in progress - wait for tiles to generate
- Check `bluemap/web/maps/` directory has files

### Container restart loop

- Verify `accept-download: true` in `core.conf`
- Check permissions: `chown` and `chmod` fixes

### High CPU usage

- Reduce `render-thread-count` in `core.conf`
- Or set to `-1` to auto-calculate based on CPU cores

## References

- **BlueMap Docs:** https://bluemap.bluecolored.de/wiki/
- **Docker Setup:** https://github.com/BlueMap-Minecraft/BlueMap/wiki/Docker-Setup
- **Official Repository:** https://github.com/BlueMap-Minecraft/BlueMap
