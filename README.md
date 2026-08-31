# BOT-BASE

Plantilla base para bots conversacionales de TECHDI. Sin info de ningún
cliente — se duplica esta carpeta para arrancar un bot nuevo.

Integra WhatsApp Business, Instagram y Claude AI para atender leads
(preventa) y clientes existentes (soporte pre/post-venta) por un mismo
canal, con derivación a un equipo humano organizada en Áreas configurables
desde el panel de administración.

---

## Stack

- **Frontend**: React + Vite + CSS Modules
- **Backend**: Node.js (ESM) + Express
- **Database**: Firebase Firestore (proyecto compartido `pedidos-lett-2`, colecciones con prefijo `bot-base_`)
- **AI**: Claude API (Anthropic)
- **Mensajería**: Meta Cloud API (WhatsApp Business + Instagram)

## Estructura

```
BOT-BASE/
├── client/           # Dashboard admin (React)
│   └── src/
│       ├── components/
│       ├── pages/
│       ├── hooks/
│       ├── contexts/
│       ├── lib/
│       └── styles/
└── server/           # API + Webhook handler (Node/Express)
    └── src/
        ├── routes/
        ├── services/
        └── middleware/
```

## Cómo duplicar esto para un cliente nuevo

1. Copiar la carpeta entera con otro nombre: `BOT-<CLIENTE>`.
2. `git init` fresco adentro (no arrastrar historia de BOT-BASE).
3. Reemplazar el prefijo de colección `bot-base_` por `bot-<cliente>_` en
   todo `server/` (grep rápido: `grep -rl "bot-base_" server | xargs sed -i 's/bot-base_/bot-<cliente>_/g'`).
4. Reemplazar el placeholder de marca `Tu Negocio` por el nombre real en:
   `client/src/components/Layout/Layout.jsx`, `Login.jsx`,
   `client/src/hooks/useNotifications.js`, `client/index.html`.
5. Completar `server/.env` y `client/.env` a partir de sus `.env.example`
   con credenciales **nuevas** para ese cliente (WhatsApp/Instagram/Firebase
   config del front — nunca reusar las de otro bot).
6. `ADMIN_EMAIL` / `ADMIN_NAME` / `ADMIN_PASSWORD` en `server/.env`: cuenta
   admin inicial del cliente.
7. Ajustar la personalidad y el mensaje de bienvenida desde la pantalla
   Config del panel (o los defaults en `server/src/routes/config.routes.js`).
8. Cargar la Knowledge Base real del cliente (arranca vacía a propósito).
9. Repo nuevo en GitHub, deploy nuevo (Railway backend + Vercel frontend),
   separado de cualquier otro bot.

## Cómo correr localmente

```bash
# Backend
cd server && npm install && npm run dev   # puerto 3001

# Frontend
cd client && npm install && npm run dev   # puerto 5173
```

Completá `server/.env` y `client/.env` a partir de sus `.env.example` antes de arrancar.
