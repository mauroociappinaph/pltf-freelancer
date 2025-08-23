# Guía de Configuración del Editor (Cursor / VSCode)

Este documento sirve como una guía para configurar tu entorno de desarrollo integrado (IDE) y asegurar una experiencia de desarrollo consistente, productiva y alineada con las guías de calidad del proyecto.

## 1. Extensiones Recomendadas

Para sacar el máximo provecho, asegúrate de tener las siguientes extensiones instaladas en tu editor:

*   **ESLint:** Integra ESLint directamente en el editor para mostrar errores de linting en tiempo real.
*   **Prettier - Code formatter:** La extensión oficial para formatear el código automáticamente.
*   **EditorConfig for VS Code:** Ayuda a mantener estilos de codificación consistentes entre diferentes editores y IDEs.
*   **GitLens — Git supercharged:** Mejora las capacidades de Git integradas, mostrando autoría del código, historial y mucho más.

## 2. Configuración del Editor (`settings.json`)

La regla más importante es hacer que tu editor obedezca las configuraciones del proyecto. Abre tu archivo `settings.json` en Cursor/VSCode (puedes usar `Cmd + Shift + P` y buscar "Open User Settings (JSON)") y asegúrate de que contenga estas líneas. Esto habilitará el formateo automático al guardar y establecerá Prettier como el formateador por defecto.

```json
{
  // ...otras configuraciones que tengas...
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"]
}
```

## 3. Snippets de Código Personalizados

Los snippets aceleran la escritura de código repetitivo. Puedes definirlos en tu editor (busca "Configure User Snippets"). Aquí tienes ejemplos para empezar:

**React Functional Component (rfc-ts):**
```json
{
  "React Functional Component": {
    "prefix": "rfc-ts",
    "body": [
      "import React from 'react';",
      "",
      "type ${1:ComponentName}Props = {",
      "  $2",
      "};",
      "",
      "const ${1:ComponentName}: React.FC<${1:ComponentName}Props> = ({ $3 }) => {",
      "  return (",
      "    <div>",
      "      <h1>${1:ComponentName}</h1>",
      "    </div>",
      "  );",
      "};",
      "",
      "export default ${1:ComponentName};"
    ],
    "description": "Creates a new React functional component with TypeScript"
  }
}
```

**NestJS Service (nest-service):**
```json
{
  "NestJS Service": {
    "prefix": "nest-service",
    "body": [
      "import { Injectable } from '@nestjs/common';",
      "",
      "@Injectable()",
      "export class ${1:ServiceName}Service {",
      "  constructor() {}",
      "",
      "  findAll() {`
    return `This action returns all ${1:ServiceName.toLowerCase()}`;
  `}",
      "}"
    ],
    "description": "Creates a new NestJS service"
  }
}
```

## 4. Comandos de IA Personalizados (Cursor)

Usa la funcionalidad de IA de Cursor para crear comandos que entiendan el contexto de nuestro proyecto. Algunos ejemplos a configurar:

*   **`@Custom Generar Test para Componente`:** Entrénale para que, al seleccionar un componente, genere un archivo de prueba `.test.tsx` que use `Jest` y `@testing-library/react`, importe el componente y cree un test de renderizado básico.
*   **`@Custom Documentar Servicio NestJS`:** Entrénale para que añada comentarios JSDoc a los métodos públicos de una clase de servicio en NestJS, explicando su propósito, parámetros y valor de retorno.
*   **`@Custom Crear DTO desde Interfaz`:** Entrénale para que, a partir de una interfaz de TypeScript, genere una clase DTO (Data Transfer Object) de NestJS con los decoradores de `class-validator` correspondientes.
