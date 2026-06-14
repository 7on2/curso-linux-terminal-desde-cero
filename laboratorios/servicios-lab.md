# Laboratorio: Servicios y systemd

## Objetivo

Aprender a gestionar servicios en Linux usando systemctl. Practicar iniciar, detener, habilitar, deshabilitar servicios y revisar sus logs.

---

## Parte 1: Explorar Servicios del Sistema

### Paso 1: ver servicios activos

```bash
systemctl list-units --type=service --state=running
```

Salida esperada:

```text
UNIT                     LOAD   ACTIVE SUB     DESCRIPTION
cron.service             loaded active running Regular background program processing
ssh.service              loaded active running OpenBSD Secure Shell server
systemd-logind.service   loaded active running Login Service
```

### Paso 2: ver todos los servicios

```bash
systemctl list-units --type=service
```

### Paso 3: ver servicios habilitados al arranque

```bash
systemctl list-unit-files --type=service --state=enabled
```

---

## Parte 2: Gestionar el Servicio SSH

### Paso 1: verificar estado de SSH

```bash
systemctl status ssh
```

Salida esperada:

```text
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since ...
```

### Paso 2: detener SSH

```bash
sudo systemctl stop ssh
systemctl status ssh
```

Salida esperada:

```text
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: inactive (dead) since ...
```

### Paso 3: iniciar SSH nuevamente

```bash
sudo systemctl start ssh
systemctl status ssh
```

### Paso 4: reiniciar SSH

```bash
sudo systemctl restart ssh
systemctl status ssh
```

---

## Parte 3: Habilitar y Deshabilitar Servicios

### Paso 1: verificar si SSH está habilitado

```bash
systemctl is-enabled ssh
```

Salida esperada:

```text
enabled
```

### Paso 2: deshabilitar SSH

```bash
sudo systemctl disable ssh
systemctl is-enabled ssh
```

Salida esperada:

```text
disabled
```

### Paso 3: habilitar SSH nuevamente

```bash
sudo systemctl enable ssh
systemctl is-enabled ssh
```

Salida esperada:

```text
enabled
```

---

## Parte 4: Trabajar con Nginx

### Paso 1: instalar Nginx

```bash
sudo apt update
sudo apt install -y nginx
```

### Paso 2: verificar estado

```bash
systemctl status nginx
```

### Paso 3: verificar que Nginx responde

```bash
curl http://localhost
```

Salida esperada:

```html
<!DOCTYPE html>
<html>
...
<title>Welcome to nginx!</title>
...
</html>
```

### Paso 4: detener Nginx

```bash
sudo systemctl stop nginx
curl http://localhost
```

El segundo comando debe fallar.

### Paso 5: iniciar Nginx

```bash
sudo systemctl start nginx
curl http://localhost
```

### Paso 6: deshabilitar Nginx al arranque

```bash
sudo systemctl disable nginx
systemctl is-enabled nginx
```

### Paso 7: habilitar Nginx al arranque

```bash
sudo systemctl enable nginx
systemctl is-enabled nginx
```

---

## Parte 5: Crear un Servicio Personalizado

### Paso 1: crear un script simple

```bash
sudo nano /opt/mi-servicio.sh
```

Contenido:

```bash
#!/bin/bash
while true; do
    echo "$(date) - Servicio ejecutándose" >> /var/log/mi-servicio.log
    sleep 10
done
```

### Paso 2: dar permisos de ejecución

```bash
sudo chmod +x /opt/mi-servicio.sh
```

### Paso 3: crear archivo de unidad

```bash
sudo nano /etc/systemd/system/mi-servicio.service
```

Contenido:

```ini
[Unit]
Description=Mi Servicio Personalizado
After=network.target

[Service]
Type=simple
ExecStart=/opt/mi-servicio.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

### Paso 4: recargar systemd

```bash
sudo systemctl daemon-reload
```

### Paso 5: iniciar el servicio

```bash
sudo systemctl start mi-servicio
systemctl status mi-servicio
```

### Paso 6: verificar que funciona

```bash
sleep 15
cat /var/log/mi-servicio.log
```

### Paso 7: habilitar al arranque

```bash
sudo systemctl enable mi-servicio
```

### Paso 8: ver logs con journalctl

```bash
journalctl -u mi-servicio -f
```

Presiona `Ctrl+C` para salir.

---

## Parte 6: Ver Logs de Servicios

### Paso 1: logs de Nginx

```bash
journalctl -u nginx
```

### Paso 2: logs recientes

```bash
journalctl -u nginx --since "10 minutes ago"
```

### Paso 3: logs en tiempo real

```bash
journalctl -u nginx -f
```

### Paso 4: logs de la última arranque

```bash
journalctl -u nginx -b
```

---

## Parte 7: Ejercicios

### Ejercicio 1: gestionar el servicio cron

```bash
# Verificar estado de cron
systemctl status cron

# Detener cron
sudo systemctl stop cron

# Verificar que está detenido
systemctl status cron

# Iniciar cron
sudo systemctl start cron

# Verificar que está corriendo
systemctl status cron
```

### Ejercicio 2: crear un servicio que escriba en un archivo

```bash
# Crear script
sudo nano /opt/contador.sh
```

Contenido:

```bash
#!/bin/bash
CONTADOR=0
while true; do
    CONTADOR=$((CONTADOR + 1))
    echo "Contador: $CONTADOR" >> /var/log/contador.log
    sleep 5
done
```

```bash
# Dar permisos
sudo chmod +x /opt/contador.sh

# Crear servicio
sudo nano /etc/systemd/system/contador.service
```

Contenido:

```ini
[Unit]
Description=Servicio Contador
After=network.target

[Service]
Type=simple
ExecStart=/opt/contador.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
# Recargar y iniciar
sudo systemctl daemon-reload
sudo systemctl start contador
sudo systemctl enable contador

# Verificar
sleep 10
cat /var/log/contador.log
journalctl -u contador --since "1 minute ago"
```

---

## Comandos Útiles

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
| `sudo systemctl daemon-reload` | Recargar unidades |

---

## Errores Frecuentes

| Error | Causa | Solución |
|-------|-------|----------|
| Service not found | Nombre incorrecto | Verificar con `systemctl list-units` |
| Failed to start | Error en el script | Revisar logs con `journalctl` |
| Unit not loaded | No se ejecutó `daemon-reload` | Ejecutar `sudo systemctl daemon-reload` |
| Permission denied | Sin permisos sudo | Usar `sudo` |

---

## Limpieza

```bash
# Detener y deshabilitar servicios personalizados
sudo systemctl stop mi-servicio
sudo systemctl disable mi-servicio
sudo systemctl stop contador
sudo systemctl disable contador

# Eliminar archivos
sudo rm /etc/systemd/system/mi-servicio.service
sudo rm /etc/systemd/system/contador.service
sudo rm /opt/mi-servicio.sh
sudo rm /opt/contador.sh
sudo rm /var/log/mi-servicio.log
sudo rm /var/log/contador.log

# Recargar systemd
sudo systemctl daemon-reload
```
