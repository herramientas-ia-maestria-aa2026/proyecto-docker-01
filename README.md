# Proyecto Docker 01 — JupyterLab

**Maestría en Inteligencia Artificial Aplicada**  
**Asignatura:** Herramientas para Inteligencia Artificial

## 1. Descripción

Este proyecto proporciona un entorno de desarrollo basado en **Docker y JupyterLab** para realizar prácticas de programación en Python, análisis de datos e inteligencia artificial.

El entorno permite ejecutar JupyterLab y las bibliotecas necesarias sin instalarlas directamente en el sistema operativo.

Los archivos creados desde JupyterLab se almacenan en el repositorio local, facilitando su administración mediante Git y GitHub.

## 2. Requisitos previos

Para trabajar con este proyecto es necesario disponer de:

- Git.
- Docker Engine.
- Docker Compose.
- Un navegador web.

Verificar las herramientas instaladas:

```bash
git --version
docker --version
docker compose version
```

No es necesario instalar Python, JupyterLab ni sus bibliotecas directamente en el equipo.

## 3. Estructura del repositorio

```text
proyecto-docker-01/
│
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── README.md
├── .gitignore
│
├── data/
│   └── dataset.csv
│
├── ejemplo01.ipynb
├── ejemplo02.ipynb
└── ejemplo03.ipynb
```

**Descripción de los componentes:**

| Archivo o directorio | Descripción |
|---|---|
| `Dockerfile` | Define la imagen Docker utilizada para ejecutar JupyterLab. |
| `docker-compose.yml` | Configura el servicio, los puertos y los volúmenes. |
| `requirements.txt` | Contiene las bibliotecas de Python necesarias. |
| `data/` | Almacena los datasets utilizados en las prácticas. |
| `*.ipynb` | Notebooks desarrollados desde JupyterLab. |
| `.gitignore` | Excluye archivos temporales del repositorio. |

Los nombres de notebooks y datasets son solo ejemplos.

## 4. Luego de hacer el fork, clonar el repositorio

Ejecutar desde una terminal:

```bash
git clone https://github.com/su-usuario/proyecto-docker-01.git
```

Ingresar al directorio:

```bash
cd proyecto-docker-01
```

## 5. Construir la imagen Docker

Para construir la imagen:

```bash
docker compose build
```

Este proceso instala las dependencias definidas en `requirements.txt`.

La construcción es necesaria en la primera ejecución y cuando se modifican las dependencias o el `Dockerfile`.

## 6. Iniciar JupyterLab

Para crear e iniciar el contenedor:

```bash
docker compose up -d
```

La opción `-d` permite ejecutar el contenedor en segundo plano.

También es posible construir la imagen e iniciar el contenedor mediante un solo comando:

```bash
docker compose up -d --build
```

Comprobar su estado:

```bash
docker compose ps
```

### Acceder a JupyterLab

Abrir el navegador e ingresar a:

**http://localhost:9999**

La configuración del proyecto utiliza el puerto `9999` del equipo para acceder a JupyterLab, que se ejecuta en el puerto `8888` del contenedor.

Cuando se solicite, ingresar el token de acceso configurado para el entorno (1234)

Para consultar los registros:

```bash
docker compose logs jupyter
```

Para observar los registros en tiempo real:

```bash
docker compose logs -f jupyter
```

Presionar `Ctrl+C` para dejar de visualizar los registros sin detener el contenedor.

## 7. Crear y ejecutar notebooks

Desde JupyterLab:

1. Seleccionar **Python Notebook**.
2. Crear un nuevo notebook.
3. Escribir y ejecutar el código Python.
4. Guardarlo con un nombre representativo, por ejemplo, `ejemplo01.ipynb`.

Los notebooks se guardan directamente en la raíz del repositorio.

Ejemplo:

```python
import pandas as pd

datos = {
    "estudiante": ["Ana", "Luis", "María"],
    "calificacion": [9.2, 8.5, 9.7]
}

df = pd.DataFrame(datos)

df
```

**Importante:** Los notebooks se almacenan automáticamente en el equipo local gracias al volumen compartido de Docker.

No es necesario copiarlos manualmente desde el contenedor.

## 8. Trabajar con datasets

Los archivos de datos utilizados en las prácticas deben almacenarse en el directorio:

```text
data/
```

Por ejemplo:

```text
data/estudiantes.csv
```

Para cargar el archivo desde un notebook ubicado en la raíz del repositorio:

```python
import pandas as pd

df = pd.read_csv("data/estudiantes.csv")

df.head()
```

Para comprobar el directorio de trabajo:

```python
import os

print(os.getcwd())
```

Cuando el notebook se ejecuta desde la raíz del proyecto, el directorio de trabajo corresponde a:

```text
/app
```

Esto permite utilizar rutas relativas como:

```python
df = pd.read_csv("data/estudiantes.csv")
```

## 9. Administrar dependencias

Las bibliotecas necesarias para el proyecto se definen en:

```text
requirements.txt
```

Por ejemplo:

```text
jupyterlab
numpy
pandas
matplotlib
scikit-learn
```

Para incorporar una nueva biblioteca:

1. Abrir `requirements.txt

2. Agregar el nombre de la biblioteca.

3. Guardar los cambios.

4. Reconstruir e iniciar el contenedor:

> docker compose up -d --build
