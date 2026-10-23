# 🚀 Laboratorio: Creación e Instalación de Laravel e Implementación del Login

**Universidad Tecnológica de Panamá**
Facultad de Ingeniería de Sistemas Computacionales
Departamento de Computación y Software · Desarrollo Web

| | |
|---|---|
| **Estudiante** | Iliana Navarro |
| **Grupo** | 1S3122 |
| **Instructor del laboratorio** | Ing. Irina Fong |
| **Fecha de ejecución** | 9 de octubre de 2026 |
| **Fecha de entrega** | 16 de octubre de 2026 |

---

## 📑 Tabla de contenido

1. [Introducción y objetivos](#-1-introducción-y-objetivos)
2. [Requisitos previos y entorno de desarrollo](#️-2-requisitos-previos-y-entorno-de-desarrollo)
3. [Desarrollo detallado del proceso](#-3-desarrollo-detallado-del-proceso-y-comandos)
4. [Dificultades técnicas y soluciones](#-4-dificultades-técnicas-encontradas-y-soluciones-aplicadas)
5. [Referencias bibliográficas](#-5-referencias-bibliográficas)

---

## 📌 1. Introducción y objetivos

Este documento recopila y detalla el proceso técnico para la creación, configuración y despliegue de una aplicación web basada en el framework **Laravel**.

El propósito de la asignación es:

- Comprender la arquitectura **Modelo-Vista-Controlador (MVC)**.
- Manejar dependencias mediante gestores de paquetes modernos.
- Resolver conflictos habituales en entornos locales con bases de datos relacionales.
- Integrar rápidamente un sistema de autenticación de usuarios (**Login y Registro**) usando **Bootstrap** como framework visual.

---

## 🛠️ 2. Requisitos previos y entorno de desarrollo

Para la correcta ejecución del proyecto se configuró un entorno local con las siguientes herramientas:

| Componente | Versión instalada | Descripción |
|---|---|---|
| **Sistema operativo** | Windows (PowerShell / CMD) | Entorno de comandos nativo para administrar procesos y ejecutar scripts. |
| **PHP** | 8.5.9 (NTS x64) | Intérprete del lado del servidor, ubicado en `C:\php\php.exe`. |
| **Composer** | 2.10.3 | Administrador de paquetes de PHP; descarga e integra las librerías del framework. |
| **Node.js y NPM** | Node v24.20.0 / NPM 11.19.0 | Herramientas de frontend y compilación de recursos estáticos con Vite. |
| **WampServer** | Apache 2.4 / MySQL 8.0 | Entorno local con servidor web Apache y gestor de base de datos MySQL. |
| **Visual Studio Code** | Última versión | IDE para modificar y estructurar el código fuente. |

---

## 💻 3. Desarrollo detallado del proceso y comandos

### Paso 3.1: Validación del entorno de consola

Antes de iniciar, se comprueba que PHP, Composer y Node respondan correctamente en la terminal.

```bash
pwd
php -v
composer -V
node -v
npm -v
```

> **Explicación:** `pwd` confirma que se trabaja dentro de la ruta del servidor local (`C:\wamp64\www`). Las validaciones de versión (`-v` / `-V`) aseguran que no haya incompatibilidades entre Laravel y el PHP instalado.

📸 **Captura de pantalla:**

<img width="768" height="273" alt="Captura de pantalla 2026-10-21 082116" src="https://github.com/user-attachments/assets/2a602781-f662-4ee2-b00d-ef4fa5fbb0be" />
<img width="1426" height="591" alt="Captura de pantalla 2026-10-21 082409" src="https://github.com/user-attachments/assets/ec0001b2-9590-4346-b898-47649fd996ff" />
<img width="768" height="171" alt="Captura de pantalla 2026-10-21 082133" src="https://github.com/user-attachments/assets/0b0ea960-49f4-4426-afa0-b71b264e387e" />



---

### Paso 3.2: Instalación del framework y creación del proyecto

```bash
cd C:\wamp64\www
composer global require laravel/installer
laravel new LabLogin
```

> **Explicación:** Nos posicionamos en la carpeta pública de WampServer. `composer global require` instala el instalador de Laravel de forma global, lo que permite ejecutar `laravel new LabLogin`, que genera el árbol de directorios MVC (`app`, `database`, `routes`, `resources`, etc.). Durante el asistente se seleccionó **Blade** como motor de plantillas.

📸 **Captura de pantalla:**

<img width="1047" height="1000" alt="Captura de pantalla 2026-10-21 083205" src="https://github.com/user-attachments/assets/be7f90f0-8978-4b98-9b6e-5219294b2c2d" />

<img width="723" height="1008" alt="Captura de pantalla 2026-10-21 084100" src="https://github.com/user-attachments/assets/7cd795ab-6d4b-4479-b523-a056778cdcc5" />
<img width="772" height="1007" alt="Captura de pantalla 2026-10-21 084532" src="https://github.com/user-attachments/assets/bbe12e24-fba3-47ba-a30b-d074bb32de8a" />


---

### Paso 3.3: Módulo de autenticación (`laravel/ui`)

```bash
cd LabLogin
composer require laravel/ui
php artisan ui bootstrap --auth
```

> **Explicación:** El paquete `laravel/ui` gestiona la autenticación clásica. El comando `ui bootstrap --auth` agrega las rutas de autenticación en `routes/web.php`, genera los controladores de acceso y crea las vistas de **Login** y **Registro** con Bootstrap.


---

### Paso 3.4: Dependencias frontend y compilación (Vite)

```bash
npm install
npm run dev
```

> **Explicación:** `npm install` lee `package.json` y descarga los módulos de Node necesarios. `npm run dev` inicia el servidor de desarrollo de Vite, que compila CSS y JavaScript en tiempo real.
>
> 💡 **Nota técnica:** si el puerto por defecto `5173` está ocupado, Vite reasigna automáticamente el servicio al `5174` sin afectar la funcionalidad.

---

### Paso 3.5: Configuración de base de datos, limpieza y migraciones

```bash
php artisan config:clear
php artisan config:cache
php artisan migrate:fresh
```

> **Explicación:** Primero se limpia y regenera la caché de configuración para que Laravel reconozca los parámetros del archivo `.env` (conexión a la base de datos `lablogin` en MySQL). Luego `migrate:fresh` elimina las tablas previas y ejecuta las migraciones desde cero, creando las tablas esenciales: usuarios, restablecimiento de contraseñas, caché y trabajos.


---

### Paso 3.6: Despliegue local del servidor

```bash
php artisan serve
```

> **Explicación:** Inicia el servidor web embebido de PHP y despliega la aplicación en [http://127.0.0.1:8000](http://127.0.0.1:8000), donde se pueden evaluar las rutas y el diseño.

📸 **Captura de pantalla:**

<img width="1046" height="1003" alt="Captura de pantalla 2026-10-22 144419" src="https://github.com/user-attachments/assets/72db777e-c76f-4afd-880c-70c0d72765ee" />


---

## 🚨 4. Dificultades técnicas encontradas y soluciones aplicadas

### 1️⃣ Conflicto de longitud de índices en MySQL

```text
SQLSTATE[42000]: Specified key was too long
```

- **Causa:** Las versiones recientes de MySQL imponen un límite estricto en los bytes de las llaves únicas, lo que genera errores al migrar las tablas predeterminadas de Laravel.
- **Solución:** En `app/Providers/AppServiceProvider.php` se importó la fachada `Schema` y se agregó la siguiente instrucción dentro del método `boot()`:

```php
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

### 2️⃣ Incompatibilidad de sintaxis en PowerShell al concatenar comandos (`&&`)

- **Causa:** PowerShell, la terminal por defecto en Windows, no soporta el operador `&&` para encadenar comandos de la misma manera que Bash.
- **Solución:** Se ejecutaron los comandos de forma secuencial e independiente:

```bash
npm install
npm run dev
```

### 3️⃣ Integración del footer institucional

- **Causa:** Se necesitaba personalizar la vista de bienvenida (`resources/views/welcome.blade.php`) manteniendo la coherencia estética del diseño original.
- **Solución:** Se añadió un bloque semántico `<footer>` al final de la estructura HTML con los datos oficiales de la universidad y los nombres de la estudiante y del instructor.

---

## 📚 5. Referencias bibliográficas

- Laravel Documentation. *Authentication & Scaffolding Guide*. <https://laravel.com/docs>
- PHP Manual. *The Model-View-Controller (MVC) Architectural Pattern*. <https://www.php.net>
- Bootstrap Framework. *Documentation v5.3 – Components and Utilities*. <https://getbootstrap.com>
