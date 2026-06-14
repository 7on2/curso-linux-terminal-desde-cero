# Laboratorio: Gestión de Paquetes

## Objetivo

Aprender a instalar, actualizar y eliminar software en Linux usando APT. Practicar búsqueda de paquetes, gestión de repositorios y limpieza del sistema.

---

## Parte 1: Actualizar el Sistema

### Paso 1: actualizar lista de paquetes

```bash
sudo apt update
```

Salida esperada:

```text
Hit:1 http://archive.ubuntu.com/ubuntu jammy InRelease
Get:2 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]
...
Reading package lists... Done
```

### Paso 2: ver actualizaciones disponibles

```bash
apt list --upgradable
```

### Paso 3: actualizar paquetes

```bash
sudo apt upgrade -y
```

### Paso 4: actualización completa

```bash
sudo apt full-upgrade -y
```

---

## Parte 2: Buscar Paquetes

### Paso 1: buscar por nombre

```bash
apt search nginx
```

### Paso 2: buscar por descripción

```bash
apt search "web server"
```

### Paso 3: ver información de un paquete

```bash
apt show nginx
```

Salida esperada:

```text
Package: nginx
Version: 1.18.0-6ubuntu14.4
Priority: optional
Section: web
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Description: small, powerful, scalable web/proxy server
 Nginx is a web server that can also be used as a reverse proxy, load
 balancer, mail proxy and HTTP cache.
```

### Paso 4: verificar si un paquete está instalado

```bash
dpkg -l | grep nginx
```

---

## Parte 3: Instalar Paquetes

### Paso 1: instalar un paquete simple

```bash
sudo apt install -y curl
```

### Paso 2: verificar instalación

```bash
curl --version
```

### Paso 3: instalar múltiples paquetes

```bash
sudo apt install -y wget htop tree
```

### Paso 4: verificar instalaciones

```bash
wget --version
htop --version
tree --version
```

---

## Parte 4: Eliminar Paquetes

### Paso 1: eliminar un paquete

```bash
sudo apt remove -y tree
```

### Paso 2: verificar eliminación

```bash
tree --version
```

Debe fallar.

### Paso 3: eliminar con configuración

```bash
sudo apt purge -y htop
```

### Paso 4: eliminar dependencias no usadas

```bash
sudo apt autoremove -y
```

### Paso 5: limpiar caché de paquetes

```bash
sudo apt clean
```

---

## Parte 5: Listar Paquetes

### Paso 1: listar paquetes instalados

```bash
apt list --installed
```

### Paso 2: contar paquetes instalados

```bash
apt list --installed | wc -l
```

### Paso 3: buscar paquetes específicos

```bash
apt list --installed | grep -i python
```

---

## Parte 6: Gestionar Repositorios

### Paso 1: ver repositorios configurados

```bash
cat /etc/apt/sources.list
```

### Paso 2: ver repositorios adicionales

```bash
ls -la /etc/apt/sources.list.d/
```

### Paso 3: agregar un repositorio PPA

```bash
sudo add-apt-repository ppa:ondrej/php -y
sudo apt update
```

### Paso 4: buscar paquetes del nuevo repositorio

```bash
apt search php8.3
```

---

## Parte 7: Trabajar con Snap

### Paso 1: verificar si snap está instalado

```bash
snap version
```

### Paso 2: buscar paquetes snap

```bash
snap find vlc
```

### Paso 3: instalar un snap

```bash
sudo snap install hello
```

### Paso 4: listar snaps instalados

```bash
snap list
```

### Paso 5: ejecutar el snap

```bash
hello
```

### Paso 6: actualizar snaps

```bash
sudo snap refresh
```

### Paso 7: eliminar un snap

```bash
sudo snap remove hello
```

---

## Parte 8: Instalar desde Código Fuente

### Paso 1: instalar herramientas de compilación

```bash
sudo apt install -y build-essential
```

### Paso 2: crear un programa simple

```bash
cat > hola.c << 'EOF'
#include <stdio.h>

int main() {
    printf("Hola desde código fuente!\n");
    return 0;
}
EOF
```

### Paso 3: compilar

```bash
gcc hola.c -o hola
```

### Paso 4: ejecutar

```bash
./hola
```

### Paso 5: instalar en el sistema

```bash
sudo cp hola /usr/local/bin/
hola
```

---

## Parte 9: Ejercicios

### Ejercicio 1: instalar y configurar un servidor web

```bash
# Instalar Nginx
sudo apt install -y nginx

# Verificar estado
systemctl status nginx

# Probar
curl http://localhost

# Ver página predeterminada
cat /var/www/html/index.nginx-debian.html
```

### Ejercicio 2: instalar herramientas de red

```bash
# Instalar herramientas
sudo apt install -y nmap netcat-openbsd traceroute

# Probar nmap
nmap localhost

# Probar netcat
echo "Hola" | nc -l 1234 &
nc localhost 1234

# Probar traceroute
traceroute google.com
```

### Ejercicio 3: gestionar versiones de Python

```bash
# Buscar versiones de Python disponibles
apt search python3.

# Instalar Python 3.11
sudo apt install -y python3.11

# Verificar versiones
python3 --version
python3.11 --version

# Crear un script
cat > test.py << 'EOF'
print("Hola desde Python")
import sys
print(f"Versión: {sys.version}")
EOF

# Ejecutar con diferentes versiones
python3 test.py
python3.11 test.py
```

---

## Comandos Útiles

### APT

| Comando | Descripción |
|---------|-------------|
| `sudo apt update` | Actualizar lista de paquetes |
| `sudo apt upgrade` | Actualizar paquetes instalados |
| `sudo apt install <paquete>` | Instalar paquete |
| `sudo apt remove <paquete>` | Eliminar paquete |
| `sudo apt purge <paquete>` | Eliminar con configuración |
| `sudo apt autoremove` | Eliminar dependencias no usadas |
| `sudo apt clean` | Limpiar caché |
| `apt search <término>` | Buscar paquete |
| `apt show <paquete>` | Información del paquete |
| `apt list --installed` | Paquetes instalados |

### Snap

| Comando | Descripción |
|---------|-------------|
| `snap find <paquete>` | Buscar snap |
| `sudo snap install <paquete>` | Instalar snap |
| `snap list` | Listar snaps |
| `sudo snap refresh` | Actualizar snaps |
| `sudo snap remove <paquete>` | Eliminar snap |

---

## Errores Frecuentes

| Error | Causa | Solución |
|-------|-------|----------|
| Unable to locate package | Nombre incorrecto | Verificar con `apt search` |
| Could not get lock | Otro proceso usando apt | Esperar o `sudo rm /var/lib/apt/lists/lock` |
| Permission denied | Sin permisos sudo | Usar `sudo` |
| Package not found | Repositorio no configurado | Agregar repositorio o ejecutar `apt update` |
| dpkg was interrupted | Instalación anterior falló | `sudo dpkg --configure -a` |

---

## Limpieza

```bash
# Eliminar paquetes instalados en el lab
sudo apt remove -y curl wget
sudo apt autoremove -y
sudo apt clean

# Eliminar repositorio PPA
sudo add-apt-repository --remove ppa:ondrej/php -y
sudo apt update

# Eliminar programa compilado
sudo rm /usr/local/bin/hola
rm hola hola.c test.py
```
