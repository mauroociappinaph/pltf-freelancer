# Manual de Flujo de Trabajo con el Agente de IA

Este documento es una guía práctica y un manual de referencia sobre cómo interactuar con el agente de IA (Gemini CLI) para ejecutar nuestro flujo de trabajo de desarrollo de manera eficiente y automatizada.

## El Ciclo de Vida de una Tarea

Nuestro desarrollo se basa en tareas. Cada tarea (feature, bug, etc.) seguirá un ciclo de vida claro. Aquí se detalla tu rol y el rol del agente en cada paso.

---

### **Paso 1: Iniciar una Nueva Tarea**

Es tu rol dar la señal de inicio. Para que yo pueda crear una rama y asociar el trabajo correctamente, necesito que me indiques la tarea en la que vamos a trabajar, idealmente con su ID del `TASK_PLAN.md` o de Linear.

#### Tu Acción

Lanza el proceso con una frase clara y directa.

**Ejemplos de frases que puedes usar:**

> "Ok, empecemos con la tarea 1.1 del `TASK_PLAN.md`: 'Inicializar el monorepo de Nx'."

> "Vamos a trabajar en la tarea 5.2: 'Implementar el servicio de registro de usuarios'."

> "He encontrado un bug. Lo he registrado en Linear como `CONEX-42`. Empecemos a trabajar en él."

> "Muéstrame los issues abiertos en GitHub."

#### Mi Respuesta

Al recibir tu instrucción, yo me encargaré de:

1.  **Listar Issues Abiertos (Opcional):** Si me pides que te muestre los issues abiertos en GitHub, usaré `github__list_issues` para presentarte una lista de tareas pendientes. Esto te ayudará a elegir en qué trabajar.
2.  **Verificar duplicados:** Antes de iniciar la tarea, buscaré archivos o lógica existente que pueda indicar que la tarea ya está realizada o que hay componentes similares. Si encuentro algo, te lo notificaré para que decidamos cómo proceder.
3.  Confirmar la tarea.
4.  Actualizar mi rama `develop` local con los últimos cambios de GitHub (`git pull`).
5.  Crear una nueva rama de feature con el nombre correcto (ej. `feat/TASK-1.1-init-nx`).
6.  Notificarte que la rama está creada y lista para empezar a trabajar.

---

### **Paso 2: Durante el Desarrollo**

En esta fase, trabajamos juntos en la rama de la tarea.

#### Tu Acción

Tu rol es el de director técnico. Me pides que genere código, que haga modificaciones, que investigue algo, y validas los resultados.

**Ejemplos de frases que puedes usar:**

> "Ejecuta el comando `npx nx@latest init`."

> "Crea el `AuthService` en el backend."

> "El método de login necesita también validar si el usuario está activo. Modifícalo."

> "El código que generaste es correcto. Continúa."

#### Mi Respuesta

Ejecutaré las acciones que me pidas (crear archivos, modificarlos, ejecutar comandos) siempre dentro del contexto de la rama de la tarea actual.

---

### **Paso 3: Finalizar una Tarea (Commit y Push)**

Una vez que consideres que todo el trabajo para la tarea está completo y verificado.

#### Tu Acción

Me das la orden de cerrar la tarea y preparar todo para la integración.

**Ejemplos de frases que puedes usar:**

> "La funcionalidad está completa y funciona como se esperaba. Podemos cerrar esta tarea."

> "Ok, todo listo. Procede a hacer el commit y subir los cambios."

#### Mi Respuesta

Automáticamente, yo haré:

1.  Añadir todos los cambios al área de preparación (`git add .`).
2.  Crear un commit con un mensaje siguiendo el estándar de Commits Convencionales (ej. `feat(auth): implement user registration endpoint`).
3.  Subir la rama a GitHub (`git push -u origin <nombre-de-la-rama>`).
4.  **Añadir comentario a la Issue:** Si la tarea está asociada a una issue de GitHub, añadiré un comentario a esa issue detallando la solución implementada.
5.  **Te preguntaré si quieres que ejecute las verificaciones automáticas para esta tarea.** (Ver Paso 4).
6.  **Te entregaré el enlace para crear el Pull Request (PR).**

---

### **Paso 4: Verificación Automatizada de Tareas**

Este paso se ejecuta después de que el código ha sido subido a GitHub, pero antes de que la tarea se marque como completada en `TASK_PLAN.md`.

#### Tu Acción

Si te pregunto si quieres verificaciones, me indicarás qué comandos ejecutar.

**Ejemplos de comandos de verificación que puedes pedir:**

> "Ejecuta `pnpm lint` y `tsc --noEmit`."
> "Corre `pnpm test`."
> "Verifica dependencias circulares con `npx madge --circular --extensions ts,tsx ./apps/<app-name>`."

#### Mi Respuesta

1.  Ejecutaré los comandos de verificación que me indiques.
2.  Te reportaré los resultados.
3.  **Si todas las verificaciones pasan:** Te preguntaré si puedo marcar la tarea como completada en `TASK_PLAN.md` (ej. `[ ]` a `[x]`).
4.  **Si alguna verificación falla:** Te reportaré el fallo y te preguntaré cómo proceder (lo que podría llevarnos al flujo de manejo de errores). Si el fallo es en el workflow de CI/CD, y tienes configurado el token de GitHub, crearé automáticamente una issue en GitHub con el mensaje de error exacto, el stack trace (si aplica) y los pasos que llevaron al fallo. Una vez que el PR de fix asociado sea fusionado, añadiré un comentario a la issue indicando que el fix ha sido aplicado y, si es posible, un resumen de la solución. Además, si el issue fue creado por un fallo en el workflow de CI/CD o un problema persistente del agente, y el fix ha sido verificado, el agente cerrará automáticamente el issue.

---

### **Paso 5: Manejo de Errores y Ramas `fix/`**

Este flujo se activa cuando un comando falla o una verificación no pasa.

#### Tu Acción

Me indicarás si quieres que cree una rama `fix/` para abordar el error.

**Ejemplo de frase:**

> "El comando falló. Crea una rama `fix/issue-<numero-del-issue>` para investigar y corregir esto."

#### Mi Respuesta

1.  Crearé la rama `fix/` (ej. `fix/issue-<numero-del-issue>`).
2.  Trabajaremos en esa rama para aplicar la solución.
3.  Una vez lista, haré el commit y subiré la rama `fix/` a GitHub.
4.  Te proporcionaré el enlace para que crees un Pull Request de la rama `fix/` a `develop`. **Tú serás responsable de revisar y fusionar este PR.**
5.  Una vez fusionado el `fix/` en `develop`, volveré a la rama de la tarea original (`feat/TASK-X.Y-...`) y reintentaré el paso que falló, o continuaré desde donde nos quedamos.
6.  Si me encuentro con un problema que no puedo resolver después de varios intentos (como un error persistente en la generación de una aplicación), y tienes configurado el token de GitHub, te preguntaré si quieres que cree una issue en GitHub con el mensaje de error exacto, el stack trace (si aplica) y los pasos que llevaron al problema para su investigación externa. Una vez que el PR de fix asociado sea fusionado, añadiré un comentario a la issue indicando que el fix ha sido aplicado y, si es posible, un resumen de la solución.

---

### **Paso 6: Revisión y Fusión (Pull Request)**

Este es el paso de control de calidad más importante, y es **100% tuyo**.

#### Tu Acción

1.  Haz clic en el enlace que te proporcioné para abrir el Pull Request en GitHub.
2.  Revisa los cambios que hemos hecho.
3.  Confirma que las pruebas automáticas de GitHub Actions (nuestro CI) pasan con éxito.
4.  Si todo es correcto, haz clic en el botón **"Merge Pull Request"** en GitHub.

#### Mi Respuesta

En este paso, yo simplemente espero tu confirmación.

---

### **Paso 7: Limpieza y Siguiente Tarea**

Una vez que el PR está fusionado en `develop`.

#### Tu Acción

Me informas que el PR fue fusionado y que podemos continuar.

**Ejemplos de frases que puedes usar:**

> "El PR ha sido fusionado. Por favor, haz la limpieza."

> "Listo, PR mergeado. Empecemos con la siguiente tarea: `TASK-1.2`..."

#### Mi Respuesta

Automáticamente, haré:

1.  Cambiar a la rama `develop` (`git checkout develop`).
2.  Actualizarla con los cambios que acabas de fusionar (`git pull`).
3.  **Actualizar el `README.md`:** Añadiré un resumen de los cambios realizados en la tarea completada a la sección "Actualizaciones Recientes del Agente" en el `README.md`.
4.  **No borraré la rama de feature local automáticamente.** Se mantendrá para tu referencia, a menos que me pidas explícitamente que la borre (ej. `git branch -d <nombre-de-la-rama>`).
5.  Te confirmaré que todo está limpio y esperaré la instrucción para la siguiente tarea.
