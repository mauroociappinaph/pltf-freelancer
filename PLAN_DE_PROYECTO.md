PLAN DE PROYECTO: Plataforma Inteligente para el Reclutamiento Óptimo de Personal Freelance

1. Resumen de los Objetivos del Proyecto

El objetivo principal es desarrollar una plataforma web innovadora que optimice el proceso de reclutamiento de talento freelance, utilizando inteligencia artificial para conectar de manera eficiente a reclutadores y freelancers. La plataforma busca resolver las frustraciones comunes de ambos grupos (opacidad, ineficiencia, falta de feedback, seguridad) y capitalizar las tendencias del mercado (digitalización, IA, revalorización de habilidades blandas).

Roles de Usuario Principales:
	•	Freelancer (Candidato): Busca proyectos, gestiona perfil, realiza pruebas, recibe feedback.
	•	Recruiter (Empresa): Publica ofertas, gestiona procesos de selección, evalúa candidatos, crea pruebas.
	•	Administrador: Gestión general de la plataforma.

2. Propuesta de Stack Tecnológico

Basado en la necesidad de una plataforma moderna, escalable, robusta y con fuerte tipado para el desarrollo eficiente, se propone el siguiente stack tecnológico:
	•	Arquitectura: Monorepo (con Nx)
	•	Frontend:
	•	Framework: Next.js (React)
	•	Lenguaje: TypeScript
	•	Estilos: Tailwind CSS (para desarrollo rápido y escalable)
	•	Gestión de Estado: Zustand (para gestión de datos con el backend)
	•	Librerías Clave:
	•	Axios: Cliente HTTP para peticiones a la API.
	•	React Query (TanStack Query): Gestión de datos asíncronos (fetching, caching).
	•	React Hook Form: Gestión y validación de formularios.
	•	Shadcn/ui: Componentes de UI reutilizables y personalizables.
	•	date-fns / Day.js: Manejo y formateo de fechas.
	•	Backend:
	•	Framework: NestJS (Node.js)
	•	Lenguaje: TypeScript
	•	Base de Datos: MongoDB (flexible, escalable y fácil de configurar para desarrollo)
	•	ORM: Prisma ORM (excelente integración con TypeScript y soporte para MongoDB)
	•	Autenticación: JWT (JSON Web Tokens) - Considerar Clerk como alternativa/complemento para simplificar la gestión de usuarios.
	•	Librerías Clave:
	•	Zod: Validación de esquemas y tipos.
	•	Winston / Pino: Logging estructurado.
	•	dotenv: Gestión de variables de entorno.
	•	Orquestación IA (Microservicio):
	•	Framework: Python con FastAPI
	•	Librerías Clave:
	•	(Se definirán según los modelos de IA específicos, ej. librerías de NLP, ML).
	•	Infraestructura (Desarrollo/Despliegue):
	•	Contenedores: Docker y Docker Compose (para entornos de desarrollo consistentes y despliegue simplificado).
	•	Control de Versiones: Git
	•	Herramientas de Calidad de Código:
	•	ESLint: Para análisis estático de código y detección de errores.
	•	Prettier: Para formateo automático de código y consistencia de estilo.
	•	MCPs (Multi-Cloud Platforms) a Considerar:
	•	Playwright: Para pruebas end-to-end automatizadas.
	•	Firecrawl: Potencialmente para web scraping de ofertas de empleo.
	•	context7 (@upstash/context7-mcp): Para caching, gestión de sesiones o datos en tiempo real.

Justificación del Stack:
	•	Monorepo (Nx): Permite compartir código y tipos de forma eficiente entre frontend, backend y microservicio de IA, garantizando consistencia y simplificando la refactorización.
	•	TypeScript End-to-End: Proporciona seguridad de tipo, mejora la mantenibilidad y reduce errores en proyectos grandes.
	•	Next.js: Ofrece renderizado del lado del servidor (SSR), generación de sitios estáticos (SSG) y optimizaciones de rendimiento, ideal para SEO y UX.
	•	NestJS: Framework robusto y modular para Node.js, basado en principios de arquitectura sólida (OOP, DI), ideal para aplicaciones empresariales.
	•	MongoDB & Prisma: Combinación potente para una base de datos NoSQL flexible con un ORM moderno que facilita el desarrollo y la sincronización de esquemas.
	•	Python/FastAPI para IA: Python es el estándar de la industria para IA/ML, y FastAPI permite construir APIs de alto rendimiento para el microservicio de IA.
	•	Docker: Asegura que el entorno de desarrollo sea idéntico al de producción, eliminando problemas de “funciona en mi máquina”.
	•	Principios de Código: El desarrollo se guiará por principios de buenas prácticas de código como DRY (Don’t Repeat Yourself) y SRP (Single Responsibility Principle), y se utilizarán patrones de organización como los ‘barrel files’ para mantener un código limpio y mantenible. **La integración de ESLint y Prettier asegurará la aplicación consistente de estos estándares.**
	•	Librerías Externas: Aprovechamiento del ecosistema para acelerar el desarrollo, mejorar la calidad y la robustez de la aplicación.

## 2.1. Control de Versiones

Todo el proyecto (esta carpeta) será gestionado y versionado en el siguiente repositorio de GitHub:

*   **Repositorio GitHub:** [https://github.com/mauroociappinaph/pltf-freelancer.git](https://github.com/mauroociappinaph/pltf-freelancer.git)

Se recomienda realizar commits frecuentes y descriptivos, siguiendo las buenas prácticas de Git.

## 3. Desglose de Fases del Proyecto

Se propone un enfoque iterativo, comenzando con un MVP (Producto Mínimo Viable) y luego añadiendo funcionalidades.

Fase 1: Configuración Inicial y Backend del MVP
	•	Objetivo: Establecer la infraestructura básica, la estructura de monorepo y desarrollar la API del backend con las funcionalidades mínimas para usuarios, perfiles, ofertas y pruebas.
	•	Tareas Clave:
	•	Configuración del entorno de desarrollo (Docker, Node.js, MongoDB) y la estructura de monorepo con Nx.
	•	Inicialización de los proyectos backend (NestJS), frontend (Next.js) y ia-microservice (FastAPI) dentro del monorepo Nx.
	•	Configuración de Prisma ORM y el esquema para los modelos de datos esenciales (User, FreelancerProfile, RecruiterProfile, JobPosting, Test, Question, Application, TestAttempt).
	•	Implementación de módulos de autenticación (registro, login, JWT).
	•	Desarrollo de APIs CRUD para User, FreelancerProfile, RecruiterProfile.
	•	Desarrollo de APIs CRUD para JobPosting (crear, listar, ver detalle, actualizar estado).
	•	Desarrollo de APIs para Test y Question (crear, añadir preguntas de opción múltiple).
	•	Implementación de la lógica de Application (postulación de freelancer a oferta).
	•	Implementación de la lógica de TestAttempt (realización y auto-evaluación de tests de opción múltiple).
	•	Pruebas unitarias e integración básicas para los endpoints del backend.

Fase 2: Frontend del MVP
	•	Objetivo: Desarrollar la interfaz de usuario para las funcionalidades del MVP, permitiendo la interacción completa de los roles de Freelancer y Recruiter.
	•	Tareas Clave:
	•	Desarrollo de componentes de autenticación (Login, Registro).
	•	Desarrollo de interfaces para la gestión de perfiles (Freelancer y Recruiter).
	•	Desarrollo de interfaces para la gestión de ofertas de empleo (crear, listar, ver detalle, aplicar).
	•	Desarrollo de interfaces para la creación y gestión de pruebas técnicas.
	•	Desarrollo de la interfaz para la realización de tests por parte del freelancer.
	•	Desarrollo de la interfaz para que el reclutador vea las aplicaciones y el ranking básico.
	•	Integración del frontend con las APIs del backend.

Fase 3: Integración del Microservicio de IA (MVP)
	•	Objetivo: Desarrollar el microservicio de IA para el matching básico y la clasificación de candidatos, integrándolo con el backend principal.
	•	Tareas Clave:
	•	Desarrollo de un endpoint en FastAPI para recibir una oferta de trabajo y devolver un ranking de freelancers (matching básico por habilidades).
	•	Implementación de un algoritmo de matching simple (ej. basado en similitud de texto de habilidades).
	•	Integración del microservicio de IA con el backend de NestJS (llamadas HTTP).
	•	Ajuste de la lógica de ranking en el backend para usar los resultados del microservicio de IA.

Fases Futuras (Post-MVP):
	•	IA Avanzada: Implementación de “genoma profesional”, evaluación de habilidades blandas, feedback generativo.
	•	Funcionalidades Adicionales: Chat en tiempo real, notificaciones avanzadas, sistemas de pago, gestión de proyectos post-contratación.
	•	Escalabilidad y Optimización: Mejoras de rendimiento, monitoreo, despliegue en producción.

4. Primeras Tareas Concretas (Fase 1 - Setup y Backend MVP)

Para comenzar de inmediato, las primeras tareas se centrarán en establecer el entorno y la base del backend:
	1.	Configuración del Entorno de Desarrollo con Docker Compose y Monorepo Nx:
	•	Crear un archivo docker-compose.yml para orquestar los servicios de MongoDB, NestJS y FastAPI.
	•	Inicializar el monorepo con Nx y generar las aplicaciones backend (NestJS), frontend (Next.js) y ia-microservice (FastAPI) dentro de él.
	•	Configurar los Dockerfiles para las aplicaciones NestJS y FastAPI.
	2.	Configuración de Prisma ORM:
	•	Configurar la conexión a la base de datos MongoDB a través de Prisma en el proyecto backend.
	3.	Definición del Esquema de Prisma (Schema.prisma):
	•	Traducir los modelos de datos esenciales definidos en el “Prompt Técnico: MVP” a un esquema schema.prisma completo.
	•	Ejecutar el comando de Prisma para sincronizar el esquema con la base de datos.

¿Estás de acuerdo con este plan actualizado? Si es así, podemos empezar con la primera tarea: Configuración del Entorno de Desarrollo con Docker Compose y Monorepo Nx.

## 5. Flujo de Trabajo con Herramientas Integradas (MCP)

Para optimizar el desarrollo y la gestión de este proyecto, se utilizará el siguiente flujo de trabajo basado en las herramientas integradas disponibles a través de los servidores MCP:

1.  **Planifica (Linear):** Se definen y asignan todas las funcionalidades, historias de usuario y tareas del proyecto en Linear. Esto centraliza la planificación y el seguimiento del trabajo pendiente.
    -   **Herramientas clave:** `create_project`, `create_issue`.

2.  **Investiga (Firecrawl):** Se utilizan las herramientas de web scraping y búsqueda para recopilar datos relevantes del mercado, analizar competidores, identificar perfiles de empresas o freelancers y validar tendencias.
    -   **Herramientas clave:** `firecrawl_search`, `firecrawl_scrape`, `firecrawl_extract`.

3.  **Desarrolla (Context7):** Durante la fase de codificación, se consulta la documentación de librerías y frameworks directamente desde el CLI para agilizar la implementación y resolver dudas técnicas sin cambiar de contexto.
    -   **Herramientas clave:** `resolve-library-id`, `get-library-docs`.

4.  **Gestiona y Sincroniza (Linear):** El progreso se actualiza constantemente en Linear. Las tareas se mueven entre estados (ej. 'Por hacer', 'En progreso', 'Hecho'), y los bugs se reportan y se les da seguimiento en la misma plataforma.
    -   **Herramientas clave:** `update_issue`, `list_issues`.

*Para una guía detallada con escenarios prácticos sobre cómo aplicar este flujo en el día a día, consulta el archivo [WORKFLOW.md](./WORKFLOW.md).*