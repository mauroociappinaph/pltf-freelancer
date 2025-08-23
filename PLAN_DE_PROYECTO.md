PLAN DE PROYECTO: Plataforma Inteligente para el Reclutamiento Óptimo de Personal Freelance

1. Resumen de los Objetivos del Proyecto

El objetivo principal es desarrollar una plataforma web innovadora que optimice el proceso de reclutamiento de talento freelance, utilizando inteligencia artificial para conectar de manera eficiente a reclutadores y freelancers. La plataforma busca resolver las frustraciones comunes de ambos grupos (opacidad, ineficiencia, falta de feedback, seguridad) y capitalizar las tendencias del mercado (digitalización, IA, revalorización de habilidades blandas).

Roles de Usuario Principales:
• Freelancer (Candidato): Busca proyectos, gestiona perfil, realiza pruebas, recibe feedback.
• Recruiter (Empresa): Publica ofertas, gestiona procesos de selección, evalúa candidatos, crea pruebas.
• Administrador: Gestión general de la plataforma.

2. Propuesta de Stack Tecnológico

Basado en la necesidad de una plataforma moderna, escalable, robusta y con fuerte tipado para el desarrollo eficiente, se propone el siguiente stack tecnológico:
• Arquitectura: Monorepo (con Nx)
• Frontend:
• Framework: Next.js (React)
• Lenguaje: TypeScript
• Estilos: Tailwind CSS (para desarrollo rápido y escalable)
• Gestión de Estado: Zustand (para gestión de datos con el backend)
• Librerías Clave:
• Axios: Cliente HTTP para peticiones a la API.
• React Query (TanStack Query): Gestión de datos asíncronos (fetching, caching).
• React Hook Form: Gestión y validación de formularios.
• Shadcn/ui: Componentes de UI reutilizables y personalizables.
• date-fns / Day.js: Manejo y formateo de fechas.
• Backend:
• Framework: NestJS (Node.js)
• Lenguaje: TypeScript
• Base de Datos: MongoDB (flexible, escalable y fácil de configurar para desarrollo)
• ORM: Prisma ORM (excelente integración con TypeScript y soporte para MongoDB)
• Autenticación: JWT (JSON Web Tokens) - Considerar Clerk como alternativa/complemento para simplificar la gestión de usuarios.
• Librerías Clave:
• Zod: Validación de esquemas y tipos.
• Winston / Pino: Logging estructurado.
• dotenv: Gestión de variables de entorno.
• Orquestación IA (Microservicio):
• Framework: Python con FastAPI
• Librerías Clave:
• (Se definirán según los modelos de IA específicos, ej. librerías de NLP, ML).
• Infraestructura (Desarrollo/Despliegue):
• Contenedores: Docker y Docker Compose (para entornos de desarrollo consistentes y despliegue simplificado).
• Control de Versiones: Git
• Herramientas de Calidad de Código:
• ESLint: Para análisis estático de código y detección de errores.
• Prettier: Para formateo automático de código y consistencia de estilo.
• MCPs (Multi-Cloud Platforms) a Considerar:
• Playwright: Para pruebas end-to-end automatizadas.
• Firecrawl: Potencialmente para web scraping de ofertas de empleo.
• context7 (@upstash/context7-mcp): Para caching, gestión de sesiones o datos en tiempo real.

Justificación del Stack:
• Monorepo (Nx): Permite compartir código y tipos de forma eficiente entre frontend, backend y microservicio de IA, garantizando consistencia y simplificando la refactorización.
• TypeScript End-to-End: Proporciona seguridad de tipo, mejora la mantenibilidad y reduce errores en proyectos grandes.
• Next.js: Ofrece renderizado del lado del servidor (SSR), generación de sitios estáticos (SSG) y optimizaciones de rendimiento, ideal para SEO y UX.
• NestJS: Framework robusto y modular para Node.js, basado en principios de arquitectura sólida (OOP, DI), ideal para aplicaciones empresariales.
• MongoDB & Prisma: Combinación potente para una base de datos NoSQL flexible con un ORM moderno que facilita el desarrollo y la sincronización de esquemas.
• Python/FastAPI para IA: Python es el estándar de la industria para IA/ML, y FastAPI permite construir APIs de alto rendimiento para el microservicio de IA.
• Docker: Asegura que el entorno de desarrollo sea idéntico al de producción, eliminando problemas de “funciona en mi máquina”.
• Principios de Código: El desarrollo se guiará por principios de buenas prácticas de código como DRY (Don’t Repeat Yourself) y SRP (Single Responsibility Principle), y se utilizarán patrones de organización como los ‘barrel files’ para mantener un código limpio y mantenible. **La integración de ESLint y Prettier asegurará la aplicación consistente de estos estándares.**
• Librerías Externas: Aprovechamiento del ecosistema para acelerar el desarrollo, mejorar la calidad y la robustez de la aplicación.

## 2.1. Control de Versiones

Todo el proyecto (esta carpeta) será gestionado y versionado en el siguiente repositorio de GitHub:

- **Repositorio GitHub:** [https://github.com/mauroociappinaph/pltf-freelancer.git](https://github.com/mauroociappinaph/pltf-freelancer.git)

Se recomienda realizar commits frecuentes y descriptivos, siguiendo las buenas prácticas de Git.

## 3. Desglose de Fases del Proyecto

Se propone un enfoque iterativo, comenzando con un MVP (Producto Mínimo Viable) y luego añadiendo funcionalidades.

### 3.1. Sugerencia Estratégica de Ejecución: Foco en el Camino Crítico del MVP

**Aportación del Agente IA:** Para maximizar el impacto y la velocidad de validación del MVP, se sugiere enfocar todos los esfuerzos iniciales de desarrollo en el **"camino crítico"** de la plataforma. Este flujo representa la interacción mínima indispensable que demuestra el valor del producto:

1.  **Flujo del Reclutador:** Un reclutador puede registrarse, crear una oferta de trabajo y asociarle un test técnico.
2.  **Flujo del Freelancer:** Un freelancer puede registrarse, encontrar la oferta, postularse y completar el test técnico de forma automatizada.
3.  **Cierre del Bucle:** El reclutador puede ver al freelancer postulante en su lista, clasificado según el resultado del test.

La recomendación es ejecutar estas tres funcionalidades de manera prioritaria, dejando características secundarias (como dashboards complejos, notificaciones avanzadas, etc.) para iteraciones posteriores, tal como lo enmarca el espíritu de este plan.

### 3.2. Fases del Proyecto

Fase 1: Configuración Inicial y Backend del MVP
• Objetivo: Establecer la infraestructura básica, la estructura de monorepo y desarrollar la API del backend con las funcionalidades mínimas para usuarios, perfiles, ofertas y pruebas.
• Tareas Clave:
• Configuración del entorno de desarrollo (Docker, Node.js, MongoDB) y la estructura de monorepo con Nx.
• Configuración de Calidad de Código Automatizada con Husky (pre-commit hooks).
• Inicialización de los proyectos backend (NestJS), frontend (Next.js) y ia-microservice (FastAPI) dentro del monorepo Nx.
• Configuración de Prisma ORM y el esquema para los modelos de datos esenciales (User, FreelancerProfile, RecruiterProfile, JobPosting, Test, Question, Application, TestAttempt).
• Implementación de módulos de autenticación (registro, login, JWT).
• Desarrollo de APIs CRUD para User, FreelancerProfile, RecruiterProfile.
• Desarrollo de APIs CRUD para JobPosting (crear, listar, ver detalle, actualizar estado).
• Desarrollo de APIs para Test y Question (crear, añadir preguntas de opción múltiple).
• Implementación de la lógica de Application (postulación de freelancer a oferta).
• Implementación de la lógica de TestAttempt (realización y auto-evaluación de tests de opción múltiple).
• Pruebas unitarias e integración básicas para los endpoints del backend.

Fase 2: Frontend del MVP
• Objetivo: Desarrollar la interfaz de usuario para las funcionalidades del MVP, permitiendo la interacción completa de los roles de Freelancer y Recruiter.
• Tareas Clave:
• Desarrollo de componentes de autenticación (Login, Registro).
• Desarrollo de interfaces para la gestión de perfiles (Freelancer y Recruiter).
• Desarrollo de interfaces para la gestión de ofertas de empleo (crear, listar, ver detalle, aplicar).
• Desarrollo de interfaces para la creación y gestión de pruebas técnicas.
• Desarrollo de la interfaz para la realización de tests por parte del freelancer.
• Desarrollo de la interfaz para que el reclutador vea las aplicaciones y el ranking básico.
• Integración del frontend con las APIs del backend.

Fase 3: Integración del Microservicio de IA (MVP)
• Objetivo: Desarrollar el microservicio de IA para el matching básico y la clasificación de candidatos, integrándolo con el backend principal.
• Tareas Clave:
• Desarrollo de un endpoint en FastAPI para recibir una oferta de trabajo y devolver un ranking de freelancers (matching básico por habilidades).
• Implementación de un algoritmo de matching simple (ej. basado en similitud de texto de habilidades).
• Integración del microservicio de IA con el backend de NestJS (llamadas HTTP).
• Ajuste de la lógica de ranking en el backend para usar los resultados del microservicio de IA.

Fases Futuras (Post-MVP):
• IA Avanzada: Implementación de “genoma profesional”, evaluación de habilidades blandas, feedback generativo.
• Funcionalidades Adicionales: Chat en tiempo real, notificaciones avanzadas, sistemas de pago, gestión de proyectos post-contratación.
• Escalabilidad y Optimización: Mejoras de rendimiento, monitoreo, despliegue en producción.

4. Primeras Tareas Concretas (Fase 1 - Setup y Backend MVP)

Para comenzar de inmediato, las primeras tareas se centrarán en establecer el entorno y la base del backend: 1. Configuración del Entorno de Desarrollo con Docker Compose y Monorepo Nx:
• Crear un archivo docker-compose.yml para orquestar los servicios de MongoDB, NestJS y FastAPI.
• Inicializar el monorepo con Nx y generar las aplicaciones backend (NestJS), frontend (Next.js) y ia-microservice (FastAPI) dentro de él.
• Configurar los Dockerfiles para las aplicaciones NestJS y FastAPI. 2. Configuración de Prisma ORM:
• Configurar la conexión a la base de datos MongoDB a través de Prisma en el proyecto backend. 3. Definición del Esquema de Prisma (Schema.prisma):
• Traducir los modelos de datos esenciales definidos en el “Prompt Técnico: MVP” a un esquema schema.prisma completo.
• Ejecutar el comando de Prisma para sincronizar el esquema con la base de datos.

¿Estás de acuerdo con este plan actualizado? Si es así, podemos empezar con la primera tarea: Configuración del Entorno de Desarrollo con Docker Compose y Monorepo Nx.

## 5. Metodología de Gestión de Proyecto con Linear

Para optimizar el desarrollo y la gestión de este proyecto, se utilizará una metodología ágil basada en Kanban, gestionada enteramente a través de la herramienta **Linear**. Esto formaliza los escenarios descritos en `WORKFLOW.md` en un sistema de seguimiento claro y accionable.

### 5.1. Estructura y Jerarquía

1.  **Proyecto en Linear:** Se creará un único proyecto en Linear llamado **"Plataforma de Reclutamiento IA"** que contendrá todo el trabajo.

2.  **Epics (Épicas):** Las **Fases** de este plan (ej. "Fase 1: Configuración y Backend del MVP", "Fase 2: Frontend del MVP") se crearán como **Proyectos** o **Marcos de tiempo** dentro de Linear. Esto nos permitirá agrupar las tareas y visualizar el progreso de cada gran bloque de trabajo.

3.  **Issues (Tareas):** Cada una de las **"Tareas Clave"** listadas en las fases de este documento se creará como un `issue` individual en Linear. Los bugs, mejoras o tareas de investigación también se registrarán como issues.
    *   **Herramienta clave:** `create_issue`

### 5.2. Organización con Etiquetas (Labels)

Se utilizará un sistema de etiquetas para categorizar y filtrar tareas eficientemente. El set inicial de etiquetas será:

*   **Área:** `area:backend`, `area:frontend`, `area:ia-service`, `area:devops`
*   **Tipo:** `type:feature`, `type:bug`, `type:chore`, `type:docs`
*   **Prioridad:** `priority:high`, `priority:medium`, `priority:low`

### 5.3. Flujo de Trabajo (Workflow)

Los issues seguirán un flujo de trabajo Kanban simple para visualizar el progreso:

1.  **Backlog:** Todas las ideas y tareas futuras.
2.  **Todo:** Tareas priorizadas y listas para ser trabajadas en el ciclo actual.
3.  **In Progress:** La tarea que se está trabajando activamente.
4.  **Done:** Tareas completadas y verificadas.

    *   **Herramienta clave:** `update_issue` (para cambiar el estado).

### 5.4. Documentación de Decisiones

Las decisiones arquitectónicas importantes, resúmenes de investigaciones o cualquier conocimiento clave que deba persistir se registrará utilizando la funcionalidad de **Documentos** de Linear.

    *   **Herramienta clave:** `create_document`

Esta metodología nos proporcionará una visión clara del progreso, facilitará la priorización y asegurará que cada pieza de trabajo esté documentada y alineada con los objetivos del proyecto. Para ver ejemplos prácticos del día a día, se debe consultar el archivo `WORKFLOW.md`.
