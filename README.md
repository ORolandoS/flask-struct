<h1 style="text-align: center;">🐍 Mi Proyecto Flask</h1>

<p style="text-align: justify;">Aplicación web desarrollada con <strong>Flask</strong> siguiendo las mejores prácticas de arquitectura, escalabilidad y mantenibilidad. Este proyecto utiliza el patrón <strong>Application Factory </strong>combinado con <strong>Blueprints</strong> para una organización modular y profesional.</p>

---

<h2>📋 Tabla de Contenidos</h2>

- [Características](#-características)
- [Requisitos Previos](#-requisitos-previos)
- [Instalación](#-instalación)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Configuración](#-configuración)
- [Uso](#-uso)
- [Comandos Útiles](#-comandos-útiles)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Contribuciones](#-contribuciones)
- [Licencia](#-licencia)

---

## ✨ Características

- ✅ Arquitectura modular con **Blueprints**
- ✅ Patrón **Application Factory** para evitar importaciones circulares
- ✅ Gestión de múltiples entornos (desarrollo, producción, testing)
- ✅ Control de versiones de base de datos con **Flask-Migrate** (Alembic)
- ✅ Autenticación de usuarios con **Flask-Login**
- ✅ Separación clara entre lógica de negocio, modelos y vistas
- ✅ Estructura lista para producción con **Gunicorn**
- ✅ Pruebas unitarias con **pytest**

---

## 🔧 Requisitos Previos

Antes de comenzar, asegúrate de tener instalado:

- **Python 3.8+** ([Descargar aquí](https://www.python.org/downloads/))
- **pip** (gestor de paquetes de Python)
- **virtualenv** o **venv** (recomendado)
- **Git** (para control de versiones)

---

## 📦 Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/mi-proyecto-flask.git
cd mi-proyecto-flask
```
---
## 📂 Estructura del Proyecto

### 1. Distribucion de carpetas y archivos

``` bash
mi_proyecto_flask/
│
├── .env                        # Variables de entorno (SECRET_KEY, DB_URI, etc.)
├── .gitignore                  # Archivos y carpetas ignorados por Git
├── requirements.txt            # Dependencias del proyecto (pip freeze)
├── config.py                   # Clases de configuración (Dev, Prod, Test)
├── run.py                      # Punto de entrada para desarrollo local
├── wsgi.py                     # Punto de entrada para producción (Gunicorn/uWSGI)
│
├── app/                        # Paquete principal de la aplicación
│   ├── __init__.py             # Application Factory (create_app)
│   ├── extensions.py           # Inicialización de extensiones (DB, Login, Migrate)
│   │
│   ├── models/                 # Modelos de Base de Datos (SQLAlchemy)
│   │   ├── __init__.py
│   │   └── user.py
│   │
│   ├── blueprints/             # Módulos de la aplicación (Rutas y Lógica)
│   │   ├── auth/               # Blueprint de Autenticación
│   │   │   ├── __init__.py
│   │   │   ├── routes.py
│   │   │   └── forms.py        # Formularios (WTForms)
│   │   │
│   │   └── main/               # Blueprint Principal (Dashboard, Home)
│   │       ├── __init__.py
│   │       ├── routes.py
│   │       └── forms.py
│   │
│   ├── templates/              # Archivos HTML (Motor Jinja2)
│   │   ├── base.html           # Layout principal (heredable)
│   │   ├── auth/
│   │   │   └── login.html
│   │   └── main/
│   │       └── index.html
│   │
│   ├── static/                 # Archivos estáticos (Frontend)
│   │   ├── css/
│   │   │   └── style.css
│   │   ├── js/
│   │   │   └── main.js
│   │   └── img/
│   │       └── logo.png
│   │
│   └── utils/                  # Funciones auxiliares y helpers
│       ├── __init__.py
│       └── helpers.py
│
├── tests/                      # Pruebas unitarias y de integración (Pytest)
│   ├── __init__.py
│   ├── conftest.py             # Fixtures globales para pytest
│   └── test_auth.py
│
└── migrations/                 # Migraciones de base de datos (Flask-Migrate)
    ├── alembic.ini                 # Configuración general de Alembic
    ├── env.py                      # Script de entorno (conexión a DB y contexto Flask)
    ├── script.py.mako              # Plantilla Mako para generar nuevos scripts de migración
    └── versions/                   # Carpeta donde se guardan las migraciones generadas
        ├── __init__.py
        └── 001_create_users_table.py  # Ejemplo de migración generada
```
---
### 2. Descripcion de carpetas y archivos
---
#### 2.1 Archivos en la Raíz del Proyecto
|Archivo|Descripción                  |
|-------|-----------------------------|
|`.env` |Archivo de variables de entorno que contiene configuraciones sensibles como SECRET_KEY", URLs de base de datos y configuraciones específicas del entorno. "Nunca debe subirse a Git.|
|`.env.example`|Plantilla de ejemplo de las variables de entorno necesarias. Sirve como guía para otros desarrolladores que clonen el proyecto.|
|`.gitignore`|Lista de archivos y carpetas que Git debe ignorar durante el control de versiones. Incluye directorios como venv/", "__pycache__/", archivos ".sqlite y el archivo .env para proteger información sensible.|
|`requirements.txt`|Archivo que lista todas las dependencias Python del proyecto con sus versiones específicas. Se genera con pip freeze > requirements.txt y se instala con pip install -r requirements.txt.|
|`config.py`|Módulo de configuración que define clases para diferentes entornos (DevelopmentConfig", "ProductionConfig", "TestingConfig). Permite cambiar el comportamiento de la aplicación según el entorno sin modificar el código.|
|`run.py`|Punto de entrada principal para desarrollo local. Ejecuta el servidor de desarrollo de Flask con app.run(). No debe usarse en producción.|
|`wsgi.py`|Punto de entrada para servidores WSGI de producción como Gunicorn o uWSGI. Crea la instancia de la aplicación usando la Application Factory.|
|`app/`|Paquete principal que contiene toda la lógica de la aplicación.|
|`tests/`|Carpeta con pruebas unitarias y de integración (pytest).|
|`migrations/`|Control de versiones de la base de datos (Alembic/Flask-Migrate).|

---
#### 2.2 app/ (Paquete principal)
|Archivo/Carpeta|Descripción                  |
|---------------|-----------------------------|
|`__init__.py`  |Contiene la Application Factory (create_app"). Es el corazón que ensambla la app: carga config, inicializa extensiones y registra blueprints."|
|`extensions.py`|Instancias globales de extensiones (SQLAlchemy, Migrate, LoginManager). Se inicializan aquí para evitar |
---
#### 2.3 app/models/
|Archivo|Descripción                  |
|-------|-----------------------------|
|`__init__.py`|Hace que models sea un paquete Python.|
|`user.py`|Modelo User" con sus columnas, relaciones y métodos (ej. "set_password).|
---
#### 2.4 app/blueprints/auth/ (Autenticación)
|Archivo|Descripción                  |
|-------|-----------------------------|
|`__init__.py`|Crea el Blueprint auth_bp.   |
|`routes.py`|Rutas de autenticación: login, logout, registro.|
|`forms.py`|Formularios WTForms para login/registro con validaciones.|

---
#### 2.5 app/blueprints/main/ (Principal)
|Archivo|Descripción                  |
|-------|-----------------------------|
|`__init__.py`|Crea el Blueprint main_bp.   |
|`routes.py`|Rutas públicas: home, about, dashboard.|
|`forms.py`|Formularios específicos de la sección principal.|

---
#### 2.6 app/templates/
|Archivo|Descripción                  |
|-------|-----------------------------|
|`__init__.py`|Crea el Blueprint main_bp.   |
|`routes.py`|Rutas públicas: home, about, dashboard.|
|`forms.py`|Formularios específicos de la sección principal.|

---
#### 2.7 app/static/
|Carpeta|Descripción                  |
|-------|-----------------------------|
|`css/` |Hojas de estilo (style.css). |
|`js/`  |Scripts del cliente (main.js).|
|`img/` |Imágenes (logos, iconos, fondos).|

---
#### 2.8 app/utils/
|Archivo|Descripción                  |
|-------|-----------------------------|
|`__init__.py`|Hace que utils sea un paquete.|
|`helpers.py`|Funciones helper: formateo de fechas, validaciones, envío de emails, etc.|

---
#### 2.9 tests/ (Pruebas)
|Archivo|Descripción                  |
|-------|-----------------------------|
|`__init__.py`|Hace que tests sea un paquete reconocible por pytest.|
|`conftest.py`|Fixtures globales de pytest (ej. cliente de prueba, base de datos temporal).|
|`test_auth.py`|Pruebas unitarias del blueprint auth.|

---
#### 2.10 migrations/ (Control de versiones DB)
|Archivo/Carpeta|Descripción                  |
|---------------|-----------------------------|
|`alembic.ini`  |Configuración de Alembic (logging, formato de archivos).|
|`env.py`       |Script que conecta Alembic con Flask y SQLAlchemy. Permite autogenerate de migraciones.|
|`script.py.mako`|Plantilla Mako usada para generar nuevos scripts de migración.|
|`versions/`    |Carpeta con los scripts de migración generados (flask db migrate). Cada archivo representa un cambio en el esquema de la DB.|

---
## ⚙️ Configuración
### 1. Variables de Entorno (.env)
```
# Configuración de Flask
FLASK_APP=run.py
FLASK_CONFIG=development
SECRET_KEY=tu-clave-secreta-aqui

# Base de datos
DEV_DATABASE_URL=sqlite:///dev-data.sqlite
DATABASE_URL=postgresql://user:password@localhost/dbname
```
---
### 2. Entornos Disponibles
```
i. development: Modo de desarrollo con DEBUG activado y base de datos SQLite.
ii. production: Modo de producción con DEBUG desactivado.
iii. testing: Modo de pruebas con base de datos temporal.
```
---
## 🚀 Uso
### 1. Ejecutar en Desarrollo
```bash
python run.py
```
La aplicación estará disponible en http://localhost:5000
---
### 2. Ejecutar en Producción
```bash
# Linux/macOS
gunicorn wsgi:app

# Windows
waitress-serve --port=5000 wsgi:app
```
---
## 🛠️ Comandos Útiles
### 1. Gestión de Base de Datos
```bash
# Inicializar sistema de migraciones (solo primera vez)
flask db init

# Generar nueva migración después de cambiar modelos
flask db migrate -m "descripción del cambio"

# Aplicar migraciones pendientes
flask db upgrade

# Revertir última migración
flask db downgrade

# Ver historial de migraciones
flask db history

# Ver estado actual de migraciones
flask db current
```
---
### 2. Ejecutar Pruebas
```bash
# Ejecutar todas las pruebas
pytest

# Ejecutar con cobertura de código
pytest --cov=app

# Ejecutar pruebas específicas
pytest tests/test_auth.py
```
---
### 3. Otros Comandos
```bash
# Abrir shell interactivo de Flask
flask shell

# Mostrar rutas registradas
flask routes

# Congelar dependencias actuales
pip freeze > requirements.txt
```
---
## 🧰 Tecnologías Utilizadas
* [Flask ☁](https://flask.palletsprojects.com/?spm=a2ty_o01.29997173.0.0.7eb6c921qbBQKT) - Microframework web
* [Flask-SQLAlchemy ☁](https://flask-sqlalchemy.palletsprojects.com/?spm=a2ty_o01.29997173.0.0.7eb6c921qbBQKT)  - ORM para base de datos
* [Flask-Migrate ☁](https://flask-migrate.readthedocs.io/?spm=a2ty_o01.29997173.0.0.7eb6c921qbBQKT) - Migraciones de base de datos (Alembic)
* [Flask-Login ☁](https://flask-login.readthedocs.io/?spm=a2ty_o01.29997173.0.0.7eb6c921qbBQKT) - Gestión de sesiones de usuario
* [Flask-WTF ☁](https://flask-wtf.readthedocs.io/?spm=a2ty_o01.29997173.0.0.7eb6c921qbBQKT) - Formularios con validación
* [python-dotenv ☁](https://pypi.org/project/python-dotenv/?spm=a2ty_o01.29997173.0.0.7eb6c921qbBQKT) - Gestión de variables de entorno
* [Gunicorn ☁](https://gunicorn.org/?spm=a2ty_o01.29997173.0.0.7eb6c921qbBQKT) - Servidor WSGI para producción
* [pytest ☁](https://docs.pytest.org/?spm=a2ty_o01.29997173.0.0.7eb6c921qbBQKT) - Framework de pruebas
---
## 🤝 Contribuciones
Las contribuciones son bienvenidas. Por favor:
   + Fork el proyecto
   + Crea una rama para tu feature (git checkout -b feature/AmazingFeature)
   + Commit tus cambios (git commit -m 'Add some AmazingFeature')
   + Push a la rama (git push origin feature/AmazingFeature)
   + Abre un Pull Request