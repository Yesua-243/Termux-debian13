# Termux-debian13
VNC + XFCE — Configuración rápida
Guía para instalar XFCE, configurar VNC y crear atajos (vncon / vncoff) para levantar y apagar el entorno gráfico.
1. Instalar dependencias
sudo apt update && sudo apt install -y dbus-x11 xfonts-base xfce4 xfce4-session
2. Editar el archivo xstartup
Abrimos el archivo de arranque de VNC:
nano ~/.vnc/xstartup
O lo generamos directamente con el siguiente contenido:
cat << 'EOF' > ~/.vnc/xstartup
#!/bin/bash
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
export DISPLAY=:1
exec dbus-launch --exit-with-session startxfce4
EOF
chmod +x ~/.vnc/xstartup
Ctrl + O para guardar, Ctrl + X para salir.
3. Probar el servidor VNC
vncserver :1 && DISPLAY=:1 dbus-launch --exit-with-session startxfce4 &
4. Crear atajos en .bashrc
Editamos el archivo:
nano ~/.bashrc
Y agregamos al final:
cat << 'EOF' >> ~/.bashrc
 
# Atajo para levantar VNC y cargar XFCE de una
alias vncon='vncserver :1 && DISPLAY=:1 dbus-launch --exit-with-session startxfce4 &'
 
# Atajo para matar la sesión VNC
alias vncoff='vncserver -kill :1; rm -rf /tmp/.X11-unix/X1 /tmp/.X1-lock'
 
EOF
Guardamos, salimos, y aplicamos los cambios:
source ~/.bashrc
5. Uso
Iniciar sesión VNC:
vncon
Apagar sesión VNC:
vncoff
