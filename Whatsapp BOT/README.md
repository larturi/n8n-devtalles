# Wahatsapp Bot (devtalles_n8n_bot)

## Resumen

Este proyecto usa n8n levantado localmente con Docker. Para que Whatsapp envíe actualizaciones a tu instancia local (webhooks) debes exponer n8n mediante una URL pública (por ejemplo usando ngrok). También debes crear un bot en Telegram con BotFather y usar su token para configurar el webhook.

> Nota de seguridad: el token del bot permite controlar el bot. No lo compartas ni lo publiques. Si crees que se filtró, revoca/regenera el token desde BotFather.

## Requisitos

- Docker y Docker Compose para levantar n8n
- ngrok (o cualquier herramienta que haga tunneling a localhost)
- Cuenta de Whatsapp Bussines (Meta)

## Pasos rápidos

1. Levantar n8n (desde la carpeta del repo):

```bash
cd "Whatsapp BOT/n8n-compose"
docker compose up -d
```

En esta configuración n8n está expuesto en localhost:5678 (el compose mapea 127.0.0.1:5678:5678).

2. Exponer n8n con ngrok (desde otra terminal):

```bash
ngrok http --url=nonspheral-unilludedly-melina.ngrok-free.dev 5678
```

ngrok te mostrará una URL pública del tipo `https://<tu-subdominio>.ngrok.io` (usa la URL HTTPS).

3. Crear el bot en Telegram (BotFather)

- En Telegram busca `@BotFather` y usa el comando `/newbot`.
- Te pedirá un nombre y un username (el username debe terminar en `bot`). Ejemplo usado en este repo:
  - Nombre: `devtalles-n8n-custombot`
  - Username: `devtalles_n8n_bot`
- BotFather te dará un token (algo así como `123456:ABC-DEF...`). Guarda ese token en un lugar seguro y úsalo en n8n o en llamadas a la API.
