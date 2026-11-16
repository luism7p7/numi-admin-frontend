# Numi · Panel administrativo · Frontend

Frontend del panel administrativo de **Numi**, la app educativa para niños de 1° a 5° de las instituciones
rurales de Medellín. Aquí el equipo de la Secretaría arma y publica actividades, sube recursos, gestiona
instituciones y usuarios y revisa el monitoreo técnico.

- **Tecnologías:** HTML, CSS, Bootstrap 5 y JavaScript (`fetch`).
- **Backend:** [numi-admin-backend](https://github.com/luism7p7/numi-admin-backend) (Flask + MySQL).
- **En producción:** https://numi-g01.northcentralus.cloudapp.azure.com

## Cómo se conecta con el backend

`js/app.js` llama a la API con rutas relativas (`/api/...`), así que el frontend y el backend se publican
detrás del mismo dominio. En la VM de Azure, **Nginx** entrega estos archivos y manda `/api/` y `/uploads/`
al backend. Antes de entregar una página privada, Nginx le pregunta al backend si hay sesión
(`GET /api/sesion`); si no la hay, lleva a `index.html`. Abrir el login cierra la sesión (`POST /api/logout`).

| Página | Qué hace |
|--------|----------|
| index.html / crear-usuario.html | Login y solicitud de cuenta (públicas) |
| inicio.html | Resumen general |
| actividades.html, actividad-detalle.html, borradores.html, constructor.html, historial.html | Actividades |
| recursos.html | Imágenes, audios y videos |
| instituciones.html, institucion-nueva.html | Instituciones |
| usuarios.html | Cuentas de docentes |
| monitoreo.html | Estado del backend de la app e informes |

## Probarlo en local

Clona este repositorio al lado de `numi-admin-backend` y sigue el README del backend: la forma más simple
es levantar todo con `despliegue/compose.yaml`. Abrir los .html con Live Server no sirve, porque sin la API
no cargan los datos.

## Equipo

- Luis Miguel Muñoz Rendón
- Alexander Mejía Ospina
- Santiago Mayorga Hueso
- Santiago Rodríguez Jiménez

Proyecto Numi · Universidad Cooperativa de Colombia, sede Medellín.
