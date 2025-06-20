# Aplicación Full-Stack de Registro de Usuarios (Angular & ASP.NET Core)

Este proyecto es una aplicación web full-stack diseñada para gestionar el registro de nuevos usuarios. Implementa un frontend moderno y reactivo con Angular y un backend robusto y seguro con ASP.NET Core Web API. Es una demostración de un flujo de autenticación completo, desde la captura de datos en el cliente hasta la creación del usuario en la base de datos.

## 📸 Vista Previa



El formulario es limpio, responsivo y proporciona validación en tiempo real para guiar al usuario.

## ✨ Características Principales

-   **Registro de Usuarios**: Formulario para registrar usuarios con Nombre Completo, Email y Contraseña.
-   **Frontend Reactivo**: Construido con Angular y `ReactiveFormsModule` para una experiencia de usuario fluida y un manejo de estado predecible.
-   **Validación Robusta del Lado del Cliente**:
    -   Campos obligatorios.
    -   Formato de correo electrónico válido.
    -   Requisitos de contraseña (longitud mínima y caracteres especiales).
    -   Confirmación de contraseña para evitar errores de tipeo.
-   **Notificaciones en Tiempo Real**: Uso de `ngx-toastr` para dar feedback instantáneo al usuario sobre el éxito o los errores del registro.
-   **Backend Seguro con ASP.NET Core Identity**: Utiliza el sistema de identidad integrado de ASP.NET Core para gestionar usuarios, contraseñas y seguridad de forma eficiente.
-   **API Minimalista**: El endpoint del backend está construido usando la sintaxis de Minimal APIs de .NET, lo que resulta en un código más limpio y directo.
-   **Modelo de Usuario Personalizado**: El modelo de usuario de Identity ha sido extendido para incluir campos adicionales como `FullName`.
-   **CORS Configurado**: El backend está configurado para permitir peticiones desde el cliente de Angular (`http://localhost:4200`).

## 🛠️ Tecnologías Utilizadas

### Frontend
-   **Angular**: Framework para construir aplicaciones web del lado del cliente.
-   **TypeScript**: Superconjunto de JavaScript que añade tipado estático.
-   **Angular Reactive Forms**: Para crear y gestionar formularios complejos con validaciones dinámicas.
-   **Bootstrap**: Framework CSS para un diseño responsivo y moderno.
-   **ngx-toastr**: Librería para mostrar notificaciones (toasts) no intrusivas en Angular.
-   **Angular CLI**: Interfaz de línea de comandos para inicializar, desarrollar y mantener aplicaciones Angular.

### Backend
-   **ASP.NET Core Web API**: Framework para construir APIs RESTful sobre .NET.
-   **C#**: Lenguaje de programación principal para el backend.
-   **Minimal APIs**: Característica de .NET para crear endpoints HTTP con código mínimo.
-   **Entity Framework Core**: ORM (Object-Relational Mapper) para interactuar con la base de datos.
-   **ASP.NET Core Identity**: Sistema de membresía que añade funcionalidades de login y gestión de usuarios a la aplicación.
-   **SQL Server**: Sistema de gestión de bases de datos relacionales.

## 🚀 Instalación y Puesta en Marcha

Sigue estos pasos para configurar y ejecutar el proyecto en tu entorno local.

### Prerrequisitos

-   [.NET SDK](https://dotnet.microsoft.com/download) (versión 8.0 o superior recomendada)
-   [Node.js y npm](https://nodejs.org/en/) (versión 18 o superior recomendada)
-   [Angular CLI](https://angular.io/cli) (`npm install -g @angular/cli`)
-   Una instancia de SQL Server (LocalDB, Express, etc.).

### 1. Configuración del Backend (ASP.NET Core)

1.  **Clonar el repositorio**:
    ```bash
    git clone [https://URL-DE-TU-REPOSITORIO.git](https://URL-DE-TU-REPOSITORIO.git)
    ```

2.  **Navegar a la carpeta del backend**: (La carpeta que contiene el archivo `.csproj`)
    ```bash
    cd ruta/a/tu/proyecto/AuthECAPI
    ```

3.  **Configurar la base de datos**:
    -   Abre el archivo `appsettings.json`.
    -   Modifica la cadena de conexión `DevDB` para que apunte a tu instancia de SQL Server.
        ```json
        "ConnectionStrings": {
          "DevDB": "Server=(localdb)\\mssqllocaldb;Database=AuthECDB;Trusted_Connection=True;"
        }
        ```

4.  **Crear y aplicar las migraciones de la base de datos**:
    -   El proyecto usa Entity Framework Core para gestionar el esquema de la base de datos. Ejecuta los siguientes comandos para crear la base de datos y sus tablas (incluyendo las tablas de Identity).
    ```bash
    dotnet ef migrations add InitialCreate
    dotnet ef database update
    ```

5.  **Ejecutar el backend**:
    ```bash
    dotnet run
    ```
    La API estará disponible en la URL que indique la consola (ej. `http://localhost:5194`).

### 2. Configuración del Frontend (Angular)

1.  **Navegar a la carpeta del frontend**: (La carpeta que contiene el archivo `angular.json`)
    ```bash
    cd ruta/a/tu/proyecto/AuthECClient
    ```

2.  **Instalar dependencias**:
    ```bash
    npm install
    ```

3.  **Ejecutar el frontend**:
    ```bash
    ng serve
    ```
    La aplicación Angular estará disponible en `http://localhost:4200`. Abre esta URL en tu navegador.

## 🏛️ Estructura del Proyecto

<details>
<summary><b>Frontend (Angular)</b></summary>

```
src/
├── app/
│   ├── user/
│   │   ├── registration/
│   │   │   ├── registration.component.html   # Estructura del formulario de registro
│   │   │   └── registration.component.ts     # Lógica del formulario y validaciones
│   │   ├── user.component.html               # Contenedor de la página de registro
│   │   └── user.component.ts
│   ├── shared/
│   │   ├── pipes/                          # Pipes personalizados (ej. firstKey)
│   │   └── services/                       # Servicios (ej. auth.service.ts para llamar a la API)
│   ├── app.component.ts                      # Componente raíz
│   ├── app.config.ts                       # Configuración principal (providers, http, etc.)
│   └── app.routes.ts                       # Definición de rutas
└── ...
```
-   El `RegistrationComponent` contiene toda la lógica del formulario, incluyendo la creación del `FormGroup`, las validaciones (tanto síncronas como la validación cruzada `passwordMatchValidator`), y la comunicación con el backend a través de un servicio.
</details>

<details>
<summary><b>Backend (ASP.NET Core)</b></summary>

```
AuthECAPI/
├── Models/
│   ├── AppUser.cs                          # Modelo de usuario extendido con FullName
│   ├── AppDbContext.cs                     # Contexto de la base de datos de EF Core
│   └── UserRegistrationModel.cs            # DTO para la petición de registro
├── Program.cs                              # Configuración y definición de endpoints de la API
├── appsettings.json                        # Cadenas de conexión y configuración
└── ...
```
-   `Program.cs` es el corazón del backend. Aquí se configura la inyección de dependencias, Identity, Entity Framework, CORS y se define el endpoint `POST /api/signup` que maneja la lógica de creación de usuarios.
-   El modelo `AppUser` extiende `IdentityUser` para agregar el campo `FullName` a la tabla de usuarios en la base de datos.
</details>


## 🔌 Endpoint de la API

### Registrar Nuevo Usuario

-   **URL**: `POST /api/signup`
-   **Descripción**: Crea un nuevo usuario en el sistema.
-   **Cuerpo de la Petición (`Request Body`)**:
    ```json
    {
      "fullName": "string",
      "email": "string",
      "password": "string"
    }
    ```
-   **Respuesta Exitosa (`200 OK`)**: Devuelve un objeto indicando que la operación fue exitosa.
    ```json
    {
      "succeeded": true,
      "errors": []
    }
    ```
-   **Respuesta de Error (`400 Bad Request`)**: Devuelve un objeto con los errores encontrados, por ejemplo, si el email ya existe.
    ```json
    {
      "succeeded": false,
      "errors": [
        {
          "code": "DuplicateEmail",
          "description": "Email 'example@test.com' is already taken."
        }
      ]
    }
    ```
