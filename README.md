TechSolutions Web — Flujo Completo con CI/CD

Proyecto académico inspirado en un entorno profesional de desarrollo colaborativo.  
Creado por **CocaColita S.A.**, empresa dedicada a soluciones tecnológicas para la gestión de datos y visualización de información.

---

## Objetivo del Proyecto

Simular un entorno real de trabajo en equipo donde los desarrolladores:

- Configuran un **flujo Git profesional** con ramas `main`, `dev`, `release` y `feature/*`.
- Generan y resuelven **conflictos de código**.
- Gestionan tareas mediante un **tablero Kanban** en GitHub Projects.
- Implementan un **pipeline CI/CD** con GitHub Actions.
- Despliegan la aplicación en **Vercel** o **Netlify**.
- Documentan el proceso completo y los resultados finales.

---

## Estructura del Proyecto

techsolutions-web/
├── index.html
├── style.css
├── script.js
├── README.md
└── .github/workflows/deploy.yml

yaml

---

## Flujo de Trabajo

### 1 Configuración Inicial

- **Dev1** crea el repositorio y las ramas principales:  
  `main`, `dev`, `release`, `feature/*`.
- Primer commit con la estructura base del proyecto.

📸 *Evidencia:* Captura del repositorio con ramas y commit inicial.

---

### 2 Gestión del Proyecto (Kanban)

- Se crean **issues** por cada requerimiento funcional (RF1–RF6).  
- Cada desarrollador trabaja en su respectiva **feature branch**.
- Tablero con columnas: `To Do → In Progress → Review → Done`.

📸 *Evidencia:* Captura del tablero con tareas asignadas.

---

### 3 Desarrollo de Features y Conflictos

| RF | Desarrollador | Descripción |
|----|----------------|-------------|
| RF2 | Dev1 | Agrega campo **email** |
| RF3 | Dev2 | Agrega campo **age** (conflicto intencional) |
| RF1 + RF4 | Dev3 | Implementa función `showUsers()` con error `user → users` |

- Cada Dev hace commits claros y push a su rama.
- Se abren PRs hacia la rama `dev`.

📸 *Evidencia:* Capturas de commits y PRs abiertos.

---

### 4 Merge a `dev` y Resolución de Conflictos

- **Dev3** revisa todos los PRs y resuelve conflictos.
- Se corrige el error `user → users`.
- Merge completado exitosamente en `dev`.

📸 *Evidencia:* PR mergeado con conflicto resuelto.

---

### 5 Configuración del Pipeline CI/CD

Archivo: `.github/workflows/deploy.yml`

```yaml
name: CI/CD Deploy

on:
  push:
    branches:
      - release

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: echo "No tests yet"  # placeholder

      - name: Deploy to Vercel
        run: npx vercel --prod --token ${{ secrets.VERCEL_TOKEN }}
