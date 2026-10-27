# test-MLOps

# Actividad 1 - MLOps

Proyecto de la Actividad 1 de MLOps. Esta guía explica cómo instalar las dependencias y validar la conexión con Prefect y MLflow en Windows usando PowerShell.

## Requisitos

- Git
- Python 3.12, 3.13 o 3.14
- Poetry
- Docker Desktop iniciado

## Clonar e instalar

Abre PowerShell y ejecuta:

```powershell
git clone https://github.com/daniicadenam-ops/Actividad-1-MLOps.git
cd Actividad-1-MLOps
poetry install
```

El proyecto configura Poetry para crear el entorno virtual dentro de la carpeta del repositorio. Si Poetry no encuentra automáticamente una versión compatible de Python, selecciona una instalada en tu computador. Por ejemplo:

```powershell
poetry env use 3.13
poetry install
```

## Iniciar MLflow y Prefect

Desde la raíz del repositorio, inicia los servicios con Docker Compose:

```powershell
cd services
docker compose up -d
```

Los servicios quedan disponibles en:

- Prefect: <http://localhost:4200>
- MLflow: <http://localhost:5000>

## Ejecutar el flujo de validación

En la misma terminal de PowerShell, configura las direcciones de los servicios:

```powershell
$env:PREFECT_API_URL = "http://localhost:4200/api"
$env:MLFLOW_TRACKING_URI = "http://localhost:5000"
```

Vuelve a la raíz del repositorio y ejecuta el flujo:

```powershell
cd ..
poetry run python flows/prueba_flow.py
```

El flujo suma los números del 1 al 5 y registra el resultado en MLflow.

## Comprobar el resultado

1. Abre <http://localhost:4200/runs> y comprueba que el flujo `prueba` finalizó con estado `Completed`.
2. Abre <http://localhost:5000> y comprueba que existe el experimento `prueba-validacion`.

El valor registrado para la suma debe ser `15`.

## Detener los servicios

Desde la raíz del repositorio:

```powershell
cd services
docker compose down
```

## Estructura del repositorio

Esa estructura refleja las carpetas principales que aparecen en GitHub. Si quieres que el README describa con precisión qué contiene cada una, comparte una captura del explorador de archivos o el resultado de `tree /F /A` ejecutado desde la raíz del repositorio.


```text
Actividad-1-MLOps/
├── configs/       # Archivos de configuración
├── data/          # Datos del proyecto
├── flows/         # Flujos de Prefect
├── scripts/       # Scripts auxiliares
├── services/      # Docker Compose para MLflow y Prefect
├── pyproject.toml # Dependencias y configuración del proyecto
├── poetry.lock    # Versiones bloqueadas de dependencias
├── poetry.toml    # Configuración de Poetry
└── README.md      # Instrucciones del proyecto
```


