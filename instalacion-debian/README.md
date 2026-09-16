# Parte 1 — Instalación de Debian en Termux

*Desglose de los comandos para instalar Debian usando PRoot dentro de Termux.*

## Permiso de almacenamiento

```bash
termux-setup-storage
```

Concede a Termux el acceso al almacenamiento interno del dispositivo Android, creando la carpeta vinculada `storage`.

## Actualización del sistema Termux

```bash
pkg update && pkg upgrade -y
```

Sincroniza la lista de paquetes disponibles (`pkg update`) y actualiza los paquetes instalados a su última versión (`pkg upgrade`), usando `-y` para confirmar la instalación de forma automática.

## Instalación de PRoot Distro

```bash
pkg install proot-distro -y
```

Instala la herramienta `proot-distro`, que permite descargar, configurar y ejecutar distribuciones Linux dentro de Android sin necesidad de acceso root.

## Instalación de la distribución Debian

```bash
proot-distro install debian
```

Descarga la imagen del sistema operativo Debian y la despliega en el contenedor virtual de PRoot dentro del almacenamiento de Termux.

## Inicio de sesión en Debian

```bash
proot-distro login debian
```

Inicia la sesión en el entorno de Debian recién instalado (por defecto ingresa como el usuario root).
