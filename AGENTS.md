# Reglas de Arquitectura y Seguridad para Agentes IA (Vicoders Golden Path)

Este repositorio es el template oficial `app_template_fullstack` gobernado por TI. Todo código generado o modificado debe cumplir estrictamente estas reglas:

## 1. Stack Tecnológico Fijo
- **Backend**: C# sobre `.NET 10` (`net10.0`) con Minimal APIs y Entity Framework Core (SQL Server).
- **Frontend**: React con TypeScript (Vite) sobre **Node.js 26 LTS** y estilos limpios/minimalistas.
- **Tests**: `xUnit` en Backend (`Books.Tests`) y `Vitest` + `@testing-library/react` en Frontend.

## 2. Separación Estricta en Clean Architecture (`backend/`)
- `Books.Domain`: Solo entidades de dominio e interfaces de repositorio. **Prohibido** agregar referencias a otros proyectos o paquetes de infraestructura (como Entity Framework).
- `Books.Application`: Casos de uso, DTOs y lógica de aplicación. Solo puede referenciar a `Books.Domain`. **Prohibido** referenciar a `Books.Infrastructure` o `Books.Api`.
- `Books.Infrastructure`: `DbContext` de EF Core, migraciones/configuración SQL Server e implementación de repositorios. Referencia a `Books.Domain` y `Books.Application`.
- `Books.Api`: Endpoints HTTP (Minimal APIs), configuración de CORS e inyección de dependencias.

## 3. Seguridad y Cero Exposición de Secretos
- **Nunca** escribir cadenas de conexión, contraseñas, tokens o IPs en `appsettings.json`, código C# o código TypeScript.
- `ConnectionStrings:DefaultConnection` en `appsettings.json` debe permanecer vacío (`""`). En producción se inyecta desde **GCP Secret Manager** vía Cloud Run (`ConnectionStrings__DefaultConnection`).

## 4. Pruebas Obligatorias
- Toda nueva funcionalidad o endpoint debe mantener en verde las pruebas de arquitectura (`ArchitectureTests.cs`), las pruebas de integración (`BooksApiTests.cs`) y las pruebas de interfaz (`App.test.tsx`).
