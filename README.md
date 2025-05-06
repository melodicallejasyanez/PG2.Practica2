## Requisitos previos
- Python 3.12 instalado
- pip

## Crear entorno virtual
1. Abrir la terminal en el directorio del proyecto
2. Ejecutar el siguiente comando a continuación:

bash
python -m venv venv

Esto permitirá crear un directorio llamado env en el entorno virtual.

## Activar entorno virtual

* *Windows:*
bash
.\env\Scripts\activate


* *Linux/Mac:*
bash
source env/bin/activate

Después de activar el entorno virtual, (env) se mostrará al inicio de la linea de comandos.

## Instalar dependencias
Tras la activación del entorno virtual, usa pip para instalar las dependencias del proyecto:

bash
pip install -r requirements.txt

## Desactivar entorno virtual
Cuando hayas terminado de trabajar en el proyecto, puedes desactivar el entorno virtual para volver a tu entorno global con este simple comando.

bash
deactivate


## Crear proyecto Django
Para iniciar un nuevo proyecto, ejecuta:

bash
django-admin startproject practica2 .


## Aplicar migraciones
Aplica los cambios definidos a la base de datos mediante:

bash
python manage.py migrate


## Iniciar servidor
Inicia el servidor de desarrollo para ver tu aplicación en funcionamiento con:

bash
python manage.py runserver


## Crear superusuario
Crea un usuario con privilegios de administrador para gestionar su sitio Django
bash
python manage.py createsuperuser


## Crear aplicación
Utiliza este comando para generar la estructura de archivos de la nueva aplicación. 

bash
python manage.py startapp libros


## Agregar aplicación a settings.py
En este punto es enecesario agregar el nombre de libros a la lista INSTALLED_APPS dentro del archivo settings.py del proyecto, lo que informa a Django que esta aplicación debe ser tenida en cuenta.

python
INSTALLED_APPS = [
    ...
    'libros',
]


## Crear modelo

Escribe el modelo en libros/models.py:

python
from django.db import models

class Autor(models.Model):
    nombre = models.CharField(max_length=100)
    fecha_nacimiento = models.DateField()

    def __str__(self):
        return self.nombre

class Libro(models.Model):
    titulo = models.CharField(max_length=100)
    autor = models.ForeignKey(Autor, on_delete=models.CASCADE, related_name="libros")
    fecha_publicacion = models.DateField()

    def __str__(self):
        return self.titulo


## Crear migraciones

bash
python manage.py makemigrations


## Aplicar migraciones

bash
python manage.py migrate


## Configurar admin.py

Escribe el siguiente código en libros/admin.py:

python
from django.contrib import admin
from .models import Autor, Libro

admin.site.register(Autor)
admin.site.register(Libro)


## Iniciar servidor

bash
python manage.py runserver


## Acceder al panel de administración

Abre tu navegador y ve a http://localhost:8000/admin/. Inicia sesión con el
superusuario que creaste anteriormente. Deberías ver las opciones para agregar
autores y libros.