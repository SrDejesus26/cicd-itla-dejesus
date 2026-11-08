# Plantilla DevOps: Lista de tareas con CI/CD (ITLA)

Práctica 3 de Electiva 1: Introducción a DevOps. Aplicación web (Node.js/Express) con un pipeline CI/CD en GitHub Actions.

- Repositorio: https://github.com/SrDejesus26/cicd-itla-dejesus
- Página publicada: https://srdejesus26.github.io/cicd-itla-dejesus/

## Estructura
| Pieza | Archivo | Función |
|---|---|---|
| API | `src/app.js`, `src/server.js` | Tareas (GET, POST, PATCH, DELETE), `/health` y `/metrics` |
| Frontend | `public/index.html` | Se publica en GitHub Pages |
| Pruebas | `tests/app.test.js` | Jest + Supertest con cobertura |
| Contenedor | `Dockerfile` | Imagen de producción |
| Pipeline | `.github/workflows/ci.yml` | Lint, pruebas, build Docker y despliegue |

## Ejecutar localmente
```bash
npm install
npm test
npm start    # http://localhost:3000
```

## Endpoints
`GET /health`, `GET /metrics`, `GET /api/tareas`, `POST /api/tareas`, `PATCH /api/tareas/:id`, `DELETE /api/tareas/:id`

## Pipeline CI/CD
Se ejecuta en cada push y pull request hacia `main`.

**Job 1: Build y pruebas**
1. **Checkout:** descarga el código del repositorio.
2. **Setup Node 20:** instala Node.js.
3. **npm install:** instala dependencias.
4. **Revisión estática (lint):** verifica la sintaxis de `app.js` y `server.js`.
5. **Pruebas con cobertura:** ejecuta Jest; si una prueba falla, el pipeline se detiene.
6. **Build Docker:** construye la imagen para validar que el `Dockerfile` funciona.

**Job 2: Despliegue a GitHub Pages**
Solo corre en push a `main` y si el Job 1 pasó. Publica la carpeta `public` en GitHub Pages.

## Mejoras de la Práctica 3
- Nuevo endpoint `DELETE /api/tareas/:id`.
- Validación de títulos de más de 100 caracteres.
- Contador de ids para evitar ids repetidos tras borrar.
- 4 pruebas nuevas (10 en total, cobertura de 95.83%).
- Demostración de pipeline en rojo (prueba fallida) y luego en verde.

## Despliegue
1. Crear un repositorio público en GitHub y subir el código a `main`.
2. En Settings → Pages, elegir Source: **GitHub Actions**.
3. Hacer push: el workflow publica el sitio automáticamente.

## Docker
```bash
docker build -t tareas-devops .
docker run -p 3000:3000 tareas-devops
```

## Autor
Wandel De Jesus, matrícula 2025-2056. Electiva 1, ITLA.