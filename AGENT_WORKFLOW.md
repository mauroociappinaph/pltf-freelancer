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

#### Mi Respuesta

Al recibir tu instrucción, yo me encargaré de:
1.  Confirmar la tarea.
2.  Actualizar mi rama `develop` local con los últimos cambios de GitHub (`git pull`).
3.  Crear una nueva rama de feature con el nombre correcto (ej. `feat/TASK-1.1-init-nx`).
4.  Notificarte que la rama está creada y lista para empezar a trabajar.

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

### **Paso 3: Finalizar una Tarea**

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
4.  **Te entregaré el enlace para crear el Pull Request (PR).**

---

### **Paso 4: Revisión y Fusión (Pull Request)**

Este es el paso de control de calidad más importante, y es **100% tuyo**.

#### Tu Acción

1.  Haz clic en el enlace que te proporcioné para abrir el Pull Request en GitHub.
2.  Revisa los cambios que hemos hecho.
3.  Confirma que las pruebas automáticas de GitHub Actions (nuestro CI) pasan con éxito.
4.  Si todo es correcto, haz clic en el botón **"Merge Pull Request"** en GitHub.

#### Mi Respuesta

En este paso, yo simplemente espero tu confirmación.

---

### **Paso 5: Limpieza y Siguiente Tarea**

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
3.  Borrar la rama de feature que ya no necesitamos (`git branch -d <nombre-de-la-rama>`).
4.  Te confirmaré que todo está limpio y esperaré la instrucción para la siguiente tarea.
