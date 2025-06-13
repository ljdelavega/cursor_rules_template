# Technical Specifications: [Project Name]

**Author:** [Your Name]
**Date:** 2025-01-01

Note: This is just an example. Fill out or simplify as needed.

---

## 1. Development Environment Setup

A guide to setting up a local development environment.

### 1.1. Prerequisites
* **Node.js:** `v20.x` or later
* **pnpm:** `pnpm` is the required package manager.
* **Docker & Docker Compose:** Required for running the database locally.
* **Git:** For version control.


## 2. Technologies Used

The specific libraries, frameworks, and tools used in this project.

| Category         | Technology       | Version  | Usage Notes                                     |
| ---------------- | ---------------- | -------- | ----------------------------------------------- |
| **Framework**    | `Next.js`        | `^14.1`  | App Router, Server Actions, and API Routes.     |
| **Language**     | `TypeScript`     | `^5.3`   | Strict mode enabled for type safety.            |
| **UI Library**   | `React`          | `^18.2`  | Functional components with management.            |
| **Styling**      | `Tailwind CSS`   | `^3.4`   | Utility-first CSS for rapid UI development.     |
| **Database**     | `PostgreSQL`         | `^16.1`  | Database schema management and queries.         |
| **Linting**      | `ESLint`         | `^8.5`   | Enforces code quality and style.                |
| **Formatting**   | `Prettier`       | `^3.2`   | Automatic code formatting.                      | 

---

## 3. Key Technical Decisions

Critical implementation-level decisions and their rationale.

*   **API Design:** The project uses **Next.js API Routes** to implement a **RESTful API**. This keeps the frontend and backend in a single codebase, simplifying development.
*   **Authentication:** Authentication is handled using **JWTs (JSON Web Tokens)** with an access token (short-lived, in memory) and a refresh token (long-lived, in a secure `HttpOnly` cookie). This provides a good balance of security and performance.
*   **Data Fetching:** Client-side data fetching uses **React Query (`@tanstack/react-query`)** for robust caching, background refetching, and request deduplication.
*   **State Management:** Global client-side state (e.g., UI theme) uses **Zustand** for its simplicity and minimal boilerplate.

---

## 4. Design Patterns & Coding Conventions

All code should adhere to the following patterns for consistency.

*   **Folder Structure:** A **feature-based** folder structure is used within the `src/` directory.
    ```
    /src
    ├── /app
    ├── /components  # Shared, reusable UI components
    └── /features
        └── /auth    # Authentication feature
            ├── /components
            └── /api       # API route handlers
    ```
*   **Component Design:** Components should be small and focused. Where appropriate, the **Container/Presentational Pattern** is encouraged to separate logic from UI.
*   **Naming Conventions:**
    *   Components: `PascalCase` (e.g., `UserProfile.tsx`)
    *   Functions/Variables: `camelCase` (e.g., `getUserProfile`)
    *   Types/Interfaces: `PascalCase` (e.g., `type UserProfile`)
*   **Error Handling:**
    *   **API:** Use centralized middleware for catching errors and formatting consistent responses.
    *   **Client:** Use React's **Error Boundaries** to catch rendering errors and `try/catch` blocks in data-fetching functions.

---

## 5. Technical Constraints

Known limitations that developers must be aware of.

*   **Database:** The project is developed against **PostgreSQL**. While Prisma allows for swapping databases, custom SQL queries are written in PostgreSQL syntax.
*   **API Rate Limits:** Any third-party APIs used (e.g., GitHub) have rate limits. Code must handle potential `429 Too Many Requests` errors gracefully.
*   **Browser Support:** Officially supports the **last two major versions of Chrome, Firefox, and Safari**. Functionality on other browsers is not guaranteed.
*   **Performance Budget:** The initial JavaScript bundle size must not exceed **250kB (gzipped)**. Use `@next/bundle-analyzer` to monitor this.
