# Instrucciones para Interactuar con el Agente Gemini

Este documento resume las frases y comandos clave que puedes usar para interactuar con el agente de IA (Gemini CLI) y guiarlo a través del flujo de trabajo de desarrollo.

---

## 1. Iniciar una Nueva Tarea

Indica al agente en qué tarea deseas trabajar o pídele que te muestre las tareas pendientes.

- `"Ok, empecemos con la tarea 1.1 del TASK_PLAN.md: 'Inicializar el monorepo de Nx'."`
- `"Vamos a trabajar en la tarea 5.2: 'Implementar el servicio de registro de usuarios'."`
- `"He encontrado un bug. Lo he registrado en Linear como CONEX-42. Empecemos a trabajar en él."`
- `"Muéstrame los issues abiertos en GitHub."`

---

## 2. Durante el Desarrollo

Guía al agente para generar código, hacer modificaciones, investigar o validar resultados.

- `"Ejecuta el comando npx nx@latest init."`
- `"Crea el AuthService en el backend."`
- `"El método de login necesita también validar si el usuario está activo. Modifícalo."`
- `"El código que generaste es correcto. Continúa."`

---

## 3. Finalizar una Tarea (Commit y Push)

Indica al agente que la tarea está completa y que debe preparar los cambios para la integración.

- `"La funcionalidad está completa y funciona como se esperaba. Podemos cerrar esta tarea."`
- `"Ok, todo listo. Procede a hacer el commit y subir los cambios."`

---

## 4. Verificación Automatizada de Tareas

Pide al agente que ejecute verificaciones de código.

- `"Ejecuta pnpm lint y tsc --noEmit."`
- `"Corre pnpm test."`
- `"Verifica dependencias circulares con npx madge --circular --extensions ts,tsx ./apps/<app-name>."`

---

## 5. Manejo de Errores y Ramas `fix/`

Indica al agente que cree una rama para abordar un error.

- `"El comando falló. Crea una rama fix/issue-<numero-del-issue> para investigar y corregir esto."`

---

## 6. Limpieza y Siguiente Tarea

Informa al agente que un Pull Request ha sido fusionado y que puede limpiar o pasar a la siguiente tarea.

- `"El PR ha sido fusionado. Por favor, haz la limpieza."`
- `"Listo, PR mergeado. Empecemos con la siguiente tarea: TASK-1.2..."`
