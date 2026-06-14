# Servicios y systemd

## Objetivo

Entender qué son los servicios en Linux, cómo se gestionan con systemd y cómo verificar su estado, iniciarlos, detenerlos y habilitarlos al arranque.

---

## 1. ¿Qué es un Servicio?

Un servicio (o daemon) es un proceso que se ejecuta en segundo plano, generalmente sin intervención del usuario. Ejemplos comunes:

| Servicio | Función |
|----------|---------|
| `nginx` | Servidor web |
| `sshd` | Conexiones SSH remotas |
| `cron` | Tareas programadas |
| `mysql` | Base de datos |
| `ufw` | Firewall |

---

## 2. systemd: El Sistema de Init

systemd es el sistema de init moderno que gestiona servicios en la mayoría de distribuciones Linux actuales (Ubuntu, Debian, CentOS, Fedora, etc.).

### Comando principal

```bash
systemctl <acción> <servicio>
```

---

## 3. Acciones Básicas de systemctl

### Ver estado de un servicio

```bash
systemctl status <servicio>
```

Ejemplo:

```bash
systemctl status ssh
```

Salida esperada:

```text
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since ...
```

### Iniciar un servicio

```bash
sudo systemctl start <servicio>
```

### Detener un servicio

```bash
sudo systemctl stop <servicio>
```

### Reiniciar un servicio

```bash
sudo systemctl restart <servicio>
```

### Recargar configuración sin reiniciar

```bash
sudo systemctl reload <servicio>
```

---

## 4. Habilitar y Deshabilitar Servicios

### Habilitar al arranque

```bash
sudo systemctl enable <servicio>
```

Esto crea un enlace simbólico que inicia el servicio automáticamente al encender el sistema.

### Deshabilitar al arranque

```bash
sudo systemctl disable <servicio>
```

### Verificar si está habilitado

```bash
systemctl is-enabled <servicio>
```

---

## 5. Listar Servicios

### Listar todos los servicios activos

```bash
systemctl list-units --type=service --state=running
```

### Listar todos los servicios (activos e inactivos)

```bash
systemctl list-units --type=service
```

### Listar servicios habilitados al arranque

```bash
systemctl list-unit-files --type=service --state=enabled
```

---

## 6. Tipos de Unidades

systemd gestiona diferentes tipos de unidades:

| Tipo | Extensión | Ejemplo |
|------|-----------|---------|
| Servicio | `.service` | `nginx.service` |
| Socket | `.socket` | `cups.socket` |
| Timer | `.timer` | `apt-daily.timer` |
| Mount | `.mount` | `home.mount` |

Generalmente, puedes omitir la extensión:

```bash
systemctl status nginx
# Equivale a:
systemctl status nginx.service
```

---

## 7. Archivos de Unidad

Los archivos de unidad están en:

| Ruta | Descripción |
|------|-------------|
| `/lib/systemd/system/` | Unidades del sistema (paquetes instalados) |
| `/etc/systemd/system/` | Unidades personalizadas (sobrescriben las del sistema) |

### Ejemplo de archivo de unidad

```ini
[Unit]
Description=Mi aplicación web
After=network.target

[Service]
Type=simple
User=www-data
ExecStart=/usr/bin/python3 /opt/mi-app/app.py
Restart=always

[Install]
WantedBy=multi-user.target
```

---

## 8. Ver Logs de un Servicio

### Logs en tiempo real

```bash
journalctl -u <servicio> -f
```

### Logs recientes

```bash
journalctl -u <servicio> --since "1 hour ago"
```

### Logs de la última arranque

```bash
journalctl -u <servicio> -b
```

---

## 9. Estados Comunes de un Servicio

| Estado | Significado |
|--------|-------------|
| `active (running)` | Ejecutándose normalmente |
| `active (exited)` | Ejecutó una vez y terminó |
| `inactive (dead)` | No está ejecutándose |
| `failed` | Falló al iniciar o durante ejecución |
| `starting` | Iniciando |
| `stopping` | Deteniendo |

---

## Comandos Resumen

| Comando | Descripción |
|---------|-------------|
| `systemctl status <servicio>` | Ver estado |
| `sudo systemctl start <servicio>` | Iniciar |
| `sudo systemctl stop <servicio>` | Detener |
| `sudo systemctl restart <servicio>` | Reiniciar |
| `sudo systemctl reload <servicio>` | Recargar configuración |
| `sudo systemctl enable <servicio>` | Habilitar al arranque |
| `sudo systemctl disable <servicio>` | Deshabilitar al arranque |
| `systemctl is-enabled <servicio>` | Verificar si está habilitado |
| `systemctl list-units --type=service` | Listar servicios |
| `journalctl -u <servicio> -f` | Ver logs en tiempo real |

---

## Siguiente

[Gestión de paquetes](./09-gestion-paquetes.md)
