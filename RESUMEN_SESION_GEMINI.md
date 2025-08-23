# RESUMEN DE LA SESIÓN GEMINI: Planificación Inicial del Proyecto

**Fecha del Resumen:** 22 de agosto de 2025

---

## 1. Objetivo General del Proyecto

Desarrollar una **Plataforma Inteligente para el Reclutamiento Óptimo de Personal Freelance**. Esta plataforma web busca optimizar la conexión entre reclutadores y freelancers, utilizando inteligencia artificial para resolver frustraciones comunes (opacidad, ineficiencia, falta de feedback, seguridad) y capitalizar las tendencias del mercado (digitalización, IA, revalorización de habilidades blandas).

---

## 2. Decisiones Clave Tomadas y Justificación

Hemos definido la base arquitectónica y tecnológica del proyecto:

*   **Arquitectura:** **Monorepo con Nx**.
    *   **Justificación:** Permite compartir código y tipos de forma eficiente entre frontend, backend y microservicio de IA, garantizando consistencia y simplificando la refactorización.
*   **Base de Datos:** **MongoDB** con **Prisma ORM**.
    *   **Justificación:** Facilidad de configuración para desarrollo y escalabilidad a producción sin necesidad de migración de tecnología. Prisma ofrece excelente integración con TypeScript y soporte para MongoDB.
*   **Stack Tecnológico Principal:**
    *   **Frontend:** Next.js (React) con TypeScript, Tailwind CSS, Zustand.
    *   **Backend:** NestJS (Node.js) con TypeScript.
    *   **Orquestación IA (Microservicio):** Python con FastAPI.
    *   **Infraestructura:** Docker y Docker Compose.
    *   **Justificación:** TypeScript end-to-end para seguridad de tipo, frameworks robustos y populares, y Docker para entornos consistentes.
*   **Principios de Codificación:** Adherencia a **DRY** (Don't Repeat Yourself), **SRP** (Single Responsibility Principle) y uso de **Barrel Files**.
    *   **Justificación:** Fomentan un código mantenible, escalable, legible y robusto.
*   **Herramientas de Calidad de Código:** **ESLint** (linter) y **Prettier** (formateador).
    *   **Justificación:** Aseguran consistencia del código, detección temprana de errores y cumplimiento de directrices de estilo.
*   **Prácticas de Desarrollo y Calidad:**
    *   Pruebas Tempranas y Continuas.
    *   Manejo de Errores y Logging Centralizado.
    *   Mejores Prácticas de Seguridad (cifrado, validación, JWT).
    *   Documentación de la API (Swagger/OpenAPI).
    *   CI/CD desde el Inicio (simple).
    *   Monitoreo de Rendimiento y Bucle de Retroalimentación del Usuario.
    *   **Justificación:** Cruciales para la robustez, estabilidad y mantenibilidad del proyecto.
*   **Librerías Externas Clave (Adicionales al Stack Principal):**
    *   **Frontend:** Axios, React Query, React Hook Form, Shadcn/ui, date-fns/Day.js.
    *   **Backend:** Zod, Winston/Pino, dotenv, Clerk (opcional/considerar).
    *   **Justificación:** Aceleran el desarrollo, mejoran la calidad y la robustez.
*   **MCPs (Multi-Cloud Platforms) a Considerar:**
    *   **Playwright:** Para pruebas end-to-end automatizadas.
    *   **Firecrawl:** Potencialmente para web scraping de ofertas de empleo.
    *   **context7 (@upstash/context7-mcp):** Para caching, gestión de sesiones o datos en tiempo real.
    *   **Justificación:** Potencian las capacidades de la plataforma.
*   **Organización de Carpetas:**
    *   **Mantener:** `data/` (integrar contenido en esquema), `design/`, `docs/`.
    *   **Eliminar:** `archives/`.
    *   **Justificación:** Mantener activos relevantes y documentación, eliminar redundancia.

---

## 3. Documentos Actualizados y Creados

Hemos generado y/o actualizado los siguientes archivos para documentar el proyecto y nuestras decisiones:

*   `PLAN_DE_PROYECTO.md` (Plan general del proyecto, stack, fases, tareas).
*   `CODING_GUIDELINES.md` (Principios de codificación, herramientas de calidad, prácticas de desarrollo, librerías, MCPs).
*   `resumen_del_proyecto.txt` (Resumen ejecutivo del proyecto).
*   `mapa-de-empatia.txt` (Análisis de frustraciones y deseos de usuarios).
*   `informe-de-tendencias.txt` (Análisis de tendencias del mercado de reclutamiento).
*   `CRUCE DE TENDENCIAS Y MAPA DE EMPATIA.txt` (Cruce de tendencias y mapa de empatía, identificando oportunidades).
*   `Funcionalidades Claves.txt` (Funcionalidades clave propuestas para la plataforma).
*   `Prompt Técnico: MVP.txt` (Especificación técnica detallada para el MVP).

---

## 4. Mi Función como Agente Orquestador

Mi rol es guiar el proceso de desarrollo, actuando como tu asistente principal. Me encargaré de:
*   Descomponer tareas complejas en pasos manejables.
*   Generar código y configuraciones.
*   Ejecutar comandos en la terminal.
*   Asegurar que el desarrollo siga las directrices y el plan acordado.
*   Mantener la comunicación clara y documentar el progreso.

---

## 5. Próximo Paso a Realizar (Lo que falta hacer)

El siguiente paso concreto, según nuestro `PLAN_DE_PROYECTO.md`, es iniciar la **Fase 1: Configuración Inicial y Backend del MVP**.

La primera tarea específica es:

**1. Configuración del Entorno de Desarrollo con Docker Compose y Monorepo Nx:**
    *   Crear un archivo `docker-compose.yml` para orquestar los servicios de MongoDB, NestJS y FastAPI.
    *   Inicializar el monorepo con Nx y generar las aplicaciones `backend` (NestJS), `frontend` (Next.js) y `ia-microservice` (FastAPI) dentro de él.
    *   Configurar los `Dockerfile`s para las aplicaciones NestJS y FastAPI.

---

Este resumen te proporcionará una visión rápida de todo lo que hemos logrado y lo que sigue.

¿Estás listo para que empecemos con la primera tarea concreta?

---

# Resumen de la Sesión - 22/08/2025: Sistema de Prompts para Desarrollo

**Tema**: Análisis e implementación de un sistema de prompts para mejorar la productividad durante el desarrollo del proyecto.

**Discusión Inicial**:
*   Se inició con la propuesta de usar un sistema de Prompts basado en el Model Context Protocol (MCP).
*   La primera recomendación se enfocó en implementar este sistema como una característica para el usuario final de la plataforma (ej. reclutadores).

**Punto de Inflexión y Aclaración Clave**:
*   Se aclaró que el objetivo real era utilizar este sistema como una **herramienta de productividad interna para el desarrollador**, no como una función del producto.

**Estrategia y Acciones Implementadas**:
*   Se reenfocó la recomendación para crear un conjunto de herramientas personales que automaticen tareas de desarrollo repetitivas.
*   Se propusieron ejemplos de comandos para el desarrollador, como `/crear_componente_react` o `/generar_test_jest`.
*   Se tomó la decisión de organizar este sistema de la siguiente manera:
    1.  **Se creó un nuevo directorio `dev_prompts/`** en la raíz del proyecto para almacenar los archivos de plantilla de los prompts.
    2.  **Se añadió una plantilla de ejemplo**: `dev_prompts/react_component.prompt` para demostrar el concepto.
    3.  **Se actualizó el archivo `CODING_GUIDELINES.md`** para documentar este nuevo sistema de desarrollo interno, su propósito y cómo utilizarlo.

**Resultado**:
El proyecto ahora cuenta con una estructura base para un sistema de prompts de desarrollo, diseñado para acelerar la creación de código, pruebas y otros artefactos de software de manera consistente.
