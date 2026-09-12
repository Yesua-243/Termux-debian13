# VNC + XFCE — Configuración rápida

*Guía para instalar XFCE, configurar VNC y crear atajos (`vncon` / `vncoff`) para levantar y apagar el entorno gráfico. Soluciona el bug de la pantalla gris.*

## 1. Instalar dependencias

```bash
sudo apt update && sudo apt install -y dbus-x11 xfonts-base xfce4 xfce4-session
```

## 2. Editar el archivo xstartup

Abrimos el archivo de arranque de VNC:

```bash
nano ~/.vnc/xstartup
```

O lo generamos directamente con el siguiente contenido:

```bash
cat << 'EOF' > ~/.vnc/xstartup
#!/bin/bash
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
export DISPLAY=:1
exec dbus-launch --exit-with-session startxfce4
EOF
chmod +x ~/.vnc/xstartup
```

*Ctrl + O para guardar, Ctrl + X para salir.*

## 3. Probar el servidor VNC

```bash
vncserver :1 && DISPLAY=:1 dbus-launch --exit-with-session startxfce4 &
```

## 4. Crear atajos en .bashrc

Editamos el archivo:

```bash
nano ~/.bashrc
```

Y agregamos al final:

```bash
cat << 'EOF' >> ~/.bashrc

# Atajo para levantar VNC y cargar XFCE de una
alias vncon='vncserver :1 && DISPLAY=:1 dbus-launch --exit-with-session startxfce4 &'

# Atajo para matar la sesión VNC
alias vncoff='vncserver -kill :1; rm -rf /tmp/.X11-unix/X1 /tmp/.X1-lock'

EOF
```

Guardamos, salimos, y aplicamos los cambios:

```bash
source ~/.bashrc
```

## 5. Uso

Iniciar sesión VNC:

```bash
vncon
```

Apagar sesión VNC:

```bash
vncoff
```
