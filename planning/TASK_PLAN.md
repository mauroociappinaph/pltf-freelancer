# Plan de Implementación: Plataforma Evaluta

Este documento desglosa el proyecto completo en fases, tareas y subtareas accionables. Cada tarea principal está vinculada a los requerimientos definidos en `REQUIREMENTS.md`.

---

### Fase 1: Configuración del Proyecto y Entorno

- [ ] **1. Estructura del Monorepo y Dependencias**
  - [ ] 1.1. Inicializar el monorepo de Nx en la rama `develop`.
  - [ ] 1.2. Instalar dependencias principales del workspace con pnpm (typescript, prettier, eslint, husky).
  - [ ] 1.3. Configurar los archivos raíz (`.prettierrc`, `.eslintrc.json`).
  - [ ] 1.4. Configurar Husky con `lint-staged` para el hook `pre-commit`.
  - _Requerimientos: 6.1, 6.3_

- [ ] **2. Configuración de Docker**
  - [ ] 2.1. Crear el archivo `docker-compose.yml` en la raíz del proyecto.
  - [ ] 2.2. Añadir el servicio de la base de datos MongoDB al `docker-compose.yml`.
  - [ ] 2.3. Crear un archivo `.env.example` con las variables de entorno necesarias (ej. `DATABASE_URL`).
  - _Requerimientos: 6.1_

### Fase 2: Desarrollo del Backend (MVP)

- [ ] **3. Inicialización de la Aplicación Backend**
  - [ ] 3.1. Generar la aplicación de NestJS (`backend`) dentro de la carpeta `apps/`.
  - [ ] 3.2. Crear el `Dockerfile` para la aplicación `backend`.
  - [ ] 3.3. Integrar el servicio del backend en el `docker-compose.yml`.
  - [ ] 3.4. Crear el archivo `apps/backend/GEMINI.md` con directrices para el desarrollo de NestJS.
  - _Requerimientos: 6.1, 6.2_

- [ ] **4. Capa de Base de Datos con Prisma**
  - [ ] 4.1. Inicializar Prisma en la aplicación `backend`.
  - [ ] 4.2. Implementar el `schema.prisma` completo con todos los modelos y relaciones.
  - [ ] 4.3. Generar el cliente de Prisma y ejecutar la migración inicial.
  - [ ] 4.4. Crear un servicio `PrismaService` para encapsular el cliente.
  - _Requerimientos: 5.1, 5.2, 5.3, 5.4_

- [ ] **5. Módulo de Autenticación y Usuarios**
  - [ ] 5.1. Crear el `AuthModule` y `UsersModule` en NestJS.
  - [ ] 5.2. Implementar el servicio de registro de usuarios (con hashing de contraseña).
  - [ ] 5.3. Implementar el servicio de login que retorna un JWT.
  - [ ] 5.4. Crear Guards de JWT para proteger rutas.
  - [ ] 5.5. Crear los endpoints (controladores) para `auth/register` y `auth/login`.
  - _Requerimientos: 1.1, 1.4_

- [ ] **6. Módulo de Perfiles (Freelancer y Reclutador)**
  - [ ] 6.1. Crear el `ProfilesModule`.
  - [ ] 6.2. Implementar los servicios para crear y actualizar perfiles de freelancer y reclutador.
  - [ ] 6.3. Crear los endpoints protegidos para la gestión de perfiles.
  - _Requerimientos: 1.2, 1.3_

- [ ] **7. Módulo de Ofertas de Trabajo y Tests**
  - [ ] 7.1. Crear el `JobsModule` y `TestsModule`.
  - [ ] 7.2. Implementar los servicios CRUD para `JobPosting`.
  - [ ] 7.3. Implementar los servicios CRUD para `Test` y `Question`.
  - [ ] 7.4. Crear los endpoints para la gestión de ofertas y tests.
  - _Requerimientos: 2.1, 3.1, 3.2_

- [ ] **8. Módulo de Postulaciones (Applications)**
  - [ ] 8.1. Crear el `ApplicationsModule`.
  - [ ] 8.2. Implementar el servicio para que un freelancer cree una postulación.
  - [ ] 8.3. Implementar la lógica para la auto-evaluación de un test al postular.
  - [ ] 8.4. Implementar el servicio para que un reclutador vea los postulantes de una oferta, ordenados por score.
  - [ ] 8.5. Crear los endpoints correspondientes.
  - _Requerimientos: 3.3, 3.4, 4.1, 4.2, 4.3, 4.4_

### Fase 3: Desarrollo del Frontend (MVP)

- [ ] **9. Inicialización de la Aplicación Frontend**
  - [ ] 9.1. Generar la aplicación de Next.js (`frontend`) dentro de la carpeta `apps/`.
  - [ ] 9.2. Configurar Tailwind CSS.
  - [ ] 9.3. Crear una librería de UI compartida (`libs/shared/ui`) con componentes base (botones, inputs).
  - [ ] 9.4. Crear el archivo `apps/frontend/GEMINI.md` con directrices para el desarrollo de Next.js.
  - _Requerimientos: 6.1, 6.2_

- [ ] **10. Flujo de Autenticación y Páginas Públicas**
  - [ ] 10.1. Crear las páginas de Registro y Login.
  - [ ] 10.2. Implementar los formularios con `react-hook-form`.
  - [ ] 10.3. Integrar las llamadas a la API de `auth/` del backend.
  - [ ] 10.4. Implementar la gestión del estado de autenticación (ej. con Zustand y almacenamiento local).
  - [ ] 10.5. Crear la página principal (`/`) y la página de listado de ofertas (`/jobs`).
  - _Requerimientos: 1.1, 2.2, 2.3_

- [ ] **11. Páginas del Freelancer**
  - [ ] 11.1. Crear el dashboard del freelancer (`/dashboard`).
  - [ ] 11.2. Crear la página para editar su perfil.
  - [ ] 11.3. Crear la página para ver sus postulaciones y el estado.
  - [ ] 11.4. Implementar el flujo para realizar un test.
  - _Requerimientos: 1.2, 4.1, 4.2_

- [ ] **12. Páginas del Reclutador**
  - [ ] 12.1. Crear el dashboard del reclutador (`/dashboard/recruiter`).
  - [ ] 12.2. Crear el formulario para publicar/editar una oferta de trabajo.
  - [ ] 12.3. Crear la vista para ver los postulantes de una oferta.
  - [ ] 12.4. Crear la interfaz para crear un Test y añadirle preguntas.
  - _Requerimientos: 1.3, 2.1, 3.1, 4.3_

### Fase 4: Desarrollo del Microservicio de IA (MVP)

- [ ] **13. Inicialización y Lógica Básica**
  - [ ] 13.1. Generar la aplicación de FastAPI (`ia-microservice`) dentro de `apps/`.
  - [ ] 13.2. Crear el `Dockerfile` para el servicio de IA e integrarlo en `docker-compose.yml`.
  - [ ] 13.3. Crear un endpoint `/suggest-candidates` que reciba un `jobId`.
  - [ ] 13.4. Implementar un algoritmo simple de matching por conteo de habilidades coincidentes.
  - [ ] 13.5. Integrar la llamada a este servicio desde el backend de NestJS.
  - [ ] 13.6. Crear el archivo `apps/ia-microservice/GEMINI.md` con directrices para el desarrollo de FastAPI/Python.
  - _Requerimientos: 5.1, 5.2, 5.3, 5.4_

### Fase 5: Pruebas y Documentación Final

- [ ] **14. Pruebas**
  - [ ] 14.1. Escribir pruebas unitarias para los servicios críticos del backend.
  - [ ] 14.2. Escribir pruebas unitarias para los componentes complejos del frontend.
  - [ ] 14.3. Escribir pruebas de integración para el flujo de postulación.
  - _Requerimientos: 6.4_

- [ ] **15. Documentación**
  - [ ] 15.1. Escribir el `README.md` principal con instrucciones de instalación y ejecución.
  - [ ] 15.2. Generar la documentación de la API del backend con Swagger/OpenAPI.
  - _Requerimientos: 6.1_
