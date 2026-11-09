<p align="center"><a href="https://coopgames.app/es"><img src="logo.svg" alt="CoopGames" width="320"></a></p>

# Servidor MCP de CoopGames

[English](README.md)

Un servidor [MCP](https://modelcontextprotocol.io) gratis y de solo lectura para que los asistentes de IA respondan «¿a qué jugamos?». Pide juegos por número de jugadores, plataformas, crossplay, cooperativo en el sillón o precio, y la respuesta sale del catálogo de juegos cooperativos y multijugador de [CoopGames](https://coopgames.app/es).

- **URL:** `https://coopgames.app/mcp`
- **Transporte:** Streamable HTTP
- **Autenticación:** ninguna
- **Nombre en el registro:** `app.coopgames/coopgames`

## Conectarlo

**Claude Code**

```bash
claude mcp add --transport http coopgames https://coopgames.app/mcp
```

**Claude (web y escritorio):** Configuración → Conectores → Agregar conector personalizado → pega `https://coopgames.app/mcp`.

**Cursor** (`~/.cursor/mcp.json`)

```json
{ "mcpServers": { "coopgames": { "url": "https://coopgames.app/mcp" } } }
```

**VS Code** (`.vscode/mcp.json`)

```json
{ "servers": { "coopgames": { "type": "http", "url": "https://coopgames.app/mcp" } } }
```

Cualquier otro cliente que acepte servidores MCP remotos por HTTP funciona con la misma URL.

## Herramientas

| Herramienta | Para qué sirve |
|---|---|
| `search_games` | Buscar juegos para un grupo: jugadores (2–8), plataformas, online o misma pantalla, cooperativo o versus, género, crossplay, gratis, una copia para todos |
| `get_game` | Todo lo multijugador de un juego: plataformas, jugadores, crossplay entre cada par de plataformas, duración de la partida |
| `crossplay_check` | Sí o no rápido: ¿puede alguien en la plataforma A jugar este juego con alguien en la plataforma B? |

Plataformas: PC, PS5, PS4, Xbox, Switch y Switch 2. Cada resultado enlaza a la página del juego en CoopGames. Las respuestas vienen en inglés.

## Ejemplos

- «Somos cuatro para jugar esta noche: dos en PC, uno en PS5 y uno en Xbox. ¿Qué tiene crossplay?»
- «Juegos cooperativos gratis para 3 en Switch»
- «¿Puedo jugar Helldivers 2 con un amigo que está en Xbox si yo estoy en PS5?»
- «Juegos para dos en el sillón en PS5»

## Probarlo sin cliente

```bash
curl -s https://coopgames.app/mcp \
  -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_games","arguments":{"players":4,"platforms":["pc","ps5"],"crossplay":true,"limit":3}}}'
```

## Límites

- Solo lectura. Nunca escribe nada.
- Hay un límite de pedidos por IP. Si recibes `429`, espera un minuto.
- Si usas los datos, cita a CoopGames y enlaza la página del juego.

## Enlaces

- Sitio: [coopgames.app/es](https://coopgames.app/es)
- Todos los juegos: [coopgames.app/es/juegos](https://coopgames.app/es/juegos)

## Licencia

El texto y los ejemplos de este repositorio están bajo la [licencia MIT](LICENSE). Los datos del catálogo detrás del servidor son de CoopGames.
