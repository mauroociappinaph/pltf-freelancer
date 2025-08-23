# Guía de Flujo de Trabajo para el Desarrollador

Este documento describe el flujo de trabajo y los escenarios de uso de las herramientas integradas (MCP) para el desarrollo de este proyecto, adaptado a un entorno de desarrollador único. El objetivo es maximizar la eficiencia, la organización personal y crear una base de conocimiento sólida.

## Escenario 1: Lunes - Plan de Ataque Semanal

**Objetivo:** Organizar la carga de trabajo personal para mantener el foco y medir el progreso real, evitando la sensación de estar abrumado.

1.  **"Stand-up" Personal:** Se inicia la semana consultando `list_my_issues` para revisar todas las tareas pendientes. Esto sirve como un auto-repaso del estado actual del proyecto.
2.  **Desglose de Tareas:** Se toman los grandes objetivos del `PLAN_DE_PROYECTO.md` y se descomponen en tareas pequeñas y manejables en Linear usando `create_issue`. Esto es clave para la automotivación y para tener victorias tempranas.
    *   *Ejemplo:* `create_issue title='(Backend) Definir el schema de Prisma para Usuarios y Perfiles'`
3.  **Priorización:** Se utiliza el campo de prioridad en Linear (`update_issue id='...' priority=1`) para marcar las tareas más críticas y definir el foco principal de la semana.

## Escenario 2: Martes - Modo Investigación Eficiente

**Objetivo:** Resolver dudas técnicas o de diseño rápidamente, sin perder horas navegando por decenas de pestañas del navegador.

1.  **Búsqueda Dirigida:** Ante una duda técnica (ej. "implementar OAuth 2.0 en Next.js"), se utiliza `firecrawl_search` para obtener una lista curada de los mejores tutoriales y artículos.
2.  **Foco Total:** Se selecciona el mejor resultado y se usa `firecrawl_scrape` para tener el contenido directamente en la terminal, al lado del editor de código, eliminando las distracciones del navegador.
3.  **Base de Conocimiento Personal:** Si un recurso es particularmente bueno, se guarda en la base de conocimiento del proyecto en Linear usando `create_document`, creando una wiki técnica personalizada.

## Escenario 3: Miércoles - Desarrollo sin Interrupciones

**Objetivo:** Mantener el "flow state" (estado de máxima concentración) durante la codificación.

1.  **Ritual de Inicio:** Al comenzar una tarea, se actualiza su estado a "In Progress" con `update_issue`. Este pequeño acto ayuda a formalizar el inicio del trabajo y a enfocarse.
2.  **Consulta Instantánea:** Para dudas sobre la sintaxis o uso de una librería, se utiliza la combinación de `resolve-library-id` y `get-library-docs` para obtener la documentación al instante sin cambiar de contexto.
    *   **Consistencia en Tiempo Real:** Las reglas de Cursor configuradas en el IDE contribuyen a este "flow state" al proporcionar feedback inmediato sobre el estilo y la calidad del código, asegurando la adherencia a las directrices sin interrupciones manuales.
3.  **Notas para el "Yo" del Futuro:** Si se descubre una complicación o una tarea futura mientras se está en medio de otra, en lugar de desviarse, se deja un comentario en la tarea de Linear usando `create_comment`.
    *   *Ejemplo:* `create_comment issueId='...' body='@mauro ¡OJO! Recordar implementar el refresco de token para la API de Google.'`

## Escenario 4: Jueves - Autogestión y Documentación

**Objetivo:** Registrar decisiones y errores para construir una memoria del proyecto fiable.

1.  **Registro Inmediato de Bugs:** Al encontrar un error durante las pruebas, no se confía en la memoria. Se registra inmediatamente con `create_issue`, asignándole la etiqueta 'bug'.
2.  **Documentación de Decisiones:** Las decisiones de arquitectura importantes (ej. "por qué se eligió MongoDB") se documentan en un nuevo documento de Linear con `create_document`. Esto es invaluable para entender el contexto del proyecto meses después.

## Escenario 5: Viernes - Cierre y Autoevaluación

**Objetivo:** Terminar la semana con una sensación clara de logro y dejar todo preparado para el siguiente ciclo.

1.  **Revisión de Logros:** Para una inyección de moral y para visualizar el progreso, se utiliza `list_issues state='Done' updatedAt='-P7D'` para obtener una lista de todo lo completado en la última semana.
2.  **Ajuste del Plan:** Se compara la lista de tareas completadas con el `PLAN_DE_PROYECTO.md` y se ajustan las expectativas o el plan para la semana siguiente, si es necesario.
