# Numi · Panel administrativo · Frontend

Frontend del Panel administrativo de **Numi**: la Secretaría arma y publica actividades, sube recursos, gestiona instituciones y usuarios y revisa el monitoreo técnico.

- **Backend:** [numi-api](https://github.com/luism7p7/numi-api)
- **En producción (Azure):** https://numi-g01.northcentralus.cloudapp.azure.com

| | |
|--|--|
| Tipo | SPA (una sola página, rutas con `#/`) |
| Tecnología | Vite 7, Bootstrap 5 y JavaScript (`fetch`) |
| Sesión | Token JWT que entrega `POST /api/v1/auth/login` y se envía en `Authorization: Bearer` |
| Servidor | Nginx (imagen Docker en dos etapas: Node compila, Nginx sirve `dist/`) |

## Estructura

```
src/js/
├── api/          # un archivo por recurso; http.js es el único cliente HTTP
├── auth/         # token y sesión
├── router/       # rutas y guards (piden sesión antes de abrir una pantalla privada)
├── components/   # barra lateral y componentes reutilizables
├── pages/        # una pantalla por archivo
└── utils/
```

La dirección de la API llega en la variable `VITE_API_URL` al compilar (ver `.env.example`).

## Probarlo en local

```powershell
npm install
npm run dev        # http://localhost:5173  (la API en http://localhost:5001/api/v1)
```

## Docker

```bash
docker build --build-arg VITE_API_URL=https://numi-g01.northcentralus.cloudapp.azure.com/api/v1 -t numi-admin-frontend .
```

En la VM de Azure se levanta con `numi-api/despliegue/compose.yaml`: Nginx entrega la SPA y reenvía `/api/` al
backend por la red interna de Docker, con HTTPS de Let's Encrypt.

## Equipo

- Luis Miguel Muñoz Rendón
- Alexander Mejía Ospina
- Santiago Mayorga Hueso
- Santiago Rodríguez Jiménez

Proyecto Numi · Universidad Cooperativa de Colombia, sede Medellín.
