# Trabajo con modelos y datos en Django

Django se centra en las aplicaciones controladas por datos, por lo que proporciona su propio asignador relacional de objetos (ORM). Exploraremos los conceptos de ORM y cómo funciona el ORM de Django. Crearemos nuestros propios modelos y configuraremos la base de datos.

### Objetivos de aprendizaje

* El propósito de un ORM.
* Cómo configurar y activar la base de datos de SQLite de Django.
* Cómo crear y activar modelos de Django.
* Por qué el método `__str__` es una adición importante en las clases.
* Cómo crear y consultar datos en la base de datos de SQLite.

### Requisitos previos

* Software
    - Visual Studio Code
    - Git
* Aptitudes de codificación
    - Conocimientos de HTML y CSS
    - Conocimientos básicos de Django
    - Conocimientos básicos de las bases de datos relacionales
    - Conocimientos intermedios de Python, incluido lo siguiente:
        - Administración de paquetes
        - Entornos virtuales
        - Herencia

<hr/>

## Introducción

Aunque es posible crear aplicaciones que interactúen directamente con una base de datos relacional, esta interacción directa puede conducir a código duplicado y poco seguro. Para solventar este problema, se introdujeron los asignadores relacionales de objetos (ORM), que separan las llamadas de base de datos de los objetos.

Como desarrollador, puede usar los ORM para diseñar objetos que representen los datos. Los ORM también pueden administrar las operaciones de la base de datos.

Django tiene un ORM integrado, que es un componente básico del marco. En este módulo, exploraremos el ORM de Django, cómo crear objetos de modelo y cómo interactuar con la base de datos mediante el ORM.

<hr/>

## Ejercicio: Configuración del proyecto e instalación de Django

En este módulo, trabajaremos en un sitio web de refugios para perros. Este proyecto se centra en recopilar información sobre todos los refugios de perros existentes y los perros que esperan ubicar en Estados Unidos. La esperanza ficticia de esta aplicación es que los perros podrán encontrar hogares adecuados con más rapidez, ya que habrá personas de todo Estados Unidos que quieran adoptarlos, y no solo de su área local.

Django es un buen marco para este proyecto porque proporciona una ruta para desarrollar rápidamente una aplicación orientada al cliente. También proporciona una función de administración y base de datos establecida a la que pueden acceder fácilmente los empleados para obtener una actualización rápida. Hemos creado la configuración inicial del proyecto para poder centrarnos en los conceptos de este módulo.

### Clonación del repositorio de inicio

1. Abra una ventana de comandos o terminal.
2. Ejecute los comandos siguientes para clonar el repositorio de inicio y cambiar al directorio del proyecto.

    ```Bash
    git clone https://github.com/MicrosoftDocs/mslearn-django-models-data
    cd mslearn-django-models-data/starter
    ```

### Creación del entorno virtual

Seguiremos el procedimiento recomendado de trabajo con entornos virtuales para nuestro proyecto.

1. En Visual Studio Code, seleccione Ver>Terminal para abrir la ventana de terminal.
2. En la nueva ventana de terminal, ejecute los comandos siguientes para crear y activar un entorno virtual:

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

En la misma ventana de terminal, ejecute el comando siguiente para instalar los paquetes necesarios:

```Bash
pip install -r requirements.txt
```

### Inicio del servidor

Django puede hospedar la aplicación localmente. Para ello, usaremos la ventana de terminal integrada en Visual Studio Code.

Escriba el comando siguiente en la misma ventana de terminal.

```Bash
python manage.py runserver
```

<hr/>

## Asignador relacional de objetos de Django

Trabajar con una base de datos relacional requiere una mentalidad diferente de la que requiere el trabajo con objetos en una aplicación. Cambiar entre estos dos entornos puede ralentizar el proceso de creación de una aplicación. Además, para convertir los resultados de las consultas de una base de datos en datos que la aplicación pueda utilizar se requiere un código adicional.

Los asignadores relacionales de objetos, u ORM, resuelven este problema actuando como middleware entre una aplicación y la base de datos. Puede crear objetos que modelan los datos, incluida la adición de restricciones y otras formas de metadatos. Así pues, el ORM:

- Administra la creación y actualización de la base de datos según sea necesario.
- Controla las consultas.
- Convierte (o asigna) las solicitudes que se realizan mediante los objetos en las llamadas de base de datos adecuadas.

### Introducción al ORM de Django

Django se creó para aplicaciones controladas por datos, por lo que es natural que tenga un ORM integrado. El ORM de Django resultará natural para los desarrolladores de Python, ya que usa la herencia y la sintaxis de clase con la que ya está familiarizado.

Dado que Django está diseñado para ser un marco web, puede usar la estructura de los modelos que crea para generar automáticamente HTML y formularios. En la mayoría de los casos, Django puede crear dinámicamente el código HTML para permitir al usuario editar los datos sin necesidad de crear el formulario manualmente. Incluso puede administrar las llamadas de base de datos.

<hr/>

## Modelos en Django

Los modelos se encuentran en el corazón de cualquier ORM. Un modelo es una representación de los datos con los que trabajará la aplicación. Puede tratarse de una persona, un producto, una categoría o cualquier otra forma de datos que necesite la aplicación.

### Creación de un modelo

En Django, un modelo es cualquier clase que hereda una colección de funcionalidades de `django.models.Model`. La colección incluye métodos que permiten consultar la base de datos, crear nuevas entradas y guardar actualizaciones. También puede definir campos, establecer metadatos y establecer relaciones entre los modelos.

Si quiere crear dos modelos, `Product` y `Category`, deberá agregar dos clases:

```Python
from django.db import models
class Product(models.Model):
    # details would go here
    pass

class Category(models.Model):
    # details would go here
    pass
```

### Agregar métodos

Antes de explicar cómo configurar los datos para el modelo, es importante resaltar el hecho de que un modelo es una clase de Python. Como resultado, puede agregar métodos e invalidar los que proporciona `Django.models.Model` o los que son inherentes a todos los objetos de Python.

Un método concreto que cabe resaltar es `__str__`. Este método se usa para mostrar un objeto si no se especifica ningún campo. Si Product tiene un campo name (que veremos en un momento), puede devolverlo como la representación de cadena predeterminada para Product mediante la invalidación de `__str__`.

```Python
class Product(models.Model):
    name = models.TextField()
    
    def __str__(self):
        return self.name
```

### Adición de campos

Los campos definen la estructura de datos de un modelo. Los campos pueden incluir el nombre de un elemento, una fecha de creación, un precio o cualquier otro dato que el modelo necesite almacenar.

Los diferentes datos tienen diferentes tipos de datos, reglas de validación y otras formas de metadatos. El ORM de Django contiene un amplio conjunto de opciones para configurar los campos de los modelos según sus especificaciones. El ORM es extensible, por lo que puede crear sus propias reglas según sea necesario.

#### Definición del tipo de campo

La parte principal de los metadatos de todos los campos es el tipo de datos que almacenará, como una cadena o un número. Los tipos de campo se asignan a un tipo de base de datos y un tipo de control de formularios HTML (como un cuadro de texto o una casilla). Django usa varios tipos de campo, incluidos los siguientes:

- `CharField`: una línea de texto única.
- `TextField`: varias líneas de texto.
- `BooleanField`: una opción booleana true/false.
- `DateField`: una fecha.
- `TimeField`: una hora.
- `DateTimeField`: fecha y hora.
- `URLField`: una dirección URL.
- `IntegerField`: un número entero.
- `DecimalField`: un número decimal de precisión fija.

Para agregar campos a nuestras clase Product y Category, podríamos usar el código siguiente:

```Python
from django.db import models
class Product(models.Model):
    name = models.TextField()
    price = models.DecimalField()
    creation_date = models.DateField()

class Category(models.Model):
    name = models.TextField()
```

#### Opciones de campo

Puede usar las opciones de campo para agregar metadatos para permitir valores NULL o en blanco, o para marcar un campo como único. También puede establecer opciones de validación y proporcionar mensajes personalizados para los errores de validación.

Al igual que con los tipos de campo, las opciones de campo se asignan a la configuración adecuada en la base de datos. Las reglas se aplicarán en los formularios que Django genere automáticamente.

Las opciones de campo se pasan a la función del propio campo. Distintos campos pueden admitir distintas opciones. Algunas de las opciones más comunes son las siguientes:

- `null`
    - Opción booleana para permitir valores NULL.
    - El valor predeterminado es False.
- `blank`
    - Opción booleana para permitir valores en blanco.
    - El valor predeterminado es False.
- `default`
    - Permite la configuración de un valor predeterminado si no se proporciona un valor para el campo.
    - Si quiere establecer el valor predeterminado en una base de datos null, establezca default en None.
- `unique`
    - Este campo debe contener un valor único.
    - El valor predeterminado es False.
- `min_length` y `max_length`
    - Se usa con tipos de cadena para identificar la longitud mínima y máxima de la cadena.
    - El valor predeterminado es None.
- `min_value` y `max_value`
    - Se usa con tipos numéricos para identificar los valores mínimo y máximo.
- `auto_now` y `auto_now_add`.
    - Se usa con tipos de fecha y hora para indicar si se debe usar la hora actual.
    - `auto_now` siempre establecerá el campo en la hora actual al guardar, lo que resulta útil para los campos `last_update`.
    - `auto_now_add` establecerá el campo en la hora actual en el momento de la creación, lo que resulta útil para los campos `creation_date`.

> ℹ️ **Nota** <br/>
> Los valores `null` y `blank` pueden parecer similares, pero significan cosas diferentes en los términos de la base de datos. `null` es la ausencia de un valor, mientras que `blank` es específicamente un valor vacío.

Para agregar opciones a nuestros modelos, se puede usar un código parecido al siguiente:

```Python
from django.db import models
class Product(models.Model):
    name = models.TextField(max_length=50, min_length=3, unique=True)
    price = models.DecimalField(min_value=0.99, max_value=1000)
    creation_date = models.DateField(auto_now_add=True)

class Category(models.Model):
    name = models.TextField(max_length=50, min_length=3, unique=True)
```

#### Claves y relaciones

Una práctica estándar en las bases de datos relacionales es tener una clave principal para cada fila de una tabla, normalmente un entero incrementado automáticamente. El ORM de Django agregará esta clave automáticamente a todos los modelos que cree mediante la adición de un campo denominado `id`.

Si quiere invalidar este comportamiento, puede establecer el campo que quiere que sea la clave principal. Sin embargo, debe basarse en el campo `id` de Django en la mayoría de las situaciones.

Las bases de datos relacionales también tienen relaciones entre las tablas. Un producto tiene una categoría, un empleado tiene un administrador y un automóvil tiene un fabricante. El ORM de Django admite todas las relaciones que podría querer crear entre los modelos.

La relación más común es "de uno a varios", técnicamente conocida como *relación de clave externa*. En una relación de clave externa, varios elementos comparten un solo atributo. Por ejemplo, se agrupan varios productos en una única categoría. Para modelar esta relación, se usa el campo `ForeignKey`.

Para crear la relación, agregue el campo `ForeignKey` al objeto secundario. Si los productos se agrupan en categorías, agregue la propiedad `category` a la clase `Product` y establezca el tipo en `ForeignKey`.

Django agrega automáticamente una propiedad al elemento primario para proporcionar acceso a todos los elementos secundarios denominados `<child>_set`, donde `<child>` es el nombre del objeto secundario. En nuestro ejemplo, se agregará `product_set` automáticamente a Category para proporcionar acceso a todos los productos de la categoría.

`ForeignKey` tiene un parámetro obligatorio, [on_delete](https://docs.djangoproject.com/en/3.1/ref/models/fields/#django.db.models.ForeignKey.on_delete). Este parámetro indica a Django qué debe hacer si se elimina el elemento primario. Es decir, si eliminamos una categoría, ¿qué debe ocurrir con los productos de esa categoría?

Las dos opciones más comunes son:

- `CASCADE`, que eliminará todos los productos si una categoría se elimina en nuestro ejemplo.
- `PROTECT`, que devolverá un error si intentamos eliminar una categoría que contiene productos.

> ℹ️ **Nota** <br/>
> En la mayoría de los casos, querrá usar `PROTECT`.

Para actualizar nuestro modelo para crear la relación, podemos usar el código siguiente:

```Python
from django.db import models
class Product(models.Model):
    name = models.TextField()
    price = models.DecimalField()
    creation_date = models.DateField()
    category = models.ForeignKey(
        'Category', #The name of the model
        on_delete=models.PROTECT
    )

class Category(models.Model):
    name = models.TextField()
    # product_set will be automatically created
```

<hr/>

## Ejercicio: Creación de modelos

Al crear un modelo, puede definir los campos esenciales y el comportamiento de los datos. Vamos a agregar los modelos necesarios para la aplicación *dog_shelters*.

### Crear modelos

El primer paso del proceso es agregar los modelos. Django proporciona un archivo vacío denominado models.py que puede usar para los modelos.

1. Abra el archivo *dog_shelters/models.py* en Visual Studio Code.

2. Agregue dos clases de Python para contener los modelos escribiendo el código siguiente en el comentario `# Create your models here`:

    ```Python
    # Create your models here
    class Shelter(models.Model):
        name = models.CharField(max_length=200)
        location = models.CharField(max_length=200)
        def __str__(self):
            return self.name

    class Dog(models.Model):
        shelter = models.ForeignKey(Shelter, on_delete=models.PROTECT)
        name = models.CharField(max_length=200)
        description = models.TextField()
        intake_date = models.DateTimeField(auto_now_add=True)
        def __str__(self):
            return self.name
    ```

Al agregar estos modelos, ahora tenemos una representación para los refugios y los perros. Observe la relación entre `Dog` y `Shelter`: una clase `Shelter` puede alojar muchos valores `Dog`. Observe también el valor `auto_now_add` de `intake_date`. Establece automáticamente el campo en la fecha actual si no se proporciona una fecha personalizada.

También usamos `ForeignKey` en la clase `Dog`. Esta parte indica a Django que existe una relación entre `Dog` y `Shelter`. Al definir esta relación, estamos indicando a Django que todos los perros están relacionados con un solo refugio.

### Registro del modelo

Todas las aplicaciones deben estar registradas con el proyecto en Django. Puede parecer poco intuitivo, pero el simple hecho de que exista una carpeta de aplicación dentro de un proyecto, no significa que esa carpeta se cargue automáticamente. Necesitamos registrarla agregándola a la lista `INSTALLED_APPS`.

1. Busque el nombre de clase de configuración dentro de la carpeta dog_shelters. Para encontrar este nombre de clase, vaya al archivo *dog_shelters/apps.py* y compruebe que el nombre de clase es `DogSheltersConfig` en el código siguiente:

    ```Python
    class DogSheltersConfig(AppConfig):
        default_auto_field = 'django.db.models.BigAutoField'
        name = 'dog_shelters'
    ```

2. Abra *settings.py* en el *project*.

3. Agregue la ruta de acceso completa al nombre de clase en el comentario `#[TODO] - Add the app to the list of INSTALLED_APPS`:

    ```Python
    #[TODO] - Add the app to the list of INSTALLED_APPS
        'dog_shelters.apps.DogSheltersConfig',
    ```

    La lista `INSTALLED_APPS` ahora contiene los elementos siguientes:

    ```Python
    INSTALLED_APPS = [
        #[TODO] - Add the app to the list of INSTALLED_APPS
        'dog_shelters.apps.DogSheltersConfig',
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
    ]
    ```

    Al agregar la línea a la lista `INSTALLED_APPS`, se indica a Django que esta aplicación debe incluirse al ejecutar el proyecto.

### Resumen

Ahora ha creado dos modelos para la aplicación de Django. La creación de modelos es la base de todos los proyectos de Django.

<hr/>

## Administración de la base de datos

El ORM de Django va más allá de permitirle interactuar con los datos. También puede usarlo para crear y actualizar la base de datos mediante un proceso conocido como migraciones.

### Migraciones

Una migración es una colección de actualizaciones que se realiza en el esquema de una base de datos. Un esquema de base de datos es la definición de la propia base de datos, incluidas todas las tablas y columnas y las relaciones entre esas tablas.

Cuando creamos nuestros modelos y definimos los campos, también definimos las tablas, columnas y relaciones entre esas tablas. Al crear los modelos, hemos creado la definición de esquema.

Las migraciones se usan para crear y actualizar la base de datos a medida que cambian los modelos. Como probablemente sabe, el software cambia constantemente. La forma en que se definen los modelos hoy podría ser diferente de cómo se definen mañana. Las migraciones nos ahorran el proceso de actualizar la base de datos nosotros mismos. Así pues, podemos realizar cambios en los modelos y usar Django para realizar los cambios necesarios en la base de datos.

### Realización de una migración

Para crear una migración, use el comando `makemigrations` de *manage.py*. El comando makemigrations usa la lista actual de migraciones para obtener un punto de partida y, después, usa el estado actual de los modelos para determinar la diferencia (los cambios que se deben realizar). Por último, genera el código necesario para actualizar la base de datos. Después de ejecutar `makemigrations`, muestra el nombre de la migración.

```Bash
python manage.py makemigrations
```

### Visualización del SQL para la migración

Todas las operaciones que se producen dentro de una base de datos relacional requieren el Lenguaje de consulta estructurado (SQL). Las migraciones de Django generan el SQL adecuado cuando se ejecutan. Aunque puede usar las herramientas de migración para actualizar la base de datos directamente, algunos entornos pueden tener administradores de bases de datos que administren el proceso automáticamente.

Para compilar las instrucciones SQL adecuadas, puede usar `sqlmigrate`.

```Bash
python manage.py sqlmigrate <app_label> <migration_name>
```

> ℹ️ **Nota** <br/>
> La parte `app_label` es el nombre de la aplicación, normalmente el nombre de la carpeta que contiene la aplicación. La parte `migration_name` es el nombre de la migración. También puede ver el código de Python para las migraciones de cualquier aplicación en su carpeta *migrations*.

#### Visualización de la lista de migraciones

Si quiere ver todas las migraciones, puede usar `showmigrations`.

```Bash
python manage.py showmigrations
```

#### Realización de una migración

El comando `migrate` ejecuta una migración específica o todas las migraciones en la base de datos configurada en *settings.py* en la raíz de la carpeta del proyecto.

Si abre *settings.py*, verá una sección `DATABASES` en la parte inferior. En esta sección se incluye una opción `default`, que en un nuevo proyecto está configurada para usar SQLite. Puede configurar diferentes cadenas de conexión de base de datos en esta sección según sea necesario.

```Bash
python manage.py migrate <app_label> <migration_name>
```

> ℹ️ **Nota** <br/>
> Las partes `app_label` y `migration_name` son opcionales. Si no proporciona ninguna, se ejecutarán todas las migraciones. Usará este comando con frecuencia durante el desarrollo.

<hr/>

## Ejercicio: Creación del esquema de base de datos

Una vez que hemos creado los modelos, podemos crear la base de datos. Usaremos el SQLite predeterminado y las herramientas disponibles en Django.

### Enumeración de todas las migraciones

Comencemos por enumerar todas las migraciones.

En la ventana de terminal de Visual Studio Code, ejecute el comando siguiente:

```Bash
python manage.py showmigrations
```

Observará una lista de migraciones. Es posible que se pregunte por qué tiene migraciones, si justo acaba de iniciar la aplicación y no ha hecho ninguna. Django incluye varias tablas para su sistema de administración de usuarios, la administración de sesiones y otros usos internos.

### Creación de migraciones para `dog_shelters`

Vamos a indicar a Django que se han agregado nuevos modelos y que queremos que los cambios se almacenen como una migración.

1. Vuelva a la ventana de terminal en Visual Studio Code.
2. Ejecute el siguiente comando:

    ```Bash
    python manage.py makemigrations dog_shelters
    ```

Tras ejecutar el comando, debería ver código que muestra ambos modelos almacenados como una migración en `dog` `shelters`.

```text
Migrations for `dog_shelters`
    dog_shelters\migrations\0001_inital.py
        - Create model Shelter
        - Create model Dog
```

### Actualizar la base de datos

El comando migrate ejecutará todas las migraciones. En el caso de SQLite, el comando también creará la base de datos si no existe. Vamos a crear la base de datos y a realizar las migraciones.

1. Vuelva a la ventana de terminal en Visual Studio Code.
2. Ejecute el siguiente comando:

    ```Bash
    python manage.py migrate
    ```

Las migraciones que ejecuta el comando incluyen la que hemos creado y las que están integradas en Django.

### Visualización del esquema

Ahora que hemos completado la configuración necesaria para nuestra base de datos de [SQLite](https://marketplace.visualstudio.com/items?itemName=alexcvzz.vscode-sqlite), vamos a usar la extensión SQLite de Visual Studio Code para explorar el esquema que hemos creado.

1. Seleccione el botón **Extensiones** en el área de trabajo y busque **SQLite**.

    ![install-sqlite-extension](/images/02-install-sqlite-extension.png)

2. Seleccione **Instalar** en SQLite.

3. Abra la paleta de comandos seleccionando `Ctrl+Mayús+P` en el teclado (o `Cmd+Mayús+P` en un equipo Mac).

4. Escriba **SQLite** y seleccione **SQLite: abrir base de datos**.

    ![sqlite-command](/images/02-sqlite-command.png)

5. Seleccione **db.sqlite3**.

6. En la parte inferior izquierda del área de trabajo, seleccione la flecha situada junto a **SQLITE EXPLORER**.

    ![sqlite-explorer](/images/02-sqlite-explorer.png)

7. Ahora puede ver la lista de todas las tablas que se han creado. Expanda cada una de ellas para ver las distintas columnas.

    Si explora las tablas shelter y dog, observará las distintas columnas que ha creado. Estas columnas incluyen el identificador, que se crea automáticamente en cada tabla.

### Resumen

Ahora ha administrado una base de datos mediante Django implementando los cambios que ha realizado.

<hr/>

## Ejercicio: Trabajar con datos

Al crear los modelos, creamos una API que se puede usar para acceder a los datos de la base de datos. Esta API nos permite crear, recuperar, actualizar y eliminar objetos de la base de datos.

Vamos a explorar la API trabajando con los modelos que hemos creado.

### Configuración del shell interactivo

Django incluye un shell interactivo en el que puede ejecutar código de Python en el entorno de Django.

1. Vuelva al terminal en Visual Studio Code; para ello, seleccione **Ver>Terminal**.

2. Ejecute el comando siguiente para iniciar el shell:

    ```Bash
    python manage.py shell
    ```

3. Importe los modelos desde `models` dentro de `dog_shelters`:

    ```Python
    from dog_shelters.models import Shelter, Dog
    ```

### Creación y modificación de objetos

Dado que los modelos son clases de Python, las nuevas instancias se crean con la misma sintaxis que usaríamos para crear un objeto. Dado que heredan de `Django.models.Model`, heredan la funcionalidad del ORM de Django. Esa funcionalidad incluye `save`, que se usa para guardar el objeto en la base de datos.

1. Cree un nuevo refugio ejecutando el comando de Python siguiente en el shell:

    ```Python
    shelter = Shelter(name="Demo shelter", location="Seattle, WA")
    shelter.save()
    ```

    La parte `save` escribirá el objeto en la base de datos. Como lo hemos creado desde cero, ejecutará una instrucción `INSERT` en la base de datos.

2. Actualice la ubicación del refugio a `Redmond, WA`; para ello, establezca el campo `location` llamando a `save`:

    ```Python
    shelter.location = "Redmond, WA"
    shelter.save()
    ```

    Este comando emitirá una instrucción `UPDATE` para actualizar el valor en la base de datos.

3. Cree dos nuevos perros para el refugio ejecutando los comandos de Python siguientes en el Shell:

    ```Python
    Dog(name="Sammy", description="Cute black and white dog", shelter=shelter).save()
    Dog(name="Roscoe", description="Lab mix", shelter=shelter).save()
    ```

    Como antes, `save` inserta el dog. Observe cómo se establece el parámetro `shelter` en el objeto `shelter` que hemos creado antes. Django establecerá automáticamente la relación en la base de datos.

    Tenga en cuenta también que no hemos configurado una variable local para cada instancia `Dog`. Dado que no se reutilizarán los objetos, no es necesario establecerlos en una variable.

### Recuperación de objetos

Para recuperar objetos de una base de datos, Django proporciona una propiedad `objects` en todas las clases `Model`. La propiedad objects proporciona varias funciones, como `all`, `filter` y `get`.

1. Recupere todos los perros del Refugio de demostración ejecutando el comando siguiente:

    ```Python
    shelter.dog_set.all()
    ```

    La parte `dog_set` almacena la lista de todos los perros para un refugio determinado. Django devolverá un objeto `QuerySet` con los dos perros que hemos creado.

    ```Bash
    <QuerySet [<Dog: Sammy>, <Dog: Roscoe>]>
    ```

2. Recupere el segundo perro usando `get` tal como se muestra en el comando siguiente:

    ```Python
    Dog.objects.get(pk=1)
    ```

    La función `get` devolverá solo un objeto. Puede pasar parámetros a `get` para proporcionar una cadena de consulta. Aquí usamos `pk`, que es una palabra clave especial para indicar la clave principal. El resultado devuelto será Sammy.

    ```Bash
    <Dog: Sammy>
    ```

3. Recupere todos los perros del refugio de demostración mediante `filter` tal como se muestra en el comando siguiente:

    ```Python
    Dog.objects.filter(shelter__name='Demo shelter')
    ```

    Al igual que `get`, `filter` nos permite pasar una consulta en los parámetros. Observe que podemos usar dos caracteres de subrayado (`__`) para ir de propiedad en propiedad. Dado que queremos encontrar todos los perros del refugio denominado refugio de demostración, usamos `shelter__name` para acceder a la propiedad `name` de `shelter`. El resultado devuelto será todos los perros, porque solo tenemos un refugio.

    ```Bash
    <QuerySet [<Dog: Sammy>, <Dog: Roscoe>]>
    ```
 
### Cierre del shell

Cuando haya terminado de experimentar con los objetos, puede cerrar el shell mediante el comando `exit()`.

### Resumen

Ahora ha visto cómo puede trabajar con datos mediante programación en Django mediante el ORM de Django.