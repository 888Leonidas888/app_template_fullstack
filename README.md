# App Template Fullstack (Golden Path - Vicoders)

Repositorio plantilla corporativo gobernado por TI para la creación de aplicaciones Fullstack asistidas por IA (**Codex / Antigravity**).

> **Nota:** Este repositorio plantilla contiene únicamente la estructura de gobernanza, pipelines CI/CD, reglas de revisión y documentación de uso. El código fuente de cada aplicación (`backend/` en .NET 10 Clean Architecture y `frontend/` en React + TypeScript con Node 26 LTS) es generado automáticamente por el agente mediante las **Skills y Rules** corporativas.

---

## 📋 Contenido del Template

| Archivo / Ruta | Propósito |
| :--- | :--- |
| [`README.md`](./README.md) | Guía de uso del template para Vicoders y el equipo de TI. |
| [`plan.md`](./plan.md) | Definición operativa de las 4 fases del **Golden Path** (Local, Filtro TI, QA en GCP y Pase a Producción). |
| [`AGENTS.md`](./AGENTS.md) | Reglas de contexto estático leídas automáticamente por agentes de IA (**Codex**, **Antigravity**, **GitHub Copilot**). |
| [`.github/copilot-instructions.md`](./.github/copilot-instructions.md) | Criterios de auditoría automática para **GitHub Copilot Code Review** en cada Pull Request. |
| [`.github/workflows/ci-cd.yml`](./.github/workflows/ci-cd.yml) | Pipeline automatizado: Filtro de TI (Tests + Clean Architecture + Cero Secretos), Despliegue a Cloud Run (QA) y Pase a Producción con aprobación de 1 clic. |
| [`.gitignore`](./.gitignore) | Exclusión estándar de artefactos de compilación, dependencias y archivos `.env` / secretos locales. |

---

## 🚀 Cómo Usar Este Template

### 1. Para el Usuario de Negocio (Vicoder)
No necesitas clonar ni configurar archivos manualmente. Abre tu agente de IA (**Codex** o **Antigravity**) y solicita tu aplicación en lenguaje natural invocando el Skill corporativo:

1. **Inicialización:** El agente instancia un nuevo proyecto a partir de este template (`app_template_fullstack`).
2. **Construcción guiada por Skills y Rules:** El agente genera las capas de **Clean Architecture** en `.NET 10` (`Domain`, `Application`, `Infrastructure`, `Api`, `Tests`) y el frontend en **React + TypeScript (Node 26 LTS)** cumpliendo las reglas definidas en `AGENTS.md`.
3. **Entrega (Pull Request):** Pide al agente subir tus cambios. El pipeline validará automáticamente tus pruebas, seguridad y arquitectura antes de desplegar en el entorno de **QA en Google Cloud Run**.

---

### 2. Para el Equipo de TI (Configuración del Nuevo Repositorio en GitHub)
Cuando se instancia un nuevo repositorio desde este template:

1. **Secretos de GitHub Actions (`Settings → Secrets and variables → Actions`):**
   * `GCP_PROJECT_ID`: ID del proyecto en Google Cloud Platform.
   * `GCP_SA_KEY`: JSON de la Service Account con permisos de Cloud Run, Artifact Registry y Secret Manager.
2. **Secreto en GCP Secret Manager:**
   * Crear el secreto `db-connection-string` con la cadena de conexión a **Cloud SQL (SQL Server)**.
3. **Entornos en GitHub (`Settings → Environments`):**
   * `qa`: Despliegue continuo automático al integrar en `main`.
   * `production`: Configurar **Required reviewers** (Desarrollador Senior de TI) para habilitar el pase a producción con 1 clic.
4. **Copilot Code Review (cuando la suscripción Copilot Pro/Enterprise esté activa):**
   * En `Settings → Rules → Rulesets`, activar **Automatically request Copilot code review** sobre la rama `main`. Copilot aplicará automáticamente las directrices de `.github/copilot-instructions.md`.
