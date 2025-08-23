Directrices de Codificación y Principios de Diseño

Este documento detalla los principios de diseño y las directrices de codificación que seguiremos en el desarrollo de la Plataforma Inteligente para el Reclutamiento Óptimo de Personal Freelance. Adherirse a estos principios nos ayudará a construir un código base mantenible, escalable, legible y robusto.

## 1. Flujo de Trabajo de Git (Git Workflow)

Para mantener un historial de cambios limpio, predecible y profesional, adoptaremos el siguiente modelo de ramas:

*   **`master`**: Esta rama es sagrada. Contiene la última versión estable y desplegable del proyecto. No se debe hacer `commit` directamente a `master`. El código solo llega a `master` a través de Pull Requests desde la rama `develop`.
*   **`develop`**: Es la rama principal de integración. Contiene las últimas funcionalidades desarrolladas que están listas para ser incluidas en la próxima versión estable. Es la rama base para todo el nuevo desarrollo.
*   **`feat/<issue-id>-nombre-descriptivo`**: Para cada nueva funcionalidad o corrección de bug planificada, se creará una rama a partir de `develop`. El nombre debe incluir el ID de la tarea de Linear (ej. `EVAL-123`) para conectar el código con la planificación.
    *   *Ejemplo de feature:* `feat/EVAL-123-user-authentication`
    *   *Ejemplo de bug fix:* `feat/EVAL-124-fix-login-button`
*   **`hotfix/<nombre-del-parche>`**: Exclusivamente para correcciones críticas y urgentes en producción. Se crea a partir de `master` y, una vez finalizado, debe fusionarse tanto en `master` como en `develop`.

Este flujo de trabajo aísla el desarrollo en progreso, mantiene la rama `master` siempre estable y facilita la revisión de código a través de Pull Requests.

## 2. Principios de Diseño de Código

### 2.1. DRY (Don’t Repeat Yourself - No te Repitas)

Principio: Cada pieza de conocimiento debe tener una representación única, inequívoca y autorizada dentro del sistema.

Aplicación en el Proyecto:
	•	Tipos e Interfaces Compartidos: Definiremos modelos de datos, interfaces y tipos de TypeScript una sola vez en una librería compartida (libs/shared-types/ en el monorepo). Esto asegura que tanto el frontend como el backend y el microservicio de IA utilicen la misma estructura de datos, eliminando la duplicación y previniendo inconsistencias.
	•	Lógica de Negocio Reutilizable: Identificaremos y extraeremos lógica de negocio común o utilidades que puedan reutilizarse en diferentes partes de la aplicación. Por ejemplo, funciones de validación de datos, formateo de fechas o cálculos específicos. Estas se colocarán en librerías compartidas (libs/utils/).
	•	Componentes Reutilizables (Frontend): Crearemos componentes de UI genéricos y reutilizables en el frontend para evitar recrear la misma interfaz múltiples veces.

### 2.2. SRP (Single Responsibility Principle - Principio de Responsabilidad Única)

Principio: Un módulo, clase o función debe tener una, y solo una, razón para cambiar.

Aplicación en el Proyecto:
	•	Separación de Servicios: Nuestra arquitectura monorepo ya promueve esto al separar claramente el backend (API), el frontend (UI) y el ia-microservice (lógica de IA). Cada uno tiene una responsabilidad principal.
	•	Clases y Módulos Cohesivos (NestJS): Dentro del backend (NestJS), cada módulo y servicio tendrá una responsabilidad bien definida. Por ejemplo, un AuthService se encargará solo de la autenticación y autorización, no de la gestión de perfiles de usuario.
	•	Funciones Enfocadas (FastAPI, NestJS, Next.js): Cada función o método debe hacer una única cosa bien. Si una función necesita hacer varias cosas, es una señal de que podría necesitar ser dividida en funciones más pequeñas y con responsabilidades más específicas.
	•	Componentes de UI (Next.js): Los componentes de React deben tener una responsabilidad clara, ya sea presentar datos, gestionar un estado específico o interactuar con una API.

### 2.3. Barrel Files (Archivos Índice)

Principio: Un “barrel” es un archivo (típicamente index.ts o index.js) que exporta públicamente interfaces, clases, funciones o constantes de otros módulos dentro del mismo directorio o subdirectorios. Esto simplifica las declaraciones de importación.

Aplicación en el Proyecto:
	•	Organización de Módulos: Utilizaremos barrel files en directorios que contengan múltiples archivos relacionados (ej. src/auth/, src/users/, libs/shared-types/).
	•	Importaciones Limpias: En lugar de importar import { User } from '../../../../libs/shared-types/src/lib/user.interface';, podremos importar import { User } from '@monorepo/shared-types'; o import { AuthService from './auth'; si el barrel file está en el mismo nivel.

Ejemplo:
En libs/shared-types/src/index.ts:

export * from './lib/user.interface';
export * from './lib/job-posting.interface';
export * from './lib/application.interface';
// ... y así sucesivamente para todos los tipos compartidos


Luego, en cualquier parte del monorepo, podemos importar:

import { User, JobPosting } from '@monorepo/shared-types';

Consideraciones:
	•	Evitar Dependencias Circulares: Hay que tener cuidado de no crear dependencias circulares al usar barrel files, donde el archivo index.ts de un directorio importa algo que a su vez importa algo del mismo index.ts.
	•	Tree-shaking: Aunque los bundlers modernos son muy buenos, un uso excesivo o incorrecto de barrel files podría, en casos raros, afectar la efectividad del tree-shaking (eliminación de código no utilizado). Sin embargo, los beneficios de organización y legibilidad suelen superar este riesgo en la mayoría de los casos.

4. Herramientas de Calidad de Código

Para asegurar la consistencia del código, la detección temprana de errores y el cumplimiento de las directrices de estilo, utilizaremos las siguientes herramientas:
	•	ESLint (Linter):
	•	Propósito: Analiza estáticamente el código para identificar patrones problemáticos, errores de programación, errores de estilo y posibles bugs. Ayuda a mantener la calidad del código y a aplicar las mejores prácticas.
	•	Configuración: Se configurará a nivel de monorepo con reglas adaptadas a TypeScript y React/NestJS, y se integrará con Nx para que se ejecute en los proyectos relevantes.
	•	Prettier (Formateador de Código):
	•	Propósito: Formatea automáticamente el código para asegurar un estilo consistente en todo el proyecto (indentación, comillas, saltos de línea, etc.). Elimina las discusiones sobre el estilo en las revisiones de código.
	•	Configuración: Se configurará a nivel de monorepo para trabajar en conjunto con ESLint, resolviendo conflictos de estilo automáticamente.
	•	Reglas de Cursor (IDE):
	•	Propósito: Complementan a ESLint y Prettier proporcionando feedback en tiempo real directamente en el IDE. Permiten aplicar las directrices de codificación y estilo de forma proactiva mientras se escribe el código, ayudando a mantener el "flow state" y la consistencia inmediata.
	•	Configuración: Se configurarán dentro del entorno de Cursor para alinear las sugerencias y correcciones automáticas con las reglas definidas por ESLint y Prettier, así como con las preferencias específicas del proyecto.
	•	Integración en el Flujo de Trabajo:
	•	Scripts de Gestor de Paquetes (pnpm): Se añadirán scripts en el package.json del monorepo para ejecutar ESLint y Prettier manualmente o como parte de los procesos de CI/CD.
	•	Integración con IDE (VS Code): Se recomendarán extensiones de VS Code para ESLint y Prettier, permitiendo que el formateo y la detección de errores ocurran en tiempo real mientras se escribe el código.
	•	Hooks de Git (Husky + lint-staged): Se configurarán hooks de pre-commit para que ESLint y Prettier se ejecuten automáticamente solo en los archivos modificados antes de cada commit. Esto asegura que solo el código que cumple con los estándares se suba al repositorio.

5. Prácticas de Desarrollo y Calidad

Para asegurar la robustez, estabilidad y mantenibilidad del proyecto, adoptaremos las siguientes prácticas clave a lo largo del ciclo de desarrollo:
	•	Seguridad de Dependencias (Dependabot): Se activará Dependabot en el repositorio de GitHub para escanear automáticamente las dependencias en busca de vulnerabilidades conocidas y crear Pull Requests para actualizarlas a versiones seguras.
	•	Pruebas Tempranas y Continuas:
	•	Esencial para el MVP: Cada funcionalidad que desarrollemos debe ir acompañada de sus pruebas (unitarias para funciones/métodos, de integración para los endpoints de la API y, eventualmente, end-to-end para los flujos de usuario críticos).
	•	Impacto: Esto nos dará confianza para iterar rápidamente, refactorizar sin miedo y asegurar la calidad del código.
	•	Manejo de Errores y Logging Centralizado:
	•	Crítico para la Estabilidad: Implementaremos una estrategia robusta para el manejo de errores en todos los servicios (frontend, backend, IA).
	•	Visibilidad: Se configurará un sistema de logging centralizado para registrar eventos importantes, errores y advertencias, lo que es fundamental para la depuración y el monitoreo en producción.
	•	Mejores Prácticas de Seguridad:
	•	Obligatorias desde el Inicio: Más allá de la autenticación con JWT, se aplicarán prácticas de seguridad como la validación estricta de entradas, el uso de bcrypt para el cifrado de contraseñas, la gestión segura de variables de entorno y la protección contra vulnerabilidades comunes (ej. inyección SQL/NoSQL, XSS, CSRF).
	•	Documentación de la API (Swagger/OpenAPI):
	•	Muy Recomendable para el MVP: Utilizaremos herramientas que permitan generar automáticamente la documentación de la API del backend (NestJS) a partir del código.
	•	Beneficio: Facilita enormemente la comunicación y el desarrollo colaborativo entre el equipo de backend y frontend, y es una buena práctica para cualquier API.
	•	CI/CD desde el Inicio (simple):
	•	Habilitador Clave: Configuraremos una pipeline de Integración Continua/Despliegue Continuo (CI/CD) utilizando **GitHub Actions** desde las primeras etapas.
	•	Alcance Inicial: Inicialmente, esta pipeline puede ser muy básica: ejecutar las pruebas automáticamente en cada push al repositorio y construir las imágenes de Docker de los servicios.
	•	Impacto: Nos acostumbra al flujo de trabajo automatizado, proporciona feedback rápido sobre la calidad del código y prepara el terreno para despliegues más complejos.
	•	Monitoreo de Rendimiento y Bucle de Retroalimentación del Usuario:
	•	Consideraciones para el MVP: Aunque pueden ser más ligeros en el MVP, los tendremos en cuenta desde el diseño.
	•	Monitoreo: Integrar herramientas básicas para el monitoreo del rendimiento de la aplicación (APM) para identificar cuellos de botella.
	•	Feedback: Pensar en mecanismos simples para recopilar la retroalimentación de los usuarios del MVP, lo cual es crucial para la evolución del producto.

6. Uso de Librerías Externas

Para acelerar el desarrollo, mejorar la calidad y la robustez de la aplicación, aprovecharemos el vasto ecosistema de librerías externas. Aquí se detallan algunas de las clave que utilizaremos:
	•	Frontend (Next.js/React):
	•	Axios: Cliente HTTP para realizar peticiones a la API de forma eficiente y robusta.
	•	React Query (TanStack Query): Para la gestión de datos asíncronos, caching, sincronización y actualización de datos del servidor.
	•	React Hook Form: Para la gestión y validación de formularios de manera performante y flexible, integrándose bien con Zod.
	•	Shadcn/ui: Colección de componentes de UI reutilizables, accesibles y personalizables, construidos con Radix UI y Tailwind CSS.
	•	date-fns / Day.js: Para el manejo, formateo y manipulación de fechas de manera eficiente.
	•	Backend (NestJS/Node.js):
	•	Zod: Para la validación de esquemas de datos y tipos en las peticiones y respuestas de la API, asegurando la integridad de los datos.
	•	Winston / Pino: Para un logging estructurado y eficiente, permitiendo diferentes niveles de log y transportes.
	•	dotenv: Para la gestión segura de variables de entorno en el entorno de desarrollo.
	•	Clerk (Opcional/Considerar): Plataforma de gestión de usuarios que simplifica la autenticación y autorización. Podría reemplazar o complementar nuestra implementación de JWT para acelerar el desarrollo del MVP en esta área.
	•	Microservicio de IA (FastAPI/Python):
	•	Las librerías específicas se definirán según los modelos de IA a implementar (ej. scikit-learn, spaCy, transformers, nltk para NLP, etc.).

7. Integración con MCPs (Multi-Cloud Platforms) y Seguridad de Claves API

Integraremos servicios externos clave para potenciar las capacidades de la plataforma. El manejo seguro de las claves API es una prioridad absoluta.
	•	MCPs a Considerar:
	•	Playwright: Para la automatización de navegadores, principalmente para pruebas end-to-end (E2E) de la interfaz de usuario.
	•	Firecrawl: Potencialmente para capacidades de web scraping o rastreo de contenido web, útil para la ingesta de datos de ofertas de empleo externas.
	•	context7 (@upstash/context7-mcp): Para caching distribuido, gestión de sesiones, o como una base de datos de clave-valor serverless para datos temporales o de alta velocidad.
	•	Manejo Seguro de Claves API:
	•	Principio: Las claves API y cualquier otra credencial sensible NUNCA deben ser hardcodeadas en el código fuente ni subidas al repositorio de Git.
	•	Implementación:
	•	Variables de Entorno: Se utilizarán variables de entorno para almacenar todas las claves API. En desarrollo, se cargarán desde archivos .env (que serán excluidos del control de versiones mediante .gitignore).
	•	Gestión de Secretos en Producción: Para entornos de producción, se utilizarán servicios dedicados de gestión de secretos (ej. AWS Secrets Manager, Google Secret Manager, HashiCorp Vault) o configuraciones seguras del proveedor de la nube.
	•	Acceso Restringido: El acceso a estas variables de entorno o secretos se restringirá solo a los servicios que los necesiten.


8. Organización del Agente Orquestador y Especialización

En este proyecto, yo (el agente orquestador) operaré de manera especializada para cada parte del monorepo, sin necesidad de “crear” agentes de IA separados. Mi especialización se logrará a través de la configuración de archivos GEMINI.md en los directorios específicos de cada aplicación o librería.
	•	Un Único Agente Orquestador: Yo soy el único agente de IA con el que interactuarás. Mi capacidad para “especializarme” reside en mi habilidad para leer y aplicar las directrices contextuales.
	•	Mecanismo de Especialización (GEMINI.md):
	•	Dentro de la estructura del monorepo (ej. apps/backend/, apps/frontend/, apps/ia-microservice/), crearemos archivos GEMINI.md específicos para cada uno.
	•	Estos archivos GEMINI.md contendrán instrucciones, preferencias y directrices detalladas para el desarrollo en esa área particular. Por ejemplo, el GEMINI.md del backend podría especificar patrones de diseño, librerías específicas para ese servicio, o reglas de negocio particulares.
	•	Cuando estemos trabajando en un directorio específico (ej. cd apps/backend/), yo leeré el GEMINI.md de ese directorio y adaptaré mi comportamiento y mis sugerencias para actuar como un “experto” en esa área.
	•	Cuándo se “Crean” (Activan): Estos archivos GEMINI.md se crearán como parte de la Fase 1: Configuración Inicial y Backend del MVP, específicamente cuando inicialicemos las aplicaciones backend, frontend y ia-microservice dentro del monorepo Nx. En ese momento, los poblaremos con las directrices iniciales.
	•	Cuáles se “Crearán”:
	•	apps/backend/GEMINI.md (para el desarrollo del backend con NestJS)
	•	apps/frontend/GEMINI.md (para el desarrollo del frontend con Next.js)
	•	apps/ia-microservice/GEMINI.md (para el desarrollo del microservicio de IA con FastAPI)
	•	Podríamos considerar libs/shared-types/GEMINI.md si necesitamos directrices muy específicas para la definición de tipos compartidos.

Este enfoque nos permite mantener un contexto muy específico y relevante para la tarea en curso, optimizando mi asistencia y asegurando que las decisiones de diseño y codificación se alineen con las necesidades de cada parte del proyecto.


⸻




Compromiso:

Nos comprometemos a aplicar estos principios y herramientas de forma consistente a lo largo de todo el ciclo de vida del desarrollo del proyecto. Esto asegurará un código base de alta calidad que sea fácil de entender, mantener y extender.

### 9. Sistema de Prompts para Desarrollo Interno

Para acelerar el desarrollo y mantener la consistencia, utilizaremos un sistema de prompts reutilizables. Este sistema no es para el usuario final, sino una herramienta de productividad para el equipo de desarrollo.

*   **Propósito**: Automatizar la creación de código repetitivo (boilerplate), pruebas, modelos de datos y más.
*   **Ubicación de Plantillas**: Todas las plantillas de prompts se almacenarán en el directorio `dev_prompts/` en la raíz del proyecto.
*   **Invocación**: Se utilizará un script auxiliar o la propia CLI de Gemini para combinar las plantillas con argumentos y generar el código.

**Ejemplo de Flujo de Trabajo**:
1.  Necesitas un nuevo componente de React.
2.  En la terminal, ejecutas un comando como: `/crear_componente_react --nombre=UserProfile`
3.  El sistema utiliza la plantilla de `dev_prompts/react_component.prompt` para generar el código del componente.
4.  Pega el código generado en un nuevo archivo en el proyecto.

## 10. Estrategia de Especialización del Agente IA (GEMINI.md)

Para optimizar la asistencia de la IA y asegurar que sus sugerencias sean contextualmente relevantes para cada parte del monorepo, se utilizará un sistema de archivos de configuración `GEMINI.md`.

*   **Concepto Clave:** No se crean múltiples "agentes de IA". Se utiliza un único agente (Gemini CLI) que adapta su comportamiento leyendo archivos de instrucciones locales.
*   **Mecanismo de Funcionamiento:**
    1.  **Un Único Agente:** El Gemini CLI es el único agente que opera en el proyecto.
    2.  **Carga de Contexto Jerárquica:** Antes de cada acción, el agente busca un archivo `GEMINI.md` en el directorio de trabajo actual. Si no lo encuentra, busca en el directorio padre, y así sucesivamente hasta la raíz del proyecto.
    3.  **Especialización por Instrucción:** Las instrucciones en el `GEMINI.md` más cercano a la tarea actual tienen la máxima prioridad. Esto permite que el agente se "especialice" temporalmente. Por ejemplo, un `GEMINI.md` en `apps/ia-microservice/` puede instruir al agente para que genere únicamente código de Python, mientras que en `apps/frontend/` las instrucciones se centrarán en Next.js.
*   **Implementación:** Se crearán archivos `GEMINI.md` dentro de los directorios de las aplicaciones (`apps/frontend`, `apps/backend`, etc.) a medida que se inicialicen, como se describe en el `TASK_PLAN.md`.

## 11. Flujo de Trabajo de Tareas Automatizado con IA

Para maximizar la eficiencia y estandarizar el desarrollo, adoptaremos un flujo de trabajo semi-automatizado gestionado por el agente de IA.

1.  **Inicio de Tarea:** El desarrollador solicita al agente de IA que comience una tarea, proveyendo el ID de la misma desde Linear (ej. "Comenzar con la tarea EVAL-125").
2.  **Creación de Rama:** El agente de IA se encarga de:
    *   Asegurarse de estar en la rama `develop`.
    *   Actualizar la rama con los últimos cambios del repositorio (`git pull`).
    *   Crear y cambiarse a una nueva rama de feature siguiendo la convención `feat/<issue-id>-nombre-descriptivo`.
    *   Notificar al desarrollador que la nueva rama está lista.
3.  **Desarrollo Colaborativo:** El desarrollador y el agente de IA trabajan juntos en la rama de feature para completar la tarea.
4.  **Finalización y Commit:** Una vez la tarea está completa y aprobada por el desarrollador, el agente de IA:
    *   Añade todos los cambios al área de preparación (`git add .`).
    *   Crea un commit siguiendo el formato de commits convencionales, incluyendo una referencia que cierra el issue de Linear (ej. `feat(auth): implement login form\n\nCloses EVAL-125`).
5.  **Creación de Pull Request (Paso Manual Clave):**
    *   El agente de IA sube la rama de feature a GitHub (`git push`).
    *   **El agente NO fusionará la rama directamente.** En su lugar, proporcionará el enlace para crear un **Pull Request (PR)**.
    *   El desarrollador es responsable de abrir el PR, revisarlo, verificar que los chequeos de CI (GitHub Actions) pasen, y finalmente, fusionarlo a `develop`. Este paso es un control de calidad humano indispensable.
6.  **Limpieza:** Una vez el PR es fusionado, el agente de IA puede, si se le solicita, volver a la rama `develop`, actualizarla y borrar la rama de feature que ya no se necesita.

