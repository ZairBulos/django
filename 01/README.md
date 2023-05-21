# Introducción a Django

Django es uno de los marcos web de Python más populares. Es especialmente eficaz cuando se trabaja con una aplicación controlada por datos, donde el objetivo principal es proporcionar un front-end a una base de datos. Django incluye numerosas características integradas para simplificar el proceso de desarrollo. En este módulo, exploramos las ventajas de Django, cómo se instala y cómo crear su primer proyecto.

### Objetivos de aprendizaje

* Por qué Django es excelente para la implementación rápida de aplicaciones web.
* La diferencia entre Django y Flask.
* Qué tipos de aplicaciones son los más adecuados para Django.
* Los procedimientos para instalar Django.
* Los procedimientos para crear un sitio web en Django.

### Requisitos previos

* Visual Studio Code
* Git
* Conocimientos de HTML y CSS
* Conocimientos de nivel intermedio de Python, incluido lo siguiente:
    - Administración de paquetes
    - Entornos virtuales
    - Herencia

<hr/>

## Introducción

Django es un conocido marco web del lado servidor. Su principal enfoque se centra en los sitios web controlados por datos con utilidades necesarias de forma frecuente y previamente integradas en la plataforma. Django se basa en Python. Ofrece flexibilidad y una colección de extensiones compiladas por la comunidad.

En este módulo se presenta Django. Para ayudarle a entender el marco de Django, le guiaremos por los tipos de aplicaciones más adecuadas para la implementación, la instalación y la creación del primer programa.

<hr/>

## ¿Qué es Django?

Django, pronunciado "yango", es un marco gratuito y de código abierto que se lanzó por primera vez en 2005. Django recibe su nombre del famoso guitarrista de jazz, Django Reinhardt. A lo largo de los años, se han desarrollado muchos marcos de Python, pero Django se ha convertido en uno de los más populares debido a su flexibilidad y seguridad.

Django es adecuado para el desarrollo web tanto de front-end como de back-end. Las bibliotecas de Python integradas facilitan el desarrollo rápido. Django se ha aceptado ampliamente en distintos sectores empresariales. Debido a su popularidad creciente, los proveedores están más predispuestos a admitir aplicaciones de Django en sus plataformas.

### Tipos de aplicación

Django ofrece una solución completa de marco, lo que significa que le proporciona todo lo que necesita para implementar rápidamente sus proyectos. Django ofrece una excelente seguridad de serie y una amplia comunidad de usuarios. Además, se puede escalar a petición. Por estos motivos, muchos desarrolladores lo consideran el marco de preferencia. Mediante el uso de Django, se pueden desarrollar aplicaciones web complejas y controladas por bases de datos que pueden incluir lo siguiente:

- Machine Learning
- Plataformas de comercio electrónico
- Análisis de datos
- Administración de contenido

### Django frente a Flask

Aunque ambos marcos podrían adaptarse a las necesidades de la siguiente aplicación de Python, existen funciones y niveles de compatibilidad específicos que proporciona cada uno de ellos. Vamos a repasar rápidamente las diferencias.

| Django                                         | Flask                                                |
| ---------------------------------------------- | ---------------------------------------------------- |
| Marco de pila completo	                     | Marco web ligero                                     |
| Ideal para aplicaciones controladas por datos	 | Ideal para API y servicios existentes                |
| Posiblemente más como una curva de aprendizaje | Posiblemente menos como una curva de aprendizaje     |
| Seguridad de serie	                         | Bibliotecas adicionales necesarias para la seguridad |  
| Motor de plantillas HTML personalizado	     | Motor de plantillas HTML Jinja                       |

Tanto Django como Flask ofrecen grandes ventajas para sus proyectos. En función de los requisitos de tiempo para el desarrollo de aplicaciones, es posible que uno sea más adecuado que el otro. Cuando elija un marco, tenga en cuenta el tipo y la complejidad de la aplicación, así como el producto final.

<hr/>

## Ejercicio: Instalación de Django

La creación de un proyecto de Django es similar a la de cualquier aplicación de Python. Comenzaremos por crear una carpeta y, después, instalaremos el paquete mediante `pip`.

### Introducción a la instalación

Antes de instalar Django, asegúrese en primer lugar de que la versión correcta de Python está instalada para el marco. Para comprobar la versión instalada, vaya al símbolo del sistema y escriba el comando siguiente:

```Bash
# Windows
python --version 

# macOS or Linux
python3 --version
```

### Creación de la carpeta del proyecto

Antes de descargar Django, cree un entorno virtual para aislarlo de otras aplicaciones. Si no se crea un entorno virtual y el marco se instala globalmente, podría producirse un conflicto con otras aplicaciones de Python, lo que provocaría un error.

Empiece por crear una carpeta para incluir el proyecto nuevo. También conservará la carpeta para el entorno virtual.

1. Abra un comando o una ventana de terminal.
2. Cree un directorio llamado *hello_django* y vaya a ese directorio.
3. Use el comando siguiente para abrir la carpeta en Visual Studio Code: `code .`

### Creación y activación del entorno virtual

Usaremos el terminal integrado en Visual Studio Code para evitar el cambio de ventanas mientras ejecutamos los comandos necesarios a fin de crear los recursos que necesitamos. Comenzaremos por la creación de un [entorno virtual](https://packaging.python.org/tutorials/installing-packages/#creating-virtual-environments) y su activación.

1. En Visual Studio Code seleccione **Terminal>Nuevo terminal**.

2. En la ventana de terminal de la parte inferior de Visual Studio Code, ejecute los comandos siguientes para crear y activar su entorno virtual.

    ```Bash
    # Windows
    python -m venv venv
    .\\venv\\Scripts\\Activate

    # macOS or Linux
    python3 -m venv venv
    source ./venv/bin/activate
    ```

    El nombre del entorno virtual estará entre paréntesis, seguido de la ruta en la que se encuentra actualmente. Este símbolo del sistema es donde comenzará a instalar el marco de Django.

### Instalación de Django

La forma más común de administrar paquetes de Python es mediante el uso de un archivo [requirements.txt](https://pip.pypa.io/en/latest/user_guide/#requirements-files). En el archivo requirements.txt se muestra una lista de los paquetes que utiliza la aplicación. Vamos a crear el archivo requirements.txt, a agregar Django y, después, a instalar la biblioteca.

1. En Visual Studio Code, cree un archivo denominado *requirements.txt* dentro de la carpeta *hello_django*.

2. Agregue el texto siguiente a *requirements.txt*.

    ```text
    Django
    ```

3. Dentro de la ventana de terminal, ejecute el comando siguiente para instalar Django y cualquier otro paquete que figure en *requirements.txt*.

    ```Bash
    pip install -r requirements.txt
    ```

Con este comando, el marco de Django comenzará a descargarse. Una vez finalizada la descarga, podemos empezar a desarrollar la aplicación.

<hr/>

## Exploración de los conceptos básicos en Django

Ahora que Django está instalado, vamos a examinar algunos conceptos clave y a detectar la diferencia entre un proyecto y una aplicación.

### Proyectos frente a aplicaciones

| Proyecto                                                                         | Aplicación
| -------------------------------------------------------------------------------- | ----------------------------------------------------- |
| Solo hay un proyecto.	                                                           | Puede haber muchas aplicaciones en el proyecto único. |
| Incluye la configuración o aplicaciones necesarias para un sitio web específico. | Es un componente del sitio web de mayor tamaño.       |
| Los proyectos no se usan en otros proyectos.	                                   | Las aplicaciones pueden usarse en varios proyectos.   |

### Vistas

Las vistas son otro componente de las aplicaciones de Django que cumplen una función específica en la aplicación. Las vistas incluyen todo el código necesario que devolverá una respuesta específica cuando se solicite, como una plantilla o una imagen. Incluso pueden redirigirse a otra página en caso de que la solicitud no siga la lógica necesaria en la función.

### Asignación de la URL

A la asignación de direcciones URL en Django se le llama `URLconf` y sirve como tabla de contenido para la aplicación. Una vez solicitada una dirección URL, este módulo busca el vínculo adecuado en el proyecto y redirige la solicitud al archivo de vistas incluido en la aplicación. Después, la vista procesa la solicitud y realiza las operaciones necesarias.

A medida que siga obteniendo información y cuente con estructuras de archivos más complejas, agregará más vistas y direcciones URL para la aplicación. La función `URLconf` desempeña un papel clave porque permite disponer de una manera sencilla de administrar y organizar las direcciones URL en la aplicación. También proporciona mayor libertad para cambiar las raíces de ruta sin interrumpir la aplicación.

<hr/>

## Creación del primer proyecto

Ahora que hemos explorado algunos conceptos básicos de Django, vamos a empezar a crear el proyecto.

### Creación de un proyecto con django-admin

al como se ha resaltado anteriormente, un proyecto de Django es el contenedor para todo el proyecto y cualquier aplicación que vayamos a crear. Vamos a crear nuestro proyecto.

Ejecute el comando siguiente dentro de la ventana del terminal en Visual Studio Code:

```Bash
django-admin startproject helloproject .
```

> ❗ **Importante** <br/>
> El punto final del comando es importante. Indica a `django-admin` que use la carpeta actual. Si deja fuera este punto final, se creará un subdirectorio adicional.

Después de ejecutar el comando anterior, el proyecto nuevo debe estar ahora en el directorio elegido. En esta instancia, verá una carpeta nueva denominada *helloproject*.

### Exploración de la estructura del proyecto
 
Ahora que se ha creado el proyecto de Django, echemos un vistazo a la estructura para ver lo que se ha incluido en él.

```text
manage.py
helloproject/
    __init__.py
    asgi.py
    settings.py
    urls.py
    wsgi.py
```

- La utilidad de la línea de comandos [manage.py](https://docs.djangoproject.com/en/3.1/ref/django-admin) se crea en cada proyecto de Django. Tiene la misma función que django-admin. En el ejemplo siguiente se muestra cómo se podría usar si estuviera en la carpeta del proyecto y quisiera ver los subcomandos disponibles.

    ```Bash
    python manage.py help
    ```

- *helloproject* se considera como el paquete de Python para el proyecto.

- *init.py* es un archivo vacío que funciona para indicar a Python que este directorio se debe considerar como un paquete.

- *settings.py* incluye todos los valores o configuraciones.

- *urls.py* incluye las direcciones URL del proyecto.

- *asgi.py* y *wsgi.py* sirven como punto de entrada para los servidores web en función del tipo de servidor implementado.

### Ejecución del proyecto

Ahora que Django está instalado, se ha creado un proyecto y hemos examinado su estructura, es el momento de asegurarse de que nuestro proyecto funciona correctamente.

1. Dentro de la ventana del terminal en Visual Studio Code, escriba el código siguiente para iniciar el servidor.

    ```Bash
    python manage.py runserver
    ```

    El proyecto realiza comprobaciones del sistema e inicia el servidor de desarrollo. Copie y pegue la dirección URL del servidor de desarrollo, que debe ser `http://localhost:8000`, en el explorador que prefiera. Debería ver una página Congratulations (Enhorabuena) en Django con una imagen de un cohete despegando.

2. Detenga el servidor temporalmente, ya que será necesario volver a configurar nuestro proyecto. Dentro de la ventana del terminal, seleccione `Ctrl+C`.

### Creación de la aplicación Hola mundo

Hemos descubierto los aspectos básicos sobre el marco de Django y examinado la estructura de carpetas de nuestro proyecto. Ahora es el momento de crear nuestra primera aplicación. La aplicación ¡Hola mundo! permitirá comprender cómo se crean las aplicaciones y cómo funcionan al unísono con el proyecto de Django.

Desde la ventana del terminal, ejecute el comando siguiente para crear la aplicación.

```Bash
python manage.py startapp hello_world
```

Con este comando, Django crea las carpetas y los archivos necesarios, y la estructura siguiente ahora debería estar visible.

```text
hello_world/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

### Registro de la aplicación en el proyecto

Dado que las aplicaciones y los proyectos son independientes en Django, debe registrar la aplicación en el proyecto. Para ello, se actualiza la variable `INSTALLED_APPS` dentro de *settings.py* en el proyecto y se agrega una referencia a la clase config para la aplicación. La clase config se encuentra en *apps.py* y tiene el mismo nombre que el proyecto. En nuestro ejemplo, la clase se llamará `HelloWorldConfig`.

1. Dentro de *helloproject*, abra *settings.py.*

2. Busque la lista `INSTALLED_APPS`, que debe estar en la línea 33.

3. Agregue lo siguiente al final de la lista, entre corchetes (`[ ]`):

    ```Python
    'hello_world.apps.HelloWorldConfig',
    ```

4. La lista `INSTALLED_APPS` actualizada debería ser similar a:

    ```Python
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'hello_world.apps.HelloWorldConfig',
    ]
    ```

5. Guarde todos los archivos; para ello, seleccione **Archivo>Guardar todo**.

<hr/>

## Descripción de las rutas y las vistas

Las vistas y rutas son fundamentales para cualquier marco web. Se usan para determinar qué información se debe mostrar al usuario y cómo accederá a ella. En Django también se usan estos conceptos.

### Rutas de acceso

Todas las aplicaciones permiten a los usuarios ejecutar métodos o funciones diferentes mediante determinados mecanismos. Esta acción podría pulsar un botón de una aplicación móvil o ejecutar un comando desde la línea de comandos.

Para realizar solicitudes de usuario en una aplicación web, haga lo siguiente:

- Navegar a distintas direcciones URL.
- Escribir en ella.
- Seleccionar un vínculo.
- Pulsar un botón.

Una ruta indica a Django qué función se va a ejecutar si el usuario realiza una solicitud para una dirección URL, o ruta, determinada.

Una dirección URL como `https://adventure-works.com/about` podría ejecutar una función denominada **about**. La dirección URL `https://adventure-works.com/login` podría ejecutar una función denominada **authenticate**.

Las rutas en Django se registran mediante la configuración de `urlpatterns`. Estos patrones identifican qué debe buscar Django en la dirección URL que el usuario solicita y determinan la función que debe controlar la solicitud. Estos patrones se recopilan en un módulo que Django denomina `URLconf`.

### Vistas

Las vistas determinan qué información se debe devolver al usuario. Las vistas son funciones o clases que ejecutan código en respuesta a la solicitud del usuario. Devuelven HTML u otros tipos de respuestas, como un error 404.

<hr/>

## Creación de rutas y vistas

Una vez creada la estructura de la aplicación, podemos empezar a seguir los pasos para agregar nuestro propio código personalizado. Crearemos una vista y, después, registraremos una ruta dentro de un elemento `URLconf`.

### Crear la vista

1. Dentro de Visual Studio Code, abra *views.py*, que estará dentro de *hello_world*.

2. Reemplace el código que hay dentro de views.py por el siguiente:

    ```Python
    from django.shortcuts import render
    from django.http import HttpResponse

    def index(request):
        return HttpResponse("Hello, world!")
    ```

    La función auxiliar `HttpResponse` permite devolver texto u otros tipos primitivos al autor de la llamada.

> ℹ️ **Nota** <br/>
> Al abrir *views.py*, es posible que reciba un mensaje de Visual Studio Code que le pida que instale **PyLint**. Si recibe este mensaje, seleccione Install PyLint (Instalar PyLint).

### Creación de la ruta

Una vez creada la vista, el paso siguiente consiste en asignarla a la dirección URL o ruta adecuada.

1. Dentro de Visual Studio Code, cree un archivo en *hello_world* denominado *urls.py*.

2. Agregue el código siguiente al archivo *urls.py nuevo.

    ```Python
    from django.urls import path
    from . import views

    urlpatterns = [
        path('', views.index, name='index'),
    ]
    ```

La parte más importante de este código es la tupla `urlpatterns`. Esta tupla es donde las vistas y las direcciones URL están conectadas o asignadas. Tal como se puede ver, hemos importado nuestro archivo views.py para poder usarlo en la línea `urlpatterns`.

### Registro de nuestro elemento `URLconf` con el proyecto

Nuestro elemento `URLconf` recientemente creado está dentro de nuestra aplicación *hello_world*. Dado que el proyecto controla todas las solicitudes de los usuarios, es necesario registrar nuestro elemento `URLconf` en el archivo principal *urls.py*, que está dentro de *helloproject*.

1. Abra *urls.py* dentro de *helloproject*.

2. Anote al principio los comentarios del documento. Estos comentarios explican cómo se pueden registrar módulos de `URLconf` nuevos.

3. Reemplace la línea que lee `from django.urls import path` con la instrucción import siguiente para agregar include y path.

    ```Python
    from django.urls import include, path
    ```

    El uso de `include` nos permite importar módulos de `URLconf`, y path se usa para identificar la raíz de `URLconf`.

4. Dentro de la lista, debajo de la línea que lee urlpatterns = [, agregue el código siguiente:

    ```Python
    path('', include('hello_world.urls')),
    ```

    Este código registra nuestro elemento `URLconf`.

El código que se encuentra debajo del comentario del documento ahora debe tener el aspecto siguiente:

```Python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('', include('hello_world.urls')),
    path('admin/', admin.site.urls),
]
```

### Ejecución de la primera aplicación

La estructura se ha completado, se han agregado vistas y se han asignado las direcciones URL. Ahora es el momento de ejecutar la aplicación.

1. Dentro de la ventana del terminal en Visual Studio Code, ejecute el comando siguiente para iniciar de nuevo el servidor.

    ```Bash
    python manage.py runserver
    ```

2. Abra la dirección URL en su explorador favorito: `http://localhost:8000/`

    Debería ver Hello, world! en la ventana del explorador.