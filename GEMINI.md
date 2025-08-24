# Project Overview

This project aims to develop an intelligent platform for optimal freelance personnel recruitment. It leverages artificial intelligence to efficiently connect companies with suitable freelance candidates, addressing common frustrations in the recruitment process.

**Key Technologies:**

- **Monorepo:** Nx
- **Frontend:** Next.js (React, TypeScript, Tailwind CSS)
- **Backend:** NestJS (Node.js, TypeScript, GraphQL)
- **AI Microservice:** FastAPI (Python, TensorFlow, Keras, scikit-learn)
- **Database:** MongoDB (with Prisma ORM)
- **Containerization:** Docker
- **Package Manager:** pnpm

**Architecture:**
The project is structured as a monorepo using Nx, separating concerns into a frontend application, a backend API, and a dedicated AI microservice. Shared libraries are used across these applications for consistency.

## Building and Running

To set up and run the project locally, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/mauroociappinaph/pltf-freelancer.git # Replace with actual repo URL if different
    cd pltf-freelancer
    ```
2.  **Install dependencies:**
    ```bash
    pnpm install
    ```
3.  **Configure environment variables:**
    Create a `.env` file in the project root based on `.env.example` and configure the necessary variables (e.g., `DATABASE_URL`).
4.  **Start Docker services (e.g., MongoDB):**
    ```bash
    docker compose up -d
    ```
5.  **Run database migrations (if applicable):**
    ```bash
    # This command will depend on the backend's ORM configuration (e.g., Prisma migrations)
    # TODO: Add specific migration command once backend is set up.
    ```
6.  **Start the applications:**
    ```bash
    pnpm nx serve frontend
    pnpm nx serve backend
    # TODO: Add command for AI microservice once it's set up.
    ```

### Project Verifications

To run all code verifications (lint, type check, tests), use the `verify-all` script:

```bash
pnpm verify-all
```

## Development Conventions

### Git Workflow

The project follows a structured Git workflow with `master`, `develop`, `feat/<issue-id>-descriptive-name`, and `hotfix/` branches to maintain a clean and predictable change history.

### Code Design Principles

- **DRY (Don’t Repeat Yourself):** Emphasizes unique, authoritative representation of knowledge, using shared types, reusable business logic, and UI components.
- **SRP (Single Responsibility Principle):** Ensures modules, classes, and functions have a single reason to change, promoting cohesive services and focused functions.
- **Barrel Files:** Utilized for organizing modules and simplifying import declarations, while being mindful of circular dependencies and tree-shaking.

### Code Quality Tools

- **ESLint:** Static analysis for identifying problematic patterns, errors, and style issues.
- **Prettier:** Automatic code formatter for consistent style.
- **Husky + lint-staged:** Git hooks to ensure code quality checks run automatically before commits.

### Agent Interaction Workflow

For detailed guidance on interacting with the Gemini AI agent and the development workflow, refer to `planning/AGENT_WORKFLOW.md` and `AGENT_INSTRUCTIONS.md`.

## Key Project Documentation

For a comprehensive understanding of the project and its processes, consult the following important documents:

- `CODING_GUIDELINES.md`: Coding guidelines.
- `IDE_SETUP_GUIDE.md`: IDE setup guide.
- `PLAN_DE_PROYECTO.md`: General project plan.
- `RESUMEN_SESION_GEMINI.md`: Summary of previous sessions with the Gemini agent.
- `WORKFLOW.md`: General project workflow description.
- `planning/AGENT_WORKFLOW.md`: Detailed workflow for AI agent interaction.
- `planning/DESIGN_DOCUMENT.md`: Project design document.
- `planning/REQUIREMENTS.md`: Project requirements document.
- `planning/TASK_PLAN.md`: Detailed task plan.
- `AGENT_INSTRUCTIONS.md`: Quick guide for agent instructions.
