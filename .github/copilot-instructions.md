# Instrucciones de Revisión de Código para GitHub Copilot (Filtro de TI)

Al revisar cualquier Pull Request en este repositorio, actúa como un Arquitecto de Software Senior de TI y verifica obligatoriamente los siguientes 3 criterios de rechazo inmediato:

## 1. Cumplimiento de Clean Architecture
- Verifica que `backend/Books.Domain` **no** tenga dependencias hacia `Books.Application`, `Books.Infrastructure`, `Books.Api` ni paquetes NuGet de persistencia (`Microsoft.EntityFrameworkCore.*`).
- Verifica que `backend/Books.Application` dependa únicamente de `Books.Domain` y **nunca** de `Books.Infrastructure`.
- Señala como error crítico cualquier acceso directo a `BookDbContext` desde `Program.cs` para operaciones de negocio que deban pasar por `BookService` / `IBookRepository`.

## 2. Cero Exposición de Credenciales y Secretos
- Revisa `appsettings.json`, archivos `.cs`, `.ts`, `.tsx` y workflows para asegurar que **no existan** cadenas de conexión (`Server=...`, `Password=...`), API Keys ni secretos hardcodeados.
- Recuerda al autor que toda credencial debe gestionarse mediante **GCP Secret Manager** en Cloud Run o `dotnet user-secrets` / variables de entorno en local.

## 3. Cobertura de Pruebas Unitarias y de Integración
- Todo nuevo endpoint en el Backend o componente en el Frontend debe incluir su prueba correspondiente en `backend/Books.Tests` (`xUnit`) o `frontend/src` (`Vitest`).
- Rechaza cambios que eliminen o deshabiliten tests existentes (`[Fact(Skip = ...)]` o `it.skip`), especialmente los tests de `ArchitectureTests.cs`.
