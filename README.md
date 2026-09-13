# Sesión 1 — Desarrollo de una aplicación Web con Django

Proyecto Django de la primera sesión del laboratorio. Implementa una aplicación
`core` con un modelo `Item` registrado en el panel de administración y una
página principal que lista los items, siguiendo la estructura de carpetas del
curso.

## Requisitos

- Python 3.12 o superior
- Git

## Estructura del proyecto

```
sesion1-djangoIA/
├── src/
│   ├── manage.py
│   ├── config/          # configuración del proyecto
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── wsgi.py
│   │   └── asgi.py
│   └── core/            # aplicación propia del laboratorio
│       ├── migrations/
│       ├── templates/
│       │   ├── base.html
│       │   └── core/item_list.html
│       ├── admin.py
│       ├── models.py
│       ├── urls.py
│       └── views.py
├── venv/                # entorno virtual (no se sube a git)
├── .gitignore
├── requirements.txt
└── README.md
```

## Configuración del entorno

```bash
# 1. Crear el entorno virtual aislado
python -m venv venv

# 2. Activarlo
venv\Scripts\activate        # Windows
source venv/bin/activate     # Linux/macOS

# 3. Instalar las dependencias
pip install -r requirements.txt

# 4. Aplicar las migraciones
python src/manage.py migrate

# 5. Crear el superusuario (en este lab: admin / admin123)
python src/manage.py createsuperuser

# 6. Levantar el servidor de desarrollo
python src/manage.py runserver
```

Abrir `http://127.0.0.1:8000/` para ver el listado de items y
`http://127.0.0.1:8000/admin/` para el panel de administración.

## Código del entorno de desarrollo

Superusuario local de pruebas (solo desarrollo):

- Usuario: `admin`
- Contraseña: `admin123`

## Observaciones

- El proyecto sigue la estructura de la guía: el proyecto se genera con
  `django-admin startproject config .` dentro de `src/`, dejando `manage.py` en
  `src/` y la configuración en `config/`.
- La aplicación `core` fue creada con `python manage.py startapp core` y quedó
  declarada en `INSTALLED_APPS` de `src/config/settings.py`. Las vistas, rutas,
  modelos, migraciones, admin y plantillas viven dentro de la app y no en el
  paquete del proyecto.
- La vista `item_list` recupera los items y los pasa a la plantilla
  `core/item_list.html`, que extiende `base.html` y recorre los items con un
  `for`, incluyendo el caso vacío.
- Se agregaron `.gitignore`, `requirements.txt` y este README. Las dependencias
  quedan declaradas en `requirements.txt`, los archivos generados
  (`db.sqlite3`, `__pycache__`, `venv/`) están excluidos del repositorio y el
  historial de git muestra el avance por etapas en commits pequeños.
- Las credenciales no se escriben a mano en `settings.py`; `SECRET_KEY` es la
  que genera Django para desarrollo y no se usa en producción.
- Sesión corregida: la primera entrega tenía la vista dentro del paquete del
  proyecto y no incluía app propia; en esta versión la app `core` concentra toda
  la lógica del laboratorio.