# Documento de Requerimientos: Plataforma Conexus

## Introducción

Este documento detalla los requerimientos para la plataforma "Conexus", un sistema inteligente diseñado para optimizar el proceso de reclutamiento de talento freelance. La plataforma conectará a freelancers con reclutadores, automatizando y mejorando la evaluación de habilidades, la gestión de postulaciones y la transparencia del proceso.

## Requerimientos

### Requerimiento 1: Gestión de Perfiles y Roles

**User Story:** Como usuario, quiero poder registrarme en la plataforma y crear un perfil detallado que represente mis capacidades (si soy freelancer) o las necesidades de mi empresa (si soy reclutador), para poder interactuar de forma significativa en la plataforma.

#### Criterios de Aceptación

1.  CUANDO un usuario se registra ENTONCES el sistema DEBERÁ permitirle elegir entre un rol de `FREELANCER` o `RECRUITER`.
2.  CUANDO un usuario es un `FREELANCER` ENTONCES el sistema DEBERÁ permitirle crear y editar un perfil con sus habilidades, experiencia, biografía y disponibilidad.
3.  CUANDO un usuario es un `RECRUITER` ENTONCES el sistema DEBERÁ permitirle crear y editar un perfil de empresa.
4.  SI un usuario intenta registrarse con un email ya existente ENTONCES el sistema DEBERÁ mostrar un error claro y prevenir el registro.

### Requerimiento 2: Publicación y Búsqueda de Ofertas de Trabajo

**User Story:** Como reclutador, quiero publicar ofertas de trabajo detalladas. Como freelancer, quiero buscar y filtrar estas ofertas para encontrar proyectos que se ajusten a mis habilidades.

#### Criterios de Aceptación

1.  CUANDO un reclutador crea una oferta ENTONCES el sistema DEBERÁ permitirle especificar título, descripción, habilidades requeridas y presupuesto.
2.  CUANDO un freelancer busca ofertas ENTONCES el sistema DEBERÁ proveer filtros por habilidad, categoría y tipo de proyecto.
3.  CUANDO un freelancer ve una oferta ENTONCES el sistema DEBERÁ mostrarle claramente los requisitos y detalles del proyecto.
4.  SI no hay ofertas que coincidan con los criterios de búsqueda ENTONCES el sistema DEBERÁ mostrar un mensaje informativo.

### Requerimiento 3: Sistema de Evaluación de Habilidades

**User Story:** Como reclutador, quiero crear y asignar tests técnicos a mis ofertas de trabajo para evaluar objetivamente las habilidades de los candidatos.

#### Criterios de Aceptación

1.  CUANDO un reclutador crea un test ENTONCES el sistema DEBERÁ permitirle añadir preguntas de opción múltiple con una respuesta correcta definida.
2.  CUANDO un reclutador crea una oferta de trabajo ENTONCES el sistema DEBERÁ permitirle asociar un test existente a esa oferta.
3.  CUANDO un freelancer completa un test ENTONCES el sistema DEBERÁ calificarlo automáticamente y almacenar el resultado.
4.  SI un freelancer aprueba el test ENTONCES su postulación DEBERÁ ser marcada como "evaluación superada".

### Requerimiento 4: Flujo de Postulación y Seguimiento

**User Story:** Como freelancer, quiero postularme a una oferta y seguir el estado de mi postulación. Como reclutador, quiero ver una lista de los candidatos que han postulado y su desempeño.

#### Criterios de Aceptación

1.  CUANDO un freelancer se postula a una oferta con test ENTONCES el sistema DEBERÁ guiarlo para que complete el test como siguiente paso.
2.  CUANDO un freelancer ve sus postulaciones ENTONCES el sistema DEBERÁ mostrar el estado actual de cada una (Ej: `APPLIED`, `TEST_COMPLETED`, `REJECTED`).
3.  CUANDO un reclutador ve los postulantes de una oferta ENTONCES el sistema DEBERÁ mostrarlos en una lista, priorizando a aquellos con mejores resultados en el test.
4.  SI un freelancer intenta postularse dos veces a la misma oferta ENTONCES el sistema DEBERÁ prevenirlo y notificarle que ya ha postulado.

### Requerimiento 5: Matching Inteligente (MVP)

**User Story:** Como reclutador, quiero que el sistema me sugiera los candidatos más relevantes para mis ofertas, para no perder tiempo revisando perfiles que no encajan.

#### Criterios de Aceptación

1.  CUANDO un reclutador publica una oferta ENTONCES el microservicio de IA DEBERÁ analizar las habilidades requeridas.
2.  CUANDO el análisis se completa ENTONCES el sistema DEBERÁ generar un ranking básico de freelancers existentes basado en la coincidencia de habilidades.
3.  CUANDO el reclutador ve la oferta ENTONCES el sistema DEBERÁ mostrarle una lista de candidatos sugeridos.
4.  SI no hay candidatos sugeridos ENTONCES el sistema DEBERÁ indicarlo claramente.

### Requerimiento 6: Calidad y Mantenibilidad del Código

**User Story:** Como desarrollador, quiero que el sistema tenga una arquitectura modular y siga las mejores prácticas, para que el código sea mantenible y escalable.

#### Criterios de Aceptación

1.  CUANDO se desarrolle el sistema ENTONCES el código DEBERÁ seguir los principios DRY y SRP.
2.  CUANDO se definan tipos de datos ENTONCES estos DEBERÁN residir en una librería compartida en el monorepo para ser usados por el frontend y el backend.
3.  CUANDO se escriba código ENTONCES este DEBERÁ cumplir con las reglas de ESLint y Prettier configuradas en el proyecto.
4.  CUANDO se añada una nueva funcionalidad ENTONCES esta DEBERÁ estar acompañada de pruebas unitarias.
