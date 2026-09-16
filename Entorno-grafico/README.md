# Parte 3 — Instalación y configuración de XFCE4 con VNC

*Desglose de los comandos para instalar y configurar el entorno gráfico XFCE4 con VNC.*

## 1. Instalación del escritorio y el servidor VNC

```bash
sudo apt update && sudo apt install xfce4 xfce4-goodies tightvncserver -y
```

Actualiza la lista de repositorios e instala de un solo golpe el entorno de escritorio ligero XFCE4, sus complementos/utilidades (`xfce4-goodies`) y el servidor VNC (`tightvncserver`).

## 2. Configuración inicial de VNC

```bash
vncserver
```

Arranca el servidor VNC por primera vez para generar los archivos de configuración (`~/.vnc/xstartup`) y pedirte la creación de una contraseña de acceso. (En la opción de "view-only password" eliges `n`).

## 3. Cierre de la sesión de prueba

```bash
vncserver -kill :1
```

Detiene la primera sesión creada en el display `:1` para poder instalar el sistema de mensajes entre procesos antes de la conexión definitiva.

## 4. Instalación del protocolo D-Bus

```bash
sudo apt install dbus-x11 -y
```

Instala `dbus-x11`, una dependencia fundamental para que XFCE4 pueda gestionar la sesión gráfica correctamente, evitando pantallas negras o fallos al abrir aplicaciones dentro de VNC.

## 5. Arranque definitivo del servidor gráfico

```bash
vncserver :1
```

Vuelve a levantar el servidor VNC en el display `:1` (que corresponde al puerto 5901 que usas en la app bVNC Free para conectarte).
