# Copilot Instructions for AI Coding Agents

## Arquitectura General
- El proyecto sigue Clean Architecture en ASP.NET Core 8.0, con capas bien definidas:
  - **Domain**: Entidades, lógica de negocio y constantes.
  - **Application**: Casos de uso, servicios de aplicación, interfaces y configuración.
  - **Infrastructure**: Implementaciones concretas, acceso a datos, servicios externos, migraciones.
  - **Web**: API REST, controladores, middlewares, validaciones y servicios web.
- Los flujos de datos y dependencias siempre van de afuera hacia adentro (Web → Application → Domain), nunca al revés.

## Flujos de Desarrollo Clave
- **Compilación y ejecución local**:
  - Modifica la cadena de conexión en `src/CleanArchitecture/appsettings.Development.json`.
  - Ejecuta: `dotnet run ./src/CleanArchitecture/CleanArchitecture.csproj`
- **Ejecución en Docker**:
  - Usa: `docker-compose up --build` (requiere Docker y SQL Server)
- **Empaquetado y plantillas**:
  - `dotnet pack -o nupkg`
  - `dotnet new install ./ --force`
  - `dotnet new cleanarch -n template-project`
- **Pruebas**:
  - Unit tests en `CleanArchitecture.UnitTests/`
  - Integration tests en `src/CleanArchitecture.IntegrationTest/` (usa `HttpClient` y configuración propia)
  - Ejecuta pruebas con: `dotnet test`

## Convenciones y Patrones Específicos
- Los modelos deben llevar sufijos `Request`/`Response` según su propósito.
- El manejo de errores y validaciones se realiza mediante middlewares en `src/CleanArchitecture/Web/Middlewares/`.
- Los repositorios siguen el patrón genérico en `src/CleanArchitecture/Application/Repositories/`.
- Los servicios de infraestructura se configuran en `src/CleanArchitecture/Infrastructure/ConfigureServices.cs`.
- Los tests de integración pueden ejecutarse en Docker para simular entornos reales.

## Integraciones y Dependencias
- Autenticación JWT y manejo de usuarios con Identity.
- Health checks expuestos en `/health` y `/healthcheck-ui`.
- Logging y manejo de excepciones centralizados.
- Soporte para background jobs y sidecar architecture (Hangfire, programado en roadmap).
- Docker y Terraform para despliegue y pruebas.

## Ejemplos de Archivos Clave
- `src/CleanArchitecture/Program.cs`: punto de entrada principal.
- `src/CleanArchitecture/Application/ConfigureServices.cs`: configuración de servicios de aplicación.
- `src/CleanArchitecture/Infrastructure/ConfigureServices.cs`: configuración de infraestructura.
- `src/CleanArchitecture/Web/Controller/`: controladores API.
- `src/CleanArchitecture/Web/Middlewares/`: middlewares personalizados.
- `src/CleanArchitecture.IntegrationTest/TestCase/`: casos de prueba de integración.

## Recomendaciones para Agentes
- Respeta la separación de capas y dependencias.
- Usa los sufijos de modelos y sigue los patrones de repositorio y middleware.
- Prioriza la configuración y ejecución de pruebas automatizadas.
- Consulta el README para comandos y flujos adicionales.

---
¿Hay alguna sección que requiera mayor detalle o ejemplos específicos? Indica qué parte del flujo o arquitectura necesitas aclarar para mejorar la productividad del agente.
