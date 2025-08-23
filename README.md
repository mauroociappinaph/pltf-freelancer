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

Actualmente, estamos experimentando los siguientes problemas:

- **Generación de Aplicación Nx:** Al intentar generar la aplicación de NestJS (`backend`) con Nx, el comando falla con el error `Unable to resolve local plugin with import path @nrwl/nest`. A pesar de varios intentos de depuración, el problema persiste. Se ha intentado crear una issue en GitHub para su seguimiento, pero ha fallado debido a problemas de credenciales.
- **CI/CD - pnpm no encontrado:** El workflow de GitHub Actions falla al no poder localizar `pnpm`. Se ha implementado un fix para instalar `pnpm` globalmente en el workflow, pero aún no se ha verificado su solución en un nuevo PR.
- **Credenciales de GitHub para el Agente:** La creación automática de issues en GitHub por parte del agente está fallando debido a problemas de credenciales ("Bad credentials"). Se ha actualizado el token en `.gemini/settings.json` con uno nuevo que tiene el scope `repo`, pero el problema persiste. Se requiere una verificación adicional de la configuración del token y sus permisos, y posiblemente reiniciar el CLI de Gemini.

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

Este proyecto está siendo desarrollado con la asistencia de un agente de IA (Gemini CLI). Para entender cómo interactuar con el agente y el flujo de trabajo de desarrollo, consulta el archivo `planning/AGENT_WORKFLOW.md`. Se ha mejorado el workflow para incluir la creación automática de issues en GitHub para fallos en CI/CD y problemas irresolubles del agente, así como el seguimiento de su resolución.

## Configuración del Token de GitHub para el Agente

El token de GitHub para la interacción del agente con la API de GitHub ha sido configurado en `.gemini/settings.json`.

## Actualizaciones Recientes del Agente

Aquí se resumen las acciones y mejoras realizadas recientemente por el agente de IA:

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
