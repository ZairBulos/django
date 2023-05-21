# Uso de vistas genéricas en Django

Dado que Django se ha diseñado para aplicaciones controladas por datos, incluye numerosas utilidades integradas para simplificar la cantidad de código necesario. Un área clave donde Django facilita la vida del desarrollador es proporcionando vistas genéricas, que están generadas previamente con todo el código necesario para realizar operaciones básicas, como mostrar y editar datos. Veremos cómo se pueden usar las vistas genéricas para reducir considerablemente la cantidad de código necesario.

### Objetivos de aprendizaje

* Usar vistas genéricas.
* Crear formularios de Django.
* Usar la biblioteca django-crispy-forms.

### Requisitos previos

* Software
    - Visual Studio Code
    - Git
* Aptitudes de codificación
    - Conocimientos de HTML y CSS
    - Conocimientos básicos de Django
    - Conocimientos básicos de las bases de datos relacionales
    - Conocimientos de nivel intermedio de Python, incluido lo siguiente:
        - Administración de paquetes
        - Entornos virtuales
        - Herencia

<hr/>

## Introducción

Las aplicaciones controladas por datos a menudo comparten una estructura parecida. Tiene una página en la que se muestra una lista de los elementos, una página para mostrar los detalles de un elemento y, después, las páginas adecuadas para permitir la creación, las actualizaciones y las eliminaciones. Tener que crear cada una de estas páginas a mano puede resultar tedioso, especialmente porque gran parte del código y HTML es repetitivo.

Para ayudar a simplificar la creación de aplicaciones controladas por datos, Django proporciona vistas genéricas. Las vistas genéricas son vistas basadas en clases diseñadas para realizar todas estas operaciones comunes. Podemos usar vistas genéricas para crear rápidamente páginas con el fin de mostrar y editar datos. Estas vistas pueden incluso generar los formularios HTML de forma automática.

En este módulo, exploraremos las vistas y los formularios genéricos y cómo podemos usar una biblioteca común para mejorar la presentación de nuestros formularios.

<hr/>

## Ejercicio: Configuración del proyecto de inicio

En este módulo, trabajaremos en un sitio web de refugios para perros. Este proyecto se centra en recopilar información sobre los refugios para perros existentes y los perros que esperan ser adoptados en Estados Unidos. La esperanza ficticia de esta aplicación es que los perros podrían encontrar hogares adecuados con más rapidez, ya que habría personas de todo Estados Unidos que querrían adoptarlos, y no solo del área local del refugio.

Django es el marco perfecto para este proyecto. Proporciona una ruta para desarrollar rápidamente una aplicación orientada al cliente. Django también proporciona una función de administración y base de datos establecida a la que pueden acceder fácilmente los empleados para obtener una actualización rápida. Hemos creado la configuración inicial de este proyecto, lo que permite centrarse en los conceptos de este módulo.

### Clonación del repositorio de inicio

1. Abra un comando o una ventana de terminal.

2. Ejecute los comandos siguientes para clonar el repositorio de inicio y cambiar al directorio del proyecto.

    ```Bash
    git clone https://github.com/MicrosoftDocs/ms-learn-django-generic-views.git
    cd ms-learn-django-generic-views/starter
    ```

### Creación del entorno virtual

Seguiremos el procedimiento recomendado de trabajo con entornos virtuales para nuestro proyecto.

1. En Visual Studio Code, seleccione Ver>Terminal para abrir la ventana de terminal.

2. En la ventana del terminal, ejecute los comandos siguientes para crear y activar un entorno virtual.

    ```Bash
    # Windows
    py -3 -m venv venv
    .\\venv\\Scripts\\activate

    # macOS or Linux
    python3 -m venv venv
    source ./venv/bin/activate
    ```

### Instalación de Django

El proyecto de inicio usa un archivo requirements.txt para incluir la lista de todos los paquetes necesarios. Se pueden instalar mediante pip.

En la misma ventana del terminal, ejecute el comando siguiente para instalar los paquetes necesarios.

```Bash
pip install -r requirements.txt
```

### Inicio del servidor

Django puede hospedar la aplicación localmente. Haremos este paso mediante la ventana del terminal integrada en Visual Studio Code.

Escriba el comando siguiente en la misma ventana de terminal.

```Bash
python manage.py runserver
```

<hr/>

## Uso de vistas genéricas para mostrar datos

El sistema de vistas genéricas de Django simplifica la creación de código repetitivo. Las operaciones comunes que realiza en una aplicación controlada por datos comparten el mismo patrón. Por ejemplo, para mostrar un elemento individual por su id. o clave principal, el flujo de trabajo siempre es el siguiente:

1. Cargue el elemento de la base de datos por id.
2. Si no se encuentra el elemento, devuelve un mensaje de error 404.
3. Si se encuentra el elemento, páselo a una plantilla para mostrarlo.

El sistema de vistas genéricas confirma este hecho y proporciona clases que se pueden usar y que contienen el código principal ya escrito. Herede de la clase adecuada, establezca un par de propiedades y, después, registre una ruta adecuada en el elemento URLconf. El resto se hace de forma automática.

Django incluye dos vistas genéricas para mostrar datos: `DetailView` y `ListView`.

### DetailView para obtener el detalle del elemento

La vista genérica `DetailView` se usa para mostrar una página de detalles de un elemento. `DetailView` recupera el elemento del elemento `model` especificado por la clave principal y lo pasa a la plantilla. Puede establecer `template_name` en el nombre de la plantilla que se va a usar. De manera predeterminada, es `<model>_detail.html`. Por último, podemos establecer `context_object_name` en el nombre de la variable que se quiere usar en nuestra plantilla.

Para crear una vista de detalles de un perro mediante la vista genérica, podría usar el código siguiente:

```Python
from . import models
from django.views import generic

class DogDetailView(generic.DetailView):
    model = models.Dog
    template_name = 'dog_detail.html'
    context_object_name = 'dog'
```

El registro de `DogDetailView` es similar a cualquier otra entrada de `path`. El elemento clave para asegurarse de que se incluye es un parámetro denominado `pk`. Django usa esta convención para identificar la clave principal. También deberá tener en cuenta que usamos el método `as_view()` para convertir la clase en una vista.

```Python
path('dog/<int:pk>', views.DogDetailView.as_view(), name='dog_detail')
```

### ListView para obtener una lista de elementos

La vista genérica `ListView` se comporta de manera similar a `DetailView`. Puede establecer `context_object_name` para el nombre de la variable en la vista y `template_name` para el nombre de la plantilla.

La principal diferencia es que `ListView` está diseñada para trabajar con cualquier forma de una consulta que devuelve varios elementos. Como resultado, debe invalidar la función `get_queryset`. El sistema de vista genérico llama a la función `get_queryset` para recuperar los elementos de la base de datos, lo que permite ordenar o filtrar los elementos según sea necesario.

Para crear una vista que muestre la lista de todos los refugios mediante la vista genérica `ListView`, podría usar el código siguiente:

```Python
from . import models
from django.views import generic

class ShelterListView(generic.ListView):
    template_name = 'shelter_list.html'
    context_object_name = 'shelters'

    def get_queryset(self):
        return models.Shelter.objects.all()
```

El registro de la vista se realiza de forma muy similar a nuestro elemento `DetailView`.

```Python
path('', ShelterListView.as_view(), name='shelter_list')
```

<hr/>

## Ejercicio: Implementación de vistas genéricas para mostrar datos

Queremos crear una nueva página de detalles para perros. Vamos a usar la vista genérica `DetailView` para simplificar la cantidad de código que necesitamos crear.

### Creación de la vista DogDetail

Comenzaremos por crear la clase del vista de detalles.

1. En Visual Studio Code, abra *dog_shelters/views.py*.

2. Debajo de la línea que lee `# TODO: Import generic views`, agregue el código siguiente para importar el módulo de vistas genéricas.

    ```Python
    # TODO: Import generic views
    from django.views import generic
    ```

3. Agregue el código siguiente a la parte inferior de views.py a fin de crear la vista genérica para `DogDetail` y establecer el modelo, la plantilla y el objeto de contexto.

    ```Python
    class DogDetailView(generic.DetailView):
        model = models.Dog
        template_name = 'dog_detail.html'
        context_object_name = 'dog'
    ```

### Registro de la vista de detalles

Con la vista creada, podemos registrar la ruta.

1. Abra *dog_shelters/urls.py*.

2. Debajo de la línea que lee `# TODO: Register detail view`, agregue el código siguiente para registrar la ruta de nuestro elemento `DogDetailView`.

    ```Python
    # TODO: Register detail view
    path('dog/<int:pk>', views.DogDetailView.as_view(), name='dog_detail'),
    ```

### Creación de la plantilla HTML

Ahora creará la plantilla HTML para mostrar los detalles del perro. El nombre del objeto será dog, que lo establecimos al crear el formulario.

1. En Visual Studio Code, cree un archivo dentro de *dog_shelters/templates* denominado *dog_detail.html*.

2. Agregue el código siguiente a *dog_detail.html* para crear la plantilla para mostrar los detalles del perro.

    ```HTML
    {% extends 'base.html' %}

    {% block title %}
    {{ dog.name }}
    {% endblock %}

    {% block content %}
    <h2>{{ dog.name }}</h2>
    <div>About {{ dog.name }} - {{ dog.description }}</div>
    {% endblock %}
    ```

### Actualización de la página de detalles del refugio para incluir nuestro vínculo

Con nuestra ruta de acceso registrada y una plantilla creada, podemos actualizar la plantilla de detalles del refugio para incluir vínculos a nuestra página de detalles del perro.

1. Abra *dog_shelters/templates/shelter_detail.html*.

2. Debajo de la línea que lee `{# TODO: Add link to dogs #}`, agregue el código siguiente para crear un vínculo de cada perro a la vista de detalles.

    ```HTML
    {# TODO: Add link to dogs #}
    <a href="{% url 'dog_detail' dog.id %}">
        {{dog.name}}
    </a>
    ```

### Prueba de la página

Con todo lo creado, vamos a ver nuestra página en acción.

1. Guarde todos los archivos seleccionando **Archivo>Guardar todo**.

2. En el explorador, vaya a `http://localhost:8000`.

3. En la lista de refugios, seleccione **Contoso**.

4. En la lista de perros, seleccione **Roscoe**.

    Aparece la página de detalles.

    ![dog-detail](/images/05-dog-detail.png)

<hr/>

## Uso de vistas genéricas para editar datos

Al igual que ocurre con el código necesario para mostrar los datos, el código para permitir que los usuarios modifiquen los datos es repetitivo. También puede resultar tedioso, ya que se requieren varios pasos para asegurarse de que los datos son válidos y se envían correctamente. Afortunadamente, el sistema de vistas genéricas puede simplificar la cantidad de código que necesitamos para habilitar esta función.

### Creación de nuevos elementos

Antes de explorar la forma en la que Django puede optimizar nuestro desarrollo, deberíamos revisar el proceso que permite a los usuarios modificar datos. Vamos a explorar el flujo de trabajo que utiliza el servidor para administrar el proceso de creación de un nuevo elemento o fragmento de datos, y el trabajo que va a crear el formulario HTML.

### Flujo de trabajo de creación

A primera vista, el código para permitir que un usuario cree un elemento podría parecer trivial. Pero, por lo visto, se trata de un proceso aparentemente complicado.

1. El usuario envía una solicitud **GET** para indicar que quiere que el formulario cree un elemento.
2. El servidor envía el formulario con un token especial para evitar la [falsificación de solicitud entre sitios (CSRF)](https://en.wikipedia.org/wiki/Cross-site_request_forgery).
3. El usuario completa el formulario y selecciona Enviar, que envía una solicitud **POST** para indicar que el formulario se ha completado.
4. El servidor valida el token CSRF para asegurarse de que no se ha producido ninguna alteración.
5. El servidor valida toda la información para asegurarse de que cumple las reglas. En caso de que se produzca un error de validación, se devolverá un mensaje de error.
6. El servidor intenta guardar el elemento en la base de datos. Si se produce un error, se devuelve al usuario un mensaje de error.
7. Después de guardar correctamente el elemento nuevo, el servidor redirige al usuario a una página de éxito.

¡Este proceso requiere bastante código! La mayor parte de este es [reutilizable](https://en.wikipedia.org/wiki/Boilerplate_code), lo que significa que es el mismo cada vez que se crea.

#### Formularios

La creación de un formulario HTML puede ser un proceso tedioso. Los desarrolladores a menudo copian y pegan etiquetas `input`, recorren listas para crear listas desplegables y configuran botones de radio. Cada vez que el modelo cambia, debe actualizarse el formulario.

Es posible que haya observado que los modelos que creamos en Django contienen todo lo necesario para crear el formulario. Cuando agregamos los distintos campos, indicamos los tipos de datos, que se acoplan con distintos elementos HTML. Por ejemplo, un campo booleano sería una casilla y una clave externa normalmente sería una lista desplegable.

### Vistas genéricas para modificar datos

Uno de los objetivos clave de Django es eliminar la necesidad de volver a crear constantemente los mismos bloques de código una y otra vez. Para que este objetivo sea compatible con las modificaciones de datos, Django proporciona una recopilación de clases y formularios genéricos con el fin de administrar esta carga de trabajo. Como veremos, incluye todo el código necesario y puede incluso crear el formulario por nosotros dinámicamente. Las clases utilizadas para crear, actualizar y eliminar datos se denominan `CreateView`, `UpdateView` y `DeleteView` respectivamente.

#### CreateView

La clase `CreateView` se utiliza para permitir a los usuarios crear elementos. Le guía por el proceso anterior y crea dinámicamente el formulario. Una vez que se ha realizado correctamente, muestra la página de detalles del elemento recientemente creado.

Se debe especificar el elemento `model` y `template_name`que quiere asociar, tal como se haría con las otras vistas genéricas. La diferencia clave de `CreateView` es la inclusión de una propiedad `fields` en la que se muestra una lista de los campos modificables. Con esta propiedad, puede asegurarse de que los campos que no se deben editar, como una fecha de creación, no aparecen en el formulario. La vista para crear un perro podría ser similar a la del ejemplo siguiente:

```Python
from . import models
from django.views import generic

class DogCreateView(generic.CreateView):
    model = models.Dog
    template_name = 'dog_form.html'
    fields = ['name', 'description', 'shelter']
```

#### UpdateView

La clase `UpdateView` se comporta de manera idéntica a `CreateView`. La única diferencia es que carga automáticamente un elemento basado en el parámetro `pk`. Django usa esta convención para la clave principal de un elemento.

```Python
from . import models
from django.views import generic

class DogUpdateView(generic.CreateView):
    model = models.Dog
    template_name = 'dog_form.html'
    fields = ['name', 'description', 'shelter']
```

Después de crear o actualizar correctamente un elemento, Django redirige a la página de detalles del elemento. Recupera la dirección URL de los detalles mediante el uso de `get_absolute_url` en el modelo asociado. Para implementar este método, devuelva la dirección URL correcta. Puede recuperar la dirección URL apropiada de URLconf mediante reverse. Tenga en cuenta que `kwargs` se usa para pasar `pk` o el parámetro de clave principal o a la ruta.

```Python
from django.db import models
# TODO: Import reverse
from django.urls import reverse
class Dog(models.Model):
    # Existing code
    def get_absolute_url(self):
        return reverse('dog_detail', kwargs={"pk": self.pk})
```

#### DeleteView

La clase `DeleteView` es parecida a `UpdateView`. Permite a un usuario eliminar un elemento e identifica el elemento que se va a eliminar mediante `pk`. A diferencia de `UpdateView`, fields no se necesita porque se eliminará todo el elemento. Además, dado que no se ha creado ni actualizado ningún elemento recientemente, necesitamos determinar dónde queremos redirigir al usuario. Podemos crear un redireccionamiento estableciendo `success_url` en el valor adecuado. Puede buscar una dirección URL mediante `reverse_lazy`.

```Python
from . import models
from django.views import generic
from django.urls import reverse_lazy

class AuthorDelete(DeleteView):
    model = Author
    success_url = reverse_lazy('author-list')
```

> ℹ️ **Nota** <br/>
> Usamos `reverse_lazy` debido al orden en que se carga la información en Django.

### Plantillas de formulario para crear y actualizar

Las vistas genéricas pueden crear el formulario HTML por nosotros dinámicamente. Todo lo que debemos proporcionar es una plantilla que actúe como el marcador de posición del formulario. La plantilla de marcador de posición garantiza que el formulario coincida con el resto de nuestro sitio. Afortunadamente, no necesitamos mucho código para crearla.

Las vistas genéricas crean automáticamente una variable `form` para que la use nuestra plantilla. Los elementos del formulario que proporciona Django se pueden mostrar dentro de las etiquetas `<p>` o como un elemento `<table>`.

La variable `form` contiene todo el HTML adecuado para crear los controles del formulario. No contiene la propia etiqueta `<form>` o un botón de envío. Nuestra plantilla debe incluir cuatro elementos:

- El elemento `form` con `method` establecido en **POST**, porque esta configuración desencadena la operación de almacenamiento en el servidor.
- El código `{% csrf_token %}` para agregar el token CSRF a fin de evitar la suplantación de identidad.
- El código `{{ form.as_p }}` o `{{ form.as_table }}` para mostrar el formulario generado de forma dinámica.
- El botón submit.

El código siguiente puede actuar como el host para cualquier formulario de vista genérica.

```HTML
<form method="post">{% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Save</button>
</form>
```

<hr/>

## Ejercicio: Implementación de vistas genéricas para editar datos

Para permitir que los usuarios registren nuevos perros en un refugio, usaremos `CreateView`.

### Actualización del modelo para admitir get_absolute_url

Comencemos por actualizar el modelo para que sea compatible con `get_absolute_url`.

1. En Visual Studio Code, abra *dog_shelters/models.py*.

2. Agregue el código siguiente debajo de la línea que lee `# TODO: Import reverse` para importar la función `reverse`.

    ```Python
    # TODO: Import reverse
    from django.urls import reverse
    ```

3. Agregue el código siguiente a la clase `Dog` inmediatamente en la línea que lee `# TODO: Add get_absolute_url` para leer la ruta `dog_detail` de URLconf y pasar el identificador como parámetro.

```Python
# TODO: Add get_absolute_url
    def get_absolute_url(self):
        return reverse('dog_detail', kwargs={"pk": self.pk})
```

### Creación de DogCreateView

Vamos a crear DogCreateView para permitir que alguien pueda registrar un perro.

1. En Visual Studio Code, abra *dog_shelters/views.py*.

2. Al final de *views.py*, agregue el código siguiente para crear `DogCreateView`.

    ```Python
    class DogCreateView(generic.CreateView):
        model = models.Dog
        template_name = 'dog_form.html'
        fields = ['shelter', 'name', 'description']
    ```

Establecemos el modelo para que sea `Dog`, nuestra plantilla para que sea *dog_form.html* y la lista de campos que queremos que se puedan editar.

> ℹ️ **Nota** <br/>
> El orden en que se enumeran los campos será el orden en que se mostrarán en el formulario.

### Registro de la ruta

Una vez creada la vista, registraremos la ruta en nuestro elemento URLconf.

1. En Visual Studio Code, abra *dog_shelters/urls.py*.

2. Debajo de la línea que lee `# TODO: Register create view`, agregue el código siguiente para registrar la ruta.

    ```Python
    # TODO: Register create view
    path('dog/register', views.DogCreateView.as_view(), name='dog_register'),
    ```

### Creación de la plantilla HTML

Vamos a crear la plantilla para hospedar nuestro formulario.

1. En Visual Studio Code, cree un archivo dentro de *dog_shelters/templates* denominado *dog_form.html*.

2. Agregue el código siguiente a *dog_form.html* para crear la plantilla que hospedará el formulario.

    ```HTML
    {% extends 'base.html' %}

    {# TODO: Register crispy_forms_tags #}

    {% block title %}
    Register dog at shelter
    {% endblock %}

    {% block content %}
    <h2>Register dog at shelter</h2>
    <form method="POST">
        {% csrf_token %}

        {{ form.as_p }}

        <button type="submit" class="btn btn-primary">Save</button>
    </form>
    {% endblock %}
    ```

### Creación de un vínculo a la página de registro

Vamos a crear un vínculo en nuestra página de lista de refugios, que actualmente es la página principal de nuestra aplicación, a la página de registro que hemos creado.

1. En Visual Studio Code, abra *dog_shelters/templates/shelter_list.html*.

2. Debajo de la línea que lee `{# TODO: Add link to registration page #}`, agregue el código siguiente para crear el vínculo.

    ```HTML
    {# TODO: Add link to registration page #}
    <div>
        <a href="{% url 'dog_register' %}">Register a dog available for adoption</a>
    </div>
    ```

### Prueba de la página

Veamos la página en acción.

1. Guarde todos los archivos; para ello, seleccione **Archivo>Guardar todo**.

2. En el explorador, vaya a `http://localhost:8000`.

3. Seleccione **Register a dog available for adoption**.

    Ahora debería ver el formulario.

    ![dog-register](/images/05-dog-register.png)

    Observe cómo nuestra relación de clave externa se convierte en una lista desplegable.

4. Elija un refugio y agregue un nombre y una descripción para un perro.

5. Seleccione Guardar.

    Ahora se le redirigirá a la página de detalles del perro.

Ya ha creado un formulario de creación mediante `CreateView` en Django.

<hr/>

## Ejercicio: Implementación de django-crispy-forms

Después de ver el formulario creado, es posible que observe que el formato no es el mismo que en el resto de la página. Estamos usando Bootstrap, pero el formulario todavía no. Afortunadamente, existe una biblioteca que puede garantizar que nuestros formularios también usan Bootstrap.

### La biblioteca django-crispy-forms

La biblioteca [django-crispy-forms](https://django-crispy-forms.readthedocs.io/en/latest/) mejora el modo en que Django genera los formularios. Vamos a explorar cómo podemos usar la biblioteca para asegurarse de que los formularios usan Bootstrap.

### Instalación de la biblioteca

Al igual que con cualquier biblioteca de Python, **django-crispy-forms** se instala con PIP.

1. En Visual Studio Code, abra *requirements.txt*.

2. En la parte inferior del archivo, agregue una nueva línea que lea lo siguiente:

    ```text
    django-crispy-forms
    ```

3. Seleccione **Terminal>Nuevo terminal** para abrir una ventana del terminal nueva.

4. Instale todos los paquetes mediante la ejecución del comando siguiente:

    ```Bash
    pip install -r requirements.txt
    ```

### Registro de la aplicación en Django y configuración de la plantilla

Cualquier cosa que Django use debe estar registrada como aplicación o middleware. Dado que django-crispy-forms es una aplicación, la mostraremos en la lista `INSTALLED_APPS`.

1. En Visual Studio Code, abra *project/settings.py*.

2. Debajo de la línea que lee `# TODO: Register crispy_forms`, agregue el código siguiente para registrar django-crispy-forms.

    ```Python
    # TODO: Register crispy_forms
    'crispy_forms',
    ```

3. Debajo de la línea que lee `# TODO: Set template_pack`, agregue el código siguiente para configurar django-crispy-forms a fin de que use Bootstrap 4.

    ```Python
    # TODO: Set template_pack
    CRISPY_TEMPLATE_PACK = 'bootstrap4'
    ```

### Actualización de la plantilla para usar django-crispy-forms

La mayor parte del fabuloso trabajo que realiza django-crispy-forms lo hace con un filtro. Un filtro permite tomar una variable en una plantilla y pasarla a otro controlador o proceso. En nuestro caso, el filtro `crispy` convertirá el formulario en la plantilla especificada, Bootstrap 4.

1. En Visual Studio Code, abra *dog_shelters/templates/dog_form.html*.

2. Debajo de la línea que lee `{# TODO: Load crispy_forms_tags #}`, agregue el código siguiente para cargar el filtro o la etiqueta.

    ```HTML
    {# TODO: Load crispy_forms_tags #}
    {% load crispy_forms_tags %}
    ```

3. Reemplace la línea que lee `{{ form.as_p }}` por el código siguiente para usar el filtro `crispy`.

    ```HTML
    {{ form | crispy }}
    ```

### Prueba del sitio

Una vez que todo está instalado y actualizado, vamos a probar nuestro sitio.

1. Guarde todos los archivos; para ello, seleccione Archivo>Guardar todo.

2. En el explorador, vaya a `http://localhost:8000/dog/register`.

    Verá que el formulario de la página ahora usa Bootstrap.

    ![dog-register-bootstrap](/images/05-dog-register-bootstrap.png)