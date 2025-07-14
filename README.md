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


En este caso el patrón MVC , arranca con …

1. El cliente - Este puede ser un usuario o otro sistema , nos solicita una información a travez de la ruta. Puede ser a travez de un blog - donde el usuario introduce la ruta → Mi blog.com 
2. El sistema ahi acude al dispacher (fichero de rutas) - donde se asocia esa ruta con un controller , cada url tendra su propia controller. Cada ruta controllada x dicho controlador
