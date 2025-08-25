Descripción General del Proyecto

Este proyecto tiene como objetivo desarrollar una plataforma inteligente para el reclutamiento óptimo de personal freelance. Se apoya en inteligencia artificial para conectar de manera eficiente a las empresas con candidatos freelance adecuados, resolviendo frustraciones comunes en el proceso de selección.

Tecnologías Clave:
• Monorepo: Nx
• Frontend: Next.js (React, TypeScript, Tailwind CSS)
• Backend: NestJS (Node.js, TypeScript, GraphQL)
• Microservicio de IA: FastAPI (Python, TensorFlow, Keras, scikit-learn)
• Base de Datos: MongoDB (con Prisma ORM)
• Contenerización: Docker
• Gestor de Paquetes: pnpm

Arquitectura:
El proyecto está estructurado como un monorepo utilizando Nx, separando las responsabilidades en una aplicación de frontend, una API backend y un microservicio de IA dedicado. Se utilizan librerías compartidas en estas aplicaciones para mantener consistencia.

Construcción y Ejecución

Para configurar y ejecutar el proyecto localmente, seguí estos pasos: 1. Clonar el repositorio:

    git clone https://github.com/mauroociappinaph/pltf-freelancer.git # Reemplazar con la URL real del repo si es diferente

cd pltf-freelancer

    2.	Instalar dependencias:

    pnpm install

    	3.	Configurar variables de entorno:

Creá un archivo .env en la raíz del proyecto basado en .env.example y configurá las variables necesarias (por ejemplo, DATABASE_URL). 4. Iniciar servicios Docker (ejemplo: MongoDB):

    docker compose up -d


    5.	Ejecutar migraciones de la base de datos (si aplica):

    # Este comando dependerá de la configuración del ORM en el backend (ejemplo: migraciones de Prisma)

# TODO: Agregar comando específico de migración una vez que el backend esté configurado.

6. Iniciar las aplicaciones:

pnpm nx serve frontend
pnpm nx serve backend

# TODO: Agregar comando para el microservicio de IA una vez que esté configurado.

Verificaciones del Proyecto

Para ejecutar todas las verificaciones de código (lint, chequeo de tipos, tests), utilizá el script verify-all:

pnpm verify-all

Convenciones de Desarrollo

Flujo de Trabajo con Git

El proyecto sigue un flujo de trabajo estructurado en Git con ramas master, develop, feat/<issue-id>-descriptive-name y hotfix/, para mantener un historial de cambios limpio y predecible.

Principios de Diseño de Código
• DRY (Don’t Repeat Yourself / No te repitas): Se enfatiza la representación única y autoritativa del conocimiento, utilizando tipos compartidos, lógica de negocio reutilizable y componentes de UI.
• SRP (Single Responsibility Principle / Principio de Responsabilidad Única): Garantiza que los módulos, clases y funciones tengan un único motivo de cambio, promoviendo servicios cohesionados y funciones enfocadas.
• Archivos Barrel: Se utilizan para organizar módulos y simplificar las declaraciones de importación, teniendo cuidado con las dependencias circulares y el tree-shaking.

Herramientas de Calidad de Código
• ESLint: Análisis estático para identificar patrones problemáticos, errores y problemas de estilo.
• Prettier: Formateador automático de código para un estilo consistente.
• Husky + lint-staged: Hooks de Git para asegurar que las verificaciones de calidad de código se ejecuten automáticamente antes de los commits.

Flujo de Interacción con el Agente

Para una guía detallada sobre cómo interactuar con el agente de IA Gemini y el flujo de desarrollo, consultá planning/AGENT_WORKFLOW.md y AGENT_INSTRUCTIONS.md.

Documentación Clave del Proyecto

Para una comprensión completa del proyecto y sus procesos, revisá los siguientes documentos importantes:
• CODING_GUIDELINES.md: Guías de codificación.
• IDE_SETUP_GUIDE.md: Guía de configuración del IDE.
• PLAN_DE_PROYECTO.md: Plan general del proyecto.
• RESUMEN_SESION_GEMINI.md: Resumen de sesiones previas con el agente Gemini.
• WORKFLOW.md: Descripción general del flujo de trabajo del proyecto.
• planning/AGENT_WORKFLOW.md: Flujo detallado de interacción con el agente de IA.
• planning/DESIGN_DOCUMENT.md: Documento de diseño del proyecto.
• planning/REQUIREMENTS.md: Documento de requisitos del proyecto.
• planning/TASK_PLAN.md: Plan de tareas detallado.
• AGENT_INSTRUCTIONS.md: Guía rápida de instrucciones para el agente.
