# Trabajo con el sitio de administración de Django

Probablemente la característica más popular de Django para marco de Python sea su sitio de administración integrado, que permite a los usuarios internos administrar datos sin necesidad de crear una utilidad especial. Exploraremos cómo se configura a los usuarios para que usen este sitio y cómo se configura el sitio en sí mismo.

### Objetivos de aprendizaje

* Habilitar el sitio de administración
* Crear un superusuario
* Agregar modelos de aplicación y acceder a los datos
* Establecer permisos de usuario

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

<hr>

## Introducción

Cuando cree aplicaciones, es probable que le interese crear permisos individuales para acceder al sitio. La creación de una interfaz de administración para empleados o clientes para manipular el contenido puede ser una tarea complicada, pero Django acude al rescate con una simple característica de administración que se crea automáticamente en los proyectos. Para proseguir nuestro recorrido por la plataforma de Django, activaremos el sitio de administración, agregaremos permisos de usuario y exploraremos otra vista de la base de datos.

<hr>

## Ejercicio: Obtención del proyecto de inicio

En este módulo, trabajaremos en un sitio web de refugios para perros. Este proyecto se centra en recopilar información sobre todos los refugios de perros existentes y los perros que esperan ubicar en Estados Unidos. La esperanza ficticia de esta aplicación es que los perros encuentren hogares adecuados con más rapidez, ya que es posible que haya personas de todo el país que quieran adoptarlos, y no solo de su área local.

Django es el marco perfecto para este proyecto. Proporciona una ruta para desarrollar rápidamente una aplicación orientada al cliente. Django también proporciona una función de administración y base de datos establecida a la que pueden acceder fácilmente los empleados para obtener una actualización rápida. Hemos creado la configuración inicial de este proyecto, lo que nos permite centrarnos en los conceptos de este módulo.

### Clonación del repositorio de inicio

1. Abra una ventana de comandos o terminal.
2. Ejecute los comandos siguientes para clonar el repositorio de inicio y cambiar al directorio del proyecto.

    ```Bash
    git clone https://github.com/MicrosoftDocs/mslearn-django-admin-site
    cd mslearn-django-admin-site/starter
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

En la misma ventana de terminal, ejecute el comando siguiente para instalar los paquetes necesarios.

```Bash
pip install -r requirements.txt
```

### Creación de la base de datos

Con fines de desarrollo, Django usa una instancia de SQLite. Puede usar Django para crear la base de datos mediante sus herramientas de migración de bases de datos.

En la misma ventana de terminal, ejecute el comando siguiente para crear la base de datos.

```Bash
python manage.py migrate
```

### Inicio del servidor

Django puede hospedar la aplicación localmente. Haremos este paso mediante la ventana del terminal integrada en Visual Studio Code.

Escriba el comando siguiente en la misma ventana de terminal.

```Bash
python manage.py runserver
```

<hr>

## Permisos para el sitio de administración

Django incluye un sitio de administración integrado que se puede usar para administrar los datos de la aplicación y la seguridad. Este sitio forma parte de la instalación predeterminada. Como veremos, solo hacen falta unas líneas de código para activarlo. Django también incluye una implementación completa de autenticación y autorización, que se puede usar para controlar el acceso al sitio de administración.

### Django y la seguridad

Django está diseñado para simplificar la creación de aplicaciones web controladas por datos, ya que proporciona la funcionalidad normal que requieren estos tipos de sitios. Django proporciona un mecanismo de autenticación y autorización, aunque el sistema incluido se puede expandir y modificar libremente. Puede incorporar autenticadores de terceros, autenticación multifactor o cualquier otro requisito de su organización. En este módulo veremos la implementación predeterminada.

### Exploración de los tipos de usuario

De forma predeterminada, Django cuenta con tres tipos principales de usuarios: usuarios, personal y superusuarios. Puede crear sus propios tipos mediante la creación de grupos o la configuración de permisos únicos.

#### Niveles de acceso

| Access	              | Usuario	| Personal | Superusuario |
| ----------------------- | ------- | -------- | ------------ |
| Sitio de administración |	No	    | Sí       | Sí           |
| Administración de datos |	No	    | No       | Sí           |
| Administrar usuarios	  | No	    | No       | Sí           |

De forma predeterminada, el personal tiene acceso al sitio de administración, pero no puede modificar los datos. Puede establecer permisos individuales o crear grupos según sea necesario para proporcionar los niveles de acceso adecuados.

#### Creación de usuarios

Para crear usuarios en Django, primero debe crear un superusuario. Use el comando `createsuperuser` de *manage.py* para crear un superusuario. Después de crear un superusuario, puede acceder al sitio de administración para crear los demás usuarios.

### El sitio de administración

La creación de una aplicación controlada por datos conlleva, por definición, trabajar con datos. Para permitir a usuarios profesionales internos acceso para modificar los datos según lo consideren oportuno, a menudo se requiere código entre la seguridad y la interfaz. Django proporciona un sitio de administración que controla este proceso automáticamente.

A través del sitio de administración, puede determinar qué usuarios tienen acceso a qué datos. Los usuarios pueden emplear el sitio de administración para agregar, actualizar y eliminar elementos. No necesitan acceder a la base de datos directamente ni omitir ninguna de las reglas de validación que haya implementado. El modelo de seguridad y la interfaz ya están creados como parte del marco. Lo único que debe hacer es activar los modelos para que aparezcan en el sitio, lo que tan solo requiere un par de líneas de código.

<hr>

## Ejercicio: Creación de usuarios

Cuando cree proyectos, la interfaz de administración se creará automáticamente, pero no configurará ningún acceso de usuario. Para iniciar sesión en el sitio de administración de Django, ahora necesitamos crear el primer usuario, que es un superusuario.

### Creación de un superusuario

1. En Visual Studio Code, seleccione **Terminal>Nuevo terminal** para abrir una nueva ventana de terminal.

2. Ejecute el comando siguiente para crear un superusuario:

    ```Bash
    python manage.py createsuperuser
    ```

3. Responda a las preguntas del asistente para completar el proceso. Escriba el nombre de usuario que quiera usar, una dirección de correo electrónico y una contraseña.

> ℹ️ **Nota** <br>
> La contraseña debe ser compleja según los estándares de Django. Esto significa que debe tener al menos ocho caracteres y una combinación de letras mayúsculas y minúsculas, caracteres especiales y números. Si no cumple las reglas de complejidad, Django le preguntará si quiere invalidar los requisitos, lo que no se recomienda.

### Inicio de sesión en el sitio de administración

Una vez que haya creado el usuario administrador, es el momento de iniciar sesión por primera vez en la interfaz de administración de Django. Durante la configuración del proyecto anteriormente en este módulo, iniciamos el servidor, por lo que el sitio de administración ya está activo.

1. Vaya a `http://localhost:8000/admin`

    ![admin-login](/images/03-admin-login.png)

2. Escriba el nombre de usuario y la contraseña que creó anteriormente.

    Una vez que haya iniciado sesión correctamente en el sitio de administración, debería ver una pantalla similar a la siguiente.

    ![admin](/images/03-admin.png)

3. Seleccione **Usuarios**.

    Ahora verá la lista de usuarios, que incluye el usuario que ha creado.

    ![user-list](/images/03-user-list.png)

### Creación de un usuario de personal

1. En la esquina superior derecha, seleccione **AGREGAR USUARIO**.

2. Escriba un nombre de usuario para **staffuser**.

3. Escriba una contraseña que cumpla los requisitos de complejidad y confírmela.

4. Seleccione **SAVE** (GUARDAR).

5. En la pantalla siguiente, seleccione **Staff status** (Estado de personal) para que el nuevo usuario sea de personal.

    ![staff-user](/images/03-staff-user.png)

6. Seleccione **SAVE** (GUARDAR).

<hr>

## Ejercicio: Administración de datos

Como ya se indicó antes, el sitio de administración no proporciona acceso a los datos de forma predeterminada. Afortunadamente, solo necesita un par de líneas de código para registrar los modelos que quiera que se puedan editar a través de la herramienta.

### Registro de modelos

1. Abra *dog_shelters/admin.py*.

2. Debajo del comentario `# Register your models here.`, agregue el código siguiente para registrar los modelos.

    ```Python
    # Register your models here.
    from .models import Shelter, Dog

    admin.site.register(Shelter)
    admin.site.register(Dog)
    ```

3. Guarde el archivo.

4. Vuelva al explorador y actualice la página.

    Tenga en cuenta que debajo de **DOG_SHELTERS** aparecen las entradas **Dogs** y **Shelters**.

    ![dogs-shelters-admin](/images/03-dogs-shelters-admin.png)

### Acceso a los datos

Ahora que hemos registrado los modelos, podemos administrar los datos. Si ya había datos en la base de datos, podemos modificarlos, en caso de que sea necesario.

En nuestro modelo de datos (que puede explorar si abre *models.py*), tenemos `Shelter` y `Dog`. Shelter contiene varios `Dogs` para crear la relación entre los modelos.

Vamos a crear un elemento `Dog` para explorar cómo funciona el sitio de administración en lo que respecta a los datos.

1. Seleccione **Agregar** junto a **Dogs**.

    ![add-dog](/images/03-add-dog.png)

    Como observará, cuando seleccione la lista desplegable de **Shelter**, no aparecerán refugios porque no se ha creado ninguno.

    La lista desplegable existe para que podamos seleccionar el refugio en el que registraremos el perro. Para crear uno, seleccione el signo más (+).

2. Seleccione el signo más (+).

    Se abre una nueva ventana donde puede crear un Shelter.

    ![new-shelter](/images/03-new-shelter.png)

3. Escriba un nombre y una ubicación para el refugio, como Contoso y Redmond, WA.

4. Seleccione **SAVE** (GUARDAR).

    La pantalla se actualiza y muestra el refugio recién creado como la opción seleccionada para el perro.

5. Escriba un nombre y una descripción para el perro.

6. Seleccione **SAVE** (GUARDAR).

    La pantalla vuelve a la lista de perros y aparece la información sobre el perro recién creado.

    ![new-dog](/images/03-new-dog.png)

7. Si selecciona el perro, se le dirigirá a la página de detalles, donde podrá actualizar los valores o eliminar la entrada.

> ℹ️ **Nota** <br/>
> En la pantalla se muestra el nombre del perro o el refugio si va a la sección **Shelters** del sitio de administración. Esta información aparece porque hemos establecido el método `__str__` en nuestros objetos. La visualización predeterminada de cualquier objeto es el valor devuelto por `__str__`.

<hr>

## Ejercicio: Administración de permisos

Como se indicó anteriormente, puede agregar usuarios con permisos para modificar datos a través del sitio de administración. Vamos a actualizar el usuario **staffuser** que creamos en una unidad anterior para que tenga permisos para modificar perros.

### Establecimiento de los permisos de usuario

1. Vuelva al sitio de administración en el explorador.

2. Seleccione **Usuarios**.

3. Seleccione **staffuser** para actualizar nuestro **usuario de personal**.

4. Asegúrese de que está seleccionado **Staff status** (Estado de personal).

5. Desplácese hacia abajo hasta **Permisos de usuario**.

6. Seleccione los permisos siguientes:

    - dog_shelters | dog | Can add dog (dog_shelters | perro | Puede agregar perro)
    - dog_shelters | dog | Can change dog (dog_shelters | perro | Puede cambiar perro)
    - dog_shelters | dog | Can view dog (dog_shelters | perro | Puede ver perro)

7. Seleccione **Choose** (Elegir).

    ![set-permissions](/images/03-set-permissions.png)

8. Seleccione **SAVE** (GUARDAR).

### Inicio de sesión como usuario de personal

Veamos ahora la diferencia entre un superusuario y un usuario de personal. Para ello, iniciaremos sesión como usuario de personal.

1. Seleccione** CERRAR SESIÓN** en la esquina superior derecha.

2. Seleccione **Iniciar sesión de nuevo**.

3. Inicie sesión como **staffuser** con la contraseña que creó anteriormente.

    Tenga en cuenta que la página de administración solo permite el acceso a **Dogs**.

    ![staff-user-display](/images/03-staff-user-display.png)

4. Seleccione **Dogs**.

5. Seleccione el perro que creó antes.

    Tenga en cuenta que puede modificar el perro, pero no eliminarlo.

### Resumen

Hemos configurado un usuario de personal con permisos limitados en el sitio de administración. Puede usar esta función para controlar el acceso a los datos confidenciales de la aplicación.