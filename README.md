# embedded-system-api-ai

> API for AI model execution, data inference, and advanced data processing in the Embedded Hardware-Software System.  
> *API para ejecución de modelos de IA, inferencia de datos y procesamiento avanzado del Sistema Embebido Hardware-Software.*

---

## Language / Idioma

- [English Documentation](#en--english)
- [Documentación en Español](#es--español)

---

## EN | English

### Overview

This repository implements the AI and Data Science API, the inference layer of the system. It consumes analytics data stored in MongoDB, executes trained machine learning models, and exposes inference results through a REST API. It is completely decoupled from the Core Operational API to allow independent scaling, versioning, and maintenance of the AI workloads.

### Role in the Ecosystem

This component sits at the top of the data processing pipeline. It reads feature data and time-series telemetry from MongoDB, runs inference or model training tasks, and writes prediction outputs back to MongoDB. Results are then consumed by the web portal (`embedded-system-portal`) for visualization. It has no direct dependency on PostgreSQL or the MQTT broker.

Primary responsibilities:

- Loading and serving trained machine learning models.
- Executing inference tasks on incoming or historical telemetry data.
- Exposing model predictions and analytics results via REST endpoints.
- Supporting model retraining workflows on demand or on schedule.

### Technology Stack

| Component | Technology |
|:---|:---|
| Language | Python 3.11+ |
| Web Framework | FastAPI |
| ML Libraries | scikit-learn, TensorFlow / PyTorch (as needed) |
| Data Processing | pandas, NumPy |
| Database Client | Motor (async MongoDB) |
| Deployment | Docker / Docker Compose |

### Prerequisites

- Python 3.11+
- Docker 24+ and Docker Compose v2+
- Running instance of `embedded-system-db-mongo`

### Project Structure

```
embedded-system-api-ai/
├── app/
│   ├── api/               # Route definitions and inference endpoint handlers
│   ├── core/              # Application configuration and startup
│   ├── models/            # Trained model artifacts and loading utilities
│   ├── schemas/           # Pydantic request/response schemas
│   └── services/          # Inference logic, data preparation, and training pipelines
├── notebooks/             # Exploratory analysis and model development notebooks
├── tests/                 # Unit and integration tests
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── README.md
```

### Environment Variables

| Variable | Description | Example |
|:---|:---|:---|
| `MONGO_URI` | MongoDB connection URI | `mongodb://admin:pass@mongo:27017` |
| `MONGO_DATABASE` | Target analytics database | `embedded_analytics` |
| `MODEL_PATH` | Path to model artifact directory | `/app/models` |
| `DEBUG` | Enable debug mode | `false` |

### Setup and Deployment

```bash
# Start the service
docker compose up -d

# View application logs
docker compose logs -f api-ai

# Run tests
docker compose run --rm api-ai pytest

# Stop the service
docker compose down
```

### API Reference

The interactive API documentation is available at `http://localhost:8001/docs` (Swagger UI) once the service is running.

---

## ES | Español

### Descripción General

Este repositorio implementa la API de IA y Ciencia de Datos, la capa de inferencia del sistema. Consume datos analíticos almacenados en MongoDB, ejecuta modelos de aprendizaje automático entrenados y expone los resultados de inferencia a través de una API REST. Está completamente desacoplada de la API Operacional Core para permitir escalado, versionado y mantenimiento independientes de las cargas de trabajo de IA.

### Rol en el Ecosistema

Este componente se ubica en la parte superior de la cadena de procesamiento de datos. Lee datos de características y telemetría en series de tiempo desde MongoDB, ejecuta tareas de inferencia o entrenamiento de modelos, y escribe las salidas de predicción de vuelta en MongoDB. Los resultados son luego consumidos por el portal web (`embedded-system-portal`) para su visualización. No tiene dependencia directa con PostgreSQL ni con el broker MQTT.

Responsabilidades principales:

- Carga y servicio de modelos de aprendizaje automático entrenados.
- Ejecución de tareas de inferencia sobre telemetría entrante o histórica.
- Exposición de predicciones de modelos y resultados analíticos mediante endpoints REST.
- Soporte de flujos de reentrenamiento de modelos bajo demanda o de forma programada.

### Stack Tecnológico

| Componente | Tecnología |
|:---|:---|
| Lenguaje | Python 3.11+ |
| Framework Web | FastAPI |
| Bibliotecas ML | scikit-learn, TensorFlow / PyTorch (según requerimiento) |
| Procesamiento de Datos | pandas, NumPy |
| Cliente de Base de Datos | Motor (MongoDB asíncrono) |
| Despliegue | Docker / Docker Compose |

### Prerequisitos

- Python 3.11+
- Docker 24+ y Docker Compose v2+
- Instancia activa de `embedded-system-db-mongo`

### Estructura del Proyecto

```
embedded-system-api-ai/
├── app/
│   ├── api/               # Definición de rutas y manejadores de endpoints de inferencia
│   ├── core/              # Configuración y arranque de la aplicación
│   ├── models/            # Artefactos de modelos entrenados y utilidades de carga
│   ├── schemas/           # Esquemas Pydantic de solicitud/respuesta
│   └── services/          # Lógica de inferencia, preparación de datos y pipelines de entrenamiento
├── notebooks/             # Notebooks de análisis exploratorio y desarrollo de modelos
├── tests/                 # Pruebas unitarias e integración
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── README.md
```

### Variables de Entorno

| Variable | Descripción | Ejemplo |
|:---|:---|:---|
| `MONGO_URI` | URI de conexión a MongoDB | `mongodb://admin:pass@mongo:27017` |
| `MONGO_DATABASE` | Base de datos analítica de destino | `embedded_analytics` |
| `MODEL_PATH` | Ruta al directorio de artefactos del modelo | `/app/models` |
| `DEBUG` | Activar modo debug | `false` |

### Configuración y Despliegue

```bash
# Iniciar el servicio
docker compose up -d

# Ver logs de la aplicación
docker compose logs -f api-ai

# Ejecutar pruebas
docker compose run --rm api-ai pytest

# Detener el servicio
docker compose down
```

### Referencia de API

La documentación interactiva de la API está disponible en `http://localhost:8001/docs` (Swagger UI) una vez que el servicio esté en ejecución.
