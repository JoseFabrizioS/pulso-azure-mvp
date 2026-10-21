# PULSO | Radar Inteligente de Necesidades Universitarias

**Proyecto Final — Azure Bootcamp LEAD UTP 2026-II**

## Descripción

PULSO es un MVP web orientado a identificar, organizar y priorizar necesidades universitarias mediante un sistema de evaluación transparente.

Su objetivo es apoyar la toma de decisiones sobre problemáticas de accesibilidad, infraestructura, bienestar estudiantil, tecnología y otros ámbitos universitarios.

## Funcionalidades

- Registro de necesidades mediante formulario interactivo.
- Evaluación de urgencia, alcance y recurrencia.
- Cálculo automático de un índice de prioridad de 0 a 100.
- Panel de indicadores y distribución de reportes.
- Consulta de diagnósticos individuales.
- Generación de enlaces compartibles.
- Exportación de información en formato JSON.

## Tecnologías implementadas

**Microsoft Azure Static Web Apps:** alojamiento de la aplicación web en el plan gratuito, con acceso público mediante HTTPS.

**GitHub Actions (CI/CD):** integración y despliegue automatizado desde el repositorio de GitHub hacia Azure.

**HTML, CSS y JavaScript:** desarrollo de la interfaz, las funcionalidades y el algoritmo de priorización.

**Almacenamiento local del navegador:** conservación de reportes de prueba sin requerir una base de datos externa.

## Arquitectura

GitHub → GitHub Actions → Azure Static Web Apps → Navegador del usuario.

El sistema ejecuta el algoritmo de priorización en el navegador. Los nuevos registros se almacenan localmente; los enlaces de diagnóstico permiten compartir una copia de la información de cada caso.

## Alcance del MVP

Esta primera versión es un prototipo educativo que utiliza datos ficticios y permite demostrar un proceso digital de registro, evaluación y priorización de necesidades.

No utiliza modelos de inteligencia artificial generativa ni una base de datos centralizada. La priorización se realiza mediante reglas programadas y criterios verificables.

## Aplicación publicada

https://white-dune-04f02a710.4.azurestaticapps.net

## Repositorio

https://github.com/JoseFabrizioS/pulso-azure-mvp
