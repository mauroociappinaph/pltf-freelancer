# Plataforma Inteligente para el Reclutamiento Óptimo de Personal Freelance

Este es el repositorio del proyecto "Plataforma Inteligente para el Reclutamiento Óptimo de Personal Freelance".

## Resumen del Proyecto

[Aquí irá un resumen detallado del proyecto, sus objetivos y funcionalidades clave.]

## Estado Actual del Proyecto

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

## Problemas Conocidos

Actualmente, estamos experimentando un problema al intentar generar la aplicación de NestJS (`backend`) con Nx. El error es `Unable to resolve local plugin with import path @nrwl/nest`. Se ha creado una issue en GitHub para su seguimiento.

## Configuración del Entorno de Desarrollo

### Docker Compose

Para levantar los servicios de desarrollo (como MongoDB), puedes usar Docker Compose:

```bash
docker compose up -d
```

### Verificaciones del Proyecto

Para ejecutar todas las verificaciones de código (lint, type check, tests), puedes usar el script `verify-all`:

```bash
pnpm verify-all
```

## Interacción con el Agente Gemini

Este proyecto está siendo desarrollado con la asistencia de un agente de IA (Gemini CLI). Para entender cómo interactuar con el agente y el flujo de trabajo de desarrollo, consulta el archivo `planning/AGENT_WORKFLOW.md`.

## Configuración del Token de GitHub para el Agente

El token de GitHub para la interacción del agente con la API de GitHub ha sido configurado en `.gemini/settings.json`.
