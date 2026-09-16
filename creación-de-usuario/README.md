# Parte 2 — Creación de usuario no-root en Debian

*Desglose de los comandos para instalar utilidades de gestión de usuarios y crear una cuenta segura sin privilegios root.*

## Instalación de utilidades esenciales (sudo y adduser)

```bash
apt update && apt install sudo adduser -y
```

Actualiza los repositorios de Debian e instala de forma automática (`-y`) las herramientas `sudo` (gestión de privilegios) y `adduser` (gestor para la creación de usuarios).

## Creación del usuario no-root

```bash
adduser tu_usuario
```

*(En el video se ingresa `jes3`)*

Crea un nuevo usuario estándar con su respectivo directorio `/home`. Durante este proceso solicitará asignar una contraseña, confirmarla, presionar Enter para omitir los campos de información personal y presionar `Y` para validar.

## Asignación de permisos de administración

```bash
usermod -aG sudo tu_usuario
```

Agrega (`-aG`) el usuario recién creado al grupo `sudo`, permitiéndole ejecutar tareas administrativas elevadas de manera segura utilizando la palabra clave `sudo`.

## Acceso a Debian con el usuario seguro

```bash
proot-distro login debian --user tu_usuario
```

Comando ejecutado desde la terminal principal de Termux para iniciar sesión en el contenedor Debian usando directamente la cuenta de usuario seguro (`--user`) en lugar del usuario root.
