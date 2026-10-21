# PULSO 3.0 — Simulador presupuestario y asesor IA

MVP para Azure Bootcamp LEAD UTP 2026-II. Sitio: https://white-dune-04f02a710.4.azurestaticapps.net

## Funcionalidades
- Radar de necesidades universitarias, formulario y puntuación explicable.
- Diagnósticos compartibles por enlace; datos nuevos almacenados en el navegador.
- Simulador presupuestario con costos hipotéticos editables y descarga CSV.
- Botón opcional **Analizar con IA**, conectado mediante una API administrada en Azure Static Web Apps al despliegue `gpt-5-mini` de Microsoft Foundry.
- Control del consumo de IA: solo usuarios GitHub autorizados pueden consultar el modelo. El resto del sitio y los diagnósticos permanecen públicos.

## Arquitectura
GitHub → GitHub Actions → Azure Static Web Apps Free → `index.html` y Azure Functions administradas (`/api/asesorar`) → Azure OpenAI / Foundry GPT-5 mini.

Se conserva aparte el agente `pulso-advisor-agent` en Foundry como demostración de la configuración de agentes. La API de esta primera integración **invoca directamente el modelo** GPT-5 mini usando instrucciones de servidor; no invoca el agente guardado. Las recomendaciones requieren verificación humana.

## Configuración segura (en Azure Portal → Static Web App → Variables de entorno, producción)

- `AZURE_OPENAI_ENDPOINT` = `https://pulso-advisor-resource.openai.azure.com`
- `AZURE_OPENAI_DEPLOYMENT` = `gpt-5-mini` (ajustar si el despliegue real tiene otro nombre)
- `AZURE_OPENAI_API_KEY` = **clave privada del recurso Foundry** (nunca subir a GitHub)
- `PULSO_ALLOWED_GITHUB_USERS` = `JoseFabrizioS` (nombres autorizados separados por coma)

La URL del sitio no incluye secretos; la función obtiene la clave únicamente del entorno de servidor. SWA exige inicio de sesión con GitHub en `/api/asesorar` y la función verifica adicionalmente la lista de usuarios autorizados.

## Despliegue

El flujo `.github/workflows/azure-static-web-apps-white-dune-04f02a710.yml` conserva el secreto de despliegue existente e incorpora `api_location: "api"`. El código de API utiliza Azure Functions Node.js v4, y `staticwebapp.config.json` fija el runtime Node 20.

**Pruebas antes de exponer:** confirmar el despliegue verde en GitHub Actions; abrir web anónima; verificar simulador; probar que sin iniciar sesión la ruta API devuelve 401, que usuarios GitHub no autorizados reciben 403, y que el propietario sí puede analizar un caso. No enviar datos personales o sensibles a la IA.

## Limitaciones
Los casos y costos no se comparten entre dispositivos; los presupuestos son educativos y ficticios. No hay base de datos ni herramientas empresariales. No hay límite de consumo global persistente: acceso al modelo restringido al usuario autorizado; el propietario debe vigilar el saldo y evitar consultas repetidas. El modelo puede generar errores.