# Gestión de Paquetes

## Objetivo

Aprender a instalar, actualizar y eliminar software en Linux usando gestores de paquetes como `apt` (Debian/Ubuntu) y `dnf` (Fedora/RHEL).

---

## 1. ¿Qué es un Paquete?

Un paquete es un archivo comprimido que contiene:

- Binarios del programa
- Archivos de configuración
- Documentación
- Scripts de instalación

Los gestores de paquetes resuelven dependencias automáticamente.

---

## 2. Gestores de Paquetes Comunes

| Distribución | Gestor | Comando |
|--------------|--------|---------|
| Ubuntu/Debian | APT | `apt` |
| Fedora/RHEL | DNF | `dnf` |
| Arch Linux | Pacman | `pacman` |
| openSUSE | Zypper | `zypper` |

---

## 3. APT (Advanced Package Tool)

APT es el gestor de paquetes para distribuciones basadas en Debian.

### Actualizar lista de paquetes

```bash
sudo apt update
```

Esto descarga la lista de paquetes disponibles desde los repositorios.

### Actualizar paquetes instalados

```bash
sudo apt upgrade
```

### Actualizar todo (incluyendo eliminación de paquetes obsoletos)

```bash
sudo apt full-upgrade
```

---

## 4. Instalar Paquetes

### Instalar un paquete

```bash
sudo apt install <paquete>
```

Ejemplo:

```bash
sudo apt install nginx
```

### Instalar múltiples paquetes

```bash
sudo apt install nginx curl wget
```

### Instalar sin confirmación

```bash
sudo apt install -y <paquete>
```

---

## 5. Eliminar Paquetes

### Eliminar paquete (conserva configuración)

```bash
sudo apt remove <paquete>
```

### Eliminar paquete y configuración

```bash
sudo apt purge <paquete>
```

### Eliminar dependencias no utilizadas

```bash
sudo apt autoremove
```

---

## 6. Buscar Paquetes

### Buscar por nombre

```bash
apt search <término>
```

Ejemplo:

```bash
apt search nginx
```

### Ver información de un paquete

```bash
apt show <paquete>
```

### Listar paquetes instalados

```bash
apt list --installed
```

### Verificar si un paquete está instalado

```bash
dpkg -l | grep <paquete>
```

---

## 7. Repositorios

Los repositorios son servidores que alojan paquetes. APT lee la lista de repositorios desde:

```bash
/etc/apt/sources.list
/etc/apt/sources.list.d/
```

### Ejemplo de línea de repositorio

```text
deb http://archive.ubuntu.com/ubuntu jammy main restricted
```

| Campo | Descripción |
|-------|-------------|
| `deb` | Tipo de paquete (binario) |
| `http://...` | URL del repositorio |
| `jammy` | Nombre en clave de la versión |
| `main restricted` | Componentes |

### Agregar un repositorio PPA

```bash
sudo add-apt-repository ppa:<usuario>/<repositorio>
sudo apt update
```

---

## 8. Paquetes Snap

Snap es un sistema de paquetes universal desarrollado por Canonical.

### Instalar un snap

```bash
sudo snap install <paquete>
```

### Listar snaps instalados

```bash
snap list
```

### Actualizar snaps

```bash
sudo snap refresh
```

### Eliminar un snap

```bash
sudo snap remove <paquete>
```

---

## 9. Paquetes Flatpak

Flatpak es otro sistema de paquetes universal.

### Instalar Flatpak

```bash
sudo apt install flatpak
```

### Agregar repositorio Flathub

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

### Instalar un paquete Flatpak

```bash
flatpak install flathub <paquete>
```

---

## 10. Instalar desde Código Fuente

A veces necesitas compilar software desde el código fuente.

### Pasos generales

```bash
# 1. Descargar código fuente
wget https://ejemplo.com/software-1.0.tar.gz

# 2. Extraer
tar -xzf software-1.0.tar.gz

# 3. Entrar al directorio
cd software-1.0

# 4. Configurar
./configure

# 5. Compilar
make

# 6. Instalar
sudo make install
```

---

## 11. Gestión de Paquetes con DNF

Para distribuciones basadas en RHEL (Fedora, CentOS, RHEL).

### Actualizar lista

```bash
sudo dnf check-update
```

### Instalar paquete

```bash
sudo dnf install <paquete>
```

### Actualizar todo

```bash
sudo dnf upgrade
```

### Eliminar paquete

```bash
sudo dnf remove <paquete>
```

### Buscar paquete

```bash
dnf search <término>
```

---

## Comandos Resumen

### APT

| Comando | Descripción |
|---------|-------------|
| `sudo apt update` | Actualizar lista de paquetes |
| `sudo apt upgrade` | Actualizar paquetes instalados |
| `sudo apt install <paquete>` | Instalar paquete |
| `sudo apt remove <paquete>` | Eliminar paquete |
| `sudo apt purge <paquete>` | Eliminar con configuración |
| `sudo apt autoremove` | Eliminar dependencias no usadas |
| `apt search <término>` | Buscar paquete |
| `apt show <paquete>` | Información del paquete |
| `apt list --installed` | Paquetes instalados |

### DNF

| Comando | Descripción |
|---------|-------------|
| `sudo dnf check-update` | Ver actualizaciones disponibles |
| `sudo dnf install <paquete>` | Instalar paquete |
| `sudo dnf upgrade` | Actualizar paquetes |
| `sudo dnf remove <paquete>` | Eliminar paquete |
| `dnf search <término>` | Buscar paquete |

---

## Siguiente

[Servicios y systemd](./08-servicios-systemd.md)
