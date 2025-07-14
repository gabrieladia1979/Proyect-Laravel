# Curso Laravel

A continuación se detallan los requisitos de software para el curso y una explicación estructurada de la arquitectura de Laravel y el ciclo de vida de una petición.

### 🛠️ **Requisitos de Software**

Para seguir el curso, es fundamental tener instalado y configurado el siguiente software:

- **XAMPP:** Provee el entorno de servidor local, incluyendo **PHP**, que es el lenguaje sobre el que corre Laravel.
- **MariaDB:** Sistema de gestión de bases de datos que usaremos para almacenar la información de nuestra aplicación.
- **Composer:** Es el gestor de dependencias para PHP. Se utiliza para instalar Laravel y todas las librerías que el framework necesita.
- **Node.js:** Se utiliza para gestionar las dependencias del *frontend* (CSS, JavaScript) y para compilar los *assets* de la aplicación con herramientas como Vite.

> Importante: Es crucial configurar las variables de entorno del sistema operativo para que se pueda acceder a los ejecutables de php y composer desde cualquier terminal.
> 

## Clase 1 - Introducción a Laravel e instalación

### **Arquitectura Basada en el Patrón MVC**

Laravel implementa una variante del patrón de arquitectura de software **Modelo-Vista-Controlador (MVC)**. Este patrón separa la lógica de la aplicación en tres componentes interconectados, haciendo el código más organizado, escalable y fácil de mantener.

- **Modelo (Model):** Representa la información (los datos) de la aplicación y la lógica de negocio. En Laravel, cada modelo generalmente corresponde a una tabla de la base de datos. Su principal función es interactuar con la base de datos para consultar, crear, actualizar o eliminar registros.
- **Vista (View):** Es la capa de presentación, responsable de mostrar la información al usuario. En Laravel, las vistas suelen ser archivos **Blade** (`.blade.php`), que son plantillas HTML con sintaxis adicional para mostrar datos dinámicos de forma sencilla.
- **Controlador (Controller):** Actúa como el intermediario entre el Modelo y la Vista. Recibe las peticiones del usuario, solicita los datos necesarios al Modelo y, finalmente, carga la Vista apropiada para mostrar esa información o devuelve una respuesta en otro formato (como JSON para una API).
  

<img width="1244" height="624" alt="image" src="https://github.com/user-attachments/assets/3d56f62f-4ce1-42b2-9c1b-8bdad09fe94b" />


### 🔄 **El Ciclo de Vida de una Petición en Laravel**

Cuando un usuario interactúa con una aplicación Laravel, se desencadena un ciclo predecible.

1. **Petición del Cliente:** Todo comienza cuando un cliente (un navegador web o_tro sistema) realiza una petición a una URL específica de la aplicación. Por ejemplo, al acceder a `https://mi-blog.com/posts`.
   
2. **Enrutamiento (Routing):** La petición es recibida por el **enrutador (router)** de Laravel. Este componente, definido en los archivos de `routes/`, asocia la URL solicitada con una acción específica, generalmente un método dentro de un **Controlador**.

3. **Controlador (Controller):** El enrutador invoca al método del Controlador asignado. Este método contiene la lógica para gestionar la petición. Por ejemplo, si se solicitan los posts de un blog, el controlador se encargará de obtenerlos.

4. **Interacción con el Modelo:** Para obtener los datos, el Controlador se comunica con el **Modelo** correspondiente (ej. `Post.php`). Gracias al **ORM** de Laravel, llamado **Eloquent**, no es necesario escribir consultas SQL manualmente. Simplemente se usan métodos del modelo como `Post::all()` o `Post::find(1)`. Eloquent traduce estas llamadas a código SQL compatible con el sistema de base de datos configurado (MariaDB, en este caso).

5. **Generación de la Respuesta:** Una vez que el Controlador recibe los datos del Modelo, prepara la respuesta para el cliente. Hay dos caminos principales:
    - **Devolver una Vista:** El Controlador pasa los datos a una **Vista (Blade)**. Blade procesa la plantilla, inserta los datos dinámicos y genera un archivo HTML completo.
    - **Devolver una API (JSON):** En aplicaciones de solo *backend* o APIs, el Controlador puede devolver directamente los datos en formato JSON, que será consumido por un *frontend* (como una aplicación en React, Vue o Angular) u otro servicio.
6. **Respuesta al Cliente:** Finalmente, el servidor envía la respuesta generada (el HTML o el JSON) de vuelta al cliente, completando así el ciclo.

![image.png](attachment:1dd5d870-f7c5-4b38-a505-b2fed538ca8c:image.png)

### ✨ **Ampliando la Arquitectura Básica**

El flujo MVC puede ser extendido con componentes adicionales muy potentes:

### **Middleware**

Un **Middleware** actúa como un "guardia de seguridad" o un filtro entre la petición del usuario y el Controlador. Permite ejecutar código antes de que la petición llegue a su destino.

- **Ejemplo clásico:** Un middleware de autenticación (`auth`) verifica si el usuario ha iniciado sesión. Si no lo está, lo redirige a la página de login en lugar de permitirle el acceso a una ruta protegida.

### **Observadores (Observers)**

Los **Observadores** permiten "escuchar" eventos que ocurren en los modelos de Eloquent. Se pueden ejecutar acciones automáticamente cuando un registro es creado, actualizado, eliminado, etc.

- **Ejemplo práctico:** Se puede crear un observador para el modelo `User`. Cuando un nuevo usuario se registra (`created` event), el observador puede disparar automáticamente el envío de un correo de bienvenida.
