=================================================================================
                       UNIVERSIDAD TECNOLÓGICA DE PANAMÁ
            FACULTAD DE INGENIERÍA DE SISTEMAS COMPUTACIONALES
                       DEPARTAMENTO DE COMPUTACIÓN Y SOFTWARE
                                DESARROLLO WEB

               LABORATORIO DEL 9 DE OCTUBRE: CREACIÓN E INSTALACIÓN DE LARAVEL
                             IMPLEMENTACIÓN DEL LOGIN EN LARAVEL


   Estudiante: Iliana Navarro
   Grupo: 1S3122
   Instructor del Laboratorio: Ing. Irina Fong
   Fecha de Ejecución: 9 de octubre de 2026
   Fecha de Entrega: 16 de octubre de 2026

=================================================================================
🚀 Documentación y Desarrollo de Laboratorio: Creación e Instalación de Laravel y Módulo de Autenticación

📌 1. Introducción y Objetivos de la Asignación

El presente documento recopila y detalla el proceso técnico implementado para la creación, configuración y despliegue de una aplicación web basada en el framework Laravel. El propósito fundamental de esta asignación es comprender a fondo la arquitectura Modelo-Vista-Controlador (MVC), el manejo de dependencias mediante gestores modernos, la resolución de conflictos habituales en entornos locales con bases de datos relacionales, y la integración rápida de un sistema robusto de autenticación de usuarios (Login y Registro) utilizando Bootstrap como framework visual.

🛠️ 2. Requisitos Previos y Entorno de Desarrollo

Para garantizar la correcta ejecución del proyecto, se configuró un ecosistema de desarrollo local integrado por las siguientes herramientas tecnológicas:

Componente Tecnológico

Versión Instalada

Descripción y Justificación Académica

Sistema Operativo

Windows (PowerShell / CMD)

Entorno de comandos nativo para la administración de procesos y ejecución de scripts del sistema.

PHP

Versión 8.5.9 (NTS x64)

Intérprete del lenguaje del lado del servidor (backend) ubicado en C:\php\php.exe.

Composer

Versión 2.10.3

Administrador de paquetes oficial de PHP, encargado de descargar e integrar las librerías del framework.

Node.js & NPM

Node v24.20.0 / NPM 11.19.0

Herramientas orientadas al desarrollo frontend y compilación de recursos estáticos mediante Vite.

WampServer

Apache 2.4 / MySQL 8.0

Entorno local integrado que provee el servidor web Apache y el gestor de base de datos relacional MySQL.

Visual Studio Code

Última versión

Entorno de desarrollo integrado (IDE) para la modificación y estructuración del código fuente.

💻 3. Desarrollo Detallado del Proceso y Comandos

A continuación se explica paso a paso la lógica detrás de cada comando ejecutado en la consola durante el laboratorio:

Paso 3.1: Validación del Entorno de Consola

Antes de iniciar cualquier estructura, es obligatorio comprobar que las rutas globales de PHP y Composer respondan de manera correcta en la terminal.

Comandos:

pwd
php -v
composer -V
node -v
npm -v


Explicación detallada: El comando pwd nos permite certificar que estamos trabajando dentro de la ruta del servidor local (C:\wamp64\www). Las validaciones de versión (-v / -V) aseguran que no existan conflictos de incompatibilidad entre las librerías de Laravel y el intérprete de PHP instalado en el equipo.

🖼️ Captura de Pantalla:

Paso 3.2: Instalación del Framework y Creación del Proyecto

Para automatizar la descarga de la estructura limpia de Laravel, se utiliza el instalador global gestionado a través de Composer.

Comandos:

cd C:\wamp64\www
composer global require laravel/installer
laravel new LabLogin


Explicación detallada: Nos posicionamos en la carpeta pública del servidor local WampServer. El comando composer global require instala el motor global de Laravel en la máquina, permitiendo ejecutar el comando laravel new LabLogin, el cual genera de manera automática todo el árbol de directorios MVC (app, database, routes, resources, etc.). Durante este asistente, se seleccionó Blade como el motor de plantillas para las vistas.

🖼️ Captura de Pantalla:

Paso 3.3: Implementación del Módulo de Autenticación (laravel/ui)

Para evitar codificar desde cero los formularios de acceso y registro, Laravel provee paquetes oficiales de scaffolding.

Comandos:

cd LabLogin
composer require laravel/ui
php artisan ui bootstrap --auth


Explicación detallada: Ingresamos al directorio del proyecto creado. El paquete laravel/ui es requerido para gestionar los componentes de autenticación clásica. Posteriormente, el comando de Artisan ui bootstrap --auth inyecta automáticamente las rutas de autenticación en routes/web.php, genera el controlador de acceso, y crea las vistas de Login y Registro estilizadas con componentes responsivos de Bootstrap.

🖼️ Captura de Pantalla:

Paso 3.4: Gestión de Dependencias Frontend y Compilación (Vite)

Los frameworks modernos separan la lógica del backend de los recursos visuales del frontend mediante herramientas de empaquetado rápido.

Comandos:

npm install
npm run dev


Explicación detallada: npm install lee el archivo package.json para descargar todos los módulos de Node necesarios para el diseño visual. Luego, npm run dev inicializa el servidor de desarrollo basado en Vite, el cual compila en tiempo real los archivos CSS y JavaScript. (Nota técnica: Si el puerto por defecto 5173 se encuentra ocupado por otro proceso, Vite reasigna automáticamente el servicio al puerto 5174 sin alterar la funcionalidad).

🖼️ Captura de Pantalla:

Paso 3.5: Configuración de Base de Datos, Limpieza y Migraciones

Laravel maneja la estructura de la base de datos a través de clases de migración orientadas a objetos, garantizando portabilidad.

Comandos:

php artisan config:clear
php artisan config:cache
php artisan migrate:fresh


Explicación detallada: Primero limpiamos y actualizamos la caché de configuración (config:clear / config:cache) para forzar a Laravel a reconocer los parámetros definidos en el archivo .env (conexión a la base de datos lablogin en MySQL). Después, migrate:fresh elimina cualquier tabla previa y ejecuta las migraciones limpias para construir las tablas esenciales del sistema (usuarios, restablecimiento de contraseñas, caché y trabajos).

🖼️ Captura de Pantalla:

Paso 3.6: Despliegue Local del Servidor de Aplicaciones

Para poner en marcha el sistema y verificar su correcta operatividad en el navegador web:

Comando:

php artisan serve


Explicación detallada: Este comando inicia el servidor web embebido de PHP, desplegando la aplicación en la dirección local por defecto http://127.0.0.1:8000, permitiendo evaluar el funcionamiento de las rutas y el diseño visual.

🖼️ Captura de Pantalla:

🚨 4. Dificultades Técnicas Encontradas y Soluciones Aplicadas

Durante el desarrollo de la práctica se presentaron diversos retos técnicos que fueron solventados de la siguiente manera:

Conflicto de longitud de índices en MySQL (SQLSTATE[42000]: Specified key was too long):

Causa: Las versiones recientes de MySQL imponen un límite estricto en los bytes de las llaves únicas, generando errores al intentar migrar las tablas predeterminadas de Laravel.

Solución: Se modificó el archivo app/Providers/AppServiceProvider.php importando la fachada Schema y agregando la instrucción global Schema::defaultStringLength(191); dentro del método boot().

Incompatibilidad de sintaxis en PowerShell al concatenar comandos (&&):

Causa: La terminal de PowerShell utilizada por defecto en Windows no soporta el operador lógico && para encadenar comandos de Node de la misma manera que Bash.

Solución: Se ejecutaron los comandos de forma secuencial e independiente (npm install y posteriormente npm run dev).

Integración del Footer Institucional:

Causa: Personalizar la vista principal de bienvenida (resources/views/welcome.blade.php) manteniendo la coherencia estética del diseño original.

Solución: Se añadió un bloque semántico <footer> al final de la estructura HTML con los datos oficiales de la universidad, nombre de la estudiante y del instructor.

📚 5. Referencias Bibliográficas

Laravel Documentation. Authentication & Scaffolding Guide. Disponible en: https://laravel.com/docs

PHP Manual. The Model-View-Controller (MVC) Architectural Pattern. Disponible en: https://www.php.net

Bootstrap Framework. Documentation v5.3 - Components and Utilities. Disponible en: https://getbootstrap.com
