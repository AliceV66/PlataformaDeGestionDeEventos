Plataforma de Gestión de Eventos en Django
​Este proyecto es una plataforma web desarrollada con Django para la gestión de eventos como conferencias, conciertos y seminarios. Permite a los usuarios registrarse, iniciar sesión y gestionar eventos según su rol asignado: Administrador, Organizador de Eventos o Asistente.
​El objetivo principal es implementar un sistema robusto de autenticación y autorización utilizando el modelo Auth de Django para controlar el acceso a los diferentes recursos de la plataforma, asegurando que solo los usuarios con los permisos adecuados puedan realizar acciones específicas.
​Características Principales
​Autenticación de Usuarios: Sistema completo de registro, inicio de sesión y cierre de sesión.
​Gestión de Eventos: Creación, visualización, edición y eliminación de eventos.
​Control de Acceso Basado en Roles (RBAC):
​Administradores: Control total sobre todos los eventos y usuarios.
​Organizadores de Eventos: Pueden crear y gestionar sus propios eventos.
​Asistentes: Pueden ver y registrarse en eventos públicos o en aquellos a los que han sido invitados.
​Vistas Protegidas: Uso de Mixins de Django (LoginRequiredMixin y PermissionRequiredMixin) para proteger las vistas.
​Manejo de Permisos: Implementación del sistema de permisos de Django para un control de acceso granular.
​Seguridad: Configuración de sesiones seguras y HTTPS.

Roadmap y Tareas Pendientes
​Aquí tienes una lista de las tareas a realizar para completar la funcionalidad del proyecto, basada en los requisitos definidos.
​1. Configuración del Modelo Auth de Django
​[ ] Explorar la estructura y funcionamiento del modelo User de Django.
​[ ] Implementar las vistas y plantillas para el registro de nuevos usuarios.
​[ ] Crear las vistas y plantillas para el inicio y cierre de sesión.
​[ ] Proteger las vistas de gestión de eventos para que solo usuarios autenticados puedan acceder.
​2. Enrutamiento para Login/Logout
​[ ] Crear las URLs /login/ y /logout/ en el archivo urls.py.
​[ ] Configurar las variables LOGIN_REDIRECT_URL y LOGOUT_REDIRECT_URL en settings.py para redirigir a los usuarios a las páginas correctas después de la autenticación.
​3. Gestión de Roles y Permisos
​[ ] Crear los grupos de usuarios: Administradores, Organizadores y Asistentes desde el panel de administración de Django.
​[ ] Asignar los permisos correspondientes a cada grupo:
​Administradores: Todos los permisos sobre el modelo de Eventos (add, change, delete, view).
​Organizadores: Permisos para add, change y view eventos.
​Asistentes: Permiso para view eventos.
​[ ] Crear usuarios de prueba y asignarlos a los diferentes roles para verificar los permisos.
​4. Uso de Mixins en el Modelo Auth
​[ ] Aplicar LoginRequiredMixin a todas las vistas que requieran que el usuario esté autenticado (crear, editar, ver detalle de evento privado).
​[ ] Usar PermissionRequiredMixin en las vistas de edición y eliminación para restringir el acceso:
​Vista de creación/edición: Requiere el permiso yourapp.change_event.
​Vista de eliminación: Requiere el permiso yourapp.delete_event.
​5. Redirección de Accesos No Autorizados
​[ ] Crear una plantilla HTML (acceso_denegado.html) para mostrar un mensaje de error amigable.
​[ ] Configurar el proyecto para que redirija a esta página cuando un usuario intente acceder a una URL para la que no tiene permisos.
​6. Manejo de Errores y Mensajes
​[ ] Utilizar el framework de mensajes de Django (django.contrib.messages) en las vistas.
​[ ] Implementar messages.error cuando un usuario intente realizar una acción no permitida (por ejemplo, al fallar la validación de un PermissionRequiredMixin).
​[ ] Mostrar los mensajes en las plantillas HTML para dar feedback al usuario.
​7. Ejecución de Migraciones
​[ ] Crear o modificar los modelos necesarios para la gestión de eventos.
​[ ] Ejecutar python manage.py makemigrations para crear los archivos de migración.
​[ ] Aplicar las migraciones con python manage.py migrate y verificar que las tablas se creen correctamente en la base de datos.
​8. Exploración de la Tabla auth_permission
​[ ] Acceder a la base de datos (usando dbeaver, pgadmin o la shell de la BBDD) y examinar el contenido de la tabla auth_permission.
​[ ] Identificar los permisos creados automáticamente por Django para los modelos del proyecto.
​[ ] Verificar en las tablas auth_user_groups y auth_group_permissions cómo se asignan los permisos a los usuarios a través de los grupos.
​9. Configuración de Seguridad
​[ ] Revisar y configurar las opciones de seguridad en settings.py.
​[ ] Asegurarse de que el middleware de sesión (django.contrib.sessions.middleware.SessionMiddleware) esté activo.
​[ ] En un entorno de producción, configurar SECURE_SSL_REDIRECT = True, SESSION_COOKIE_SECURE = True, y CSRF_COOKIE_SECURE = True para forzar el uso de HTTPS.