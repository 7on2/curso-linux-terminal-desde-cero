# Permisos, Propietarios Y Modos

## Objetivo

Leer permisos en Linux, interpretar propietarios y cambiar accesos usando `chmod`, `chown` y `chgrp` con criterio.

## Leer Permisos Con `ls -l`

```text
-rw-r----- 1 ana devops 1240 may 30 14:10 reporte.txt
drwxr-x--- 2 root devops 4096 may 30 14:15 proyectos
```

Lectura:

- Primer caracter: tipo de archivo (`-` archivo, `d` directorio, `l` enlace).
- Primer bloque `rwx`: permisos del usuario propietario.
- Segundo bloque `rwx`: permisos del grupo propietario.
- Tercer bloque `rwx`: permisos de otros.
- Luego aparecen propietario, grupo, tamano, fecha y nombre.

## Permisos `rwx`

| Permiso | Archivo | Directorio |
|---|---|---|
| `r` | Leer contenido | Listar nombres |
| `w` | Modificar contenido | Crear, borrar o renombrar |
| `x` | Ejecutar archivo | Entrar o atravesar |

## Modo Simbolico Y Octal

```bash
chmod u+x script.sh
chmod g+w reporte.txt
chmod o-r secreto.txt
chmod 755 script.sh
chmod 644 index.html
chmod 600 secreto.txt
chmod 700 carpeta_privada
```

| Modo | Resultado | Uso comun |
|---|---|---|
| `755` | `rwx r-x r-x` | Script o directorio publico ejecutable |
| `644` | `rw- r-- r--` | Archivo publico de lectura |
| `640` | `rw- r-- ---` | Archivo compartido con grupo |
| `600` | `rw- --- ---` | Archivo sensible |
| `700` | `rwx --- ---` | Carpeta privada |

## Micro-Lab: Ejecucion De Un Script

```bash
cd ~
mkdir -p lab-permisos
cd lab-permisos
echo 'echo "Hola desde script"' > hola.sh
ls -l hola.sh
./hola.sh
chmod u+x hola.sh
ls -l hola.sh
./hola.sh
```

El script existia, pero sin permiso de ejecucion no podia ejecutarse directamente.

## Cambiar Propiedad Con `chown` Y `chgrp`

```bash
sudo mkdir -p /srv/demo-propiedad
sudo touch /srv/demo-propiedad/reporte.txt
sudo chown root:devops /srv/demo-propiedad/reporte.txt
sudo chmod 660 /srv/demo-propiedad/reporte.txt
ls -l /srv/demo-propiedad/reporte.txt
```

Comandos clave:

```bash
sudo chown ana reporte.txt
sudo chown ana:devops reporte.txt
sudo chgrp devops reporte.txt
sudo chown -R ana:devops proyecto/
```

## Enlaces Simbolicos Y Duros

```bash
cd ~/lab-permisos
echo "contenido original" > original.txt
ln -s original.txt enlace-simbolico.txt
ln original.txt enlace-duro.txt
ls -li original.txt enlace-simbolico.txt enlace-duro.txt
```

Un enlace simbolico apunta a una ruta. Un enlace duro comparte el mismo inodo del archivo.

## Regla Practica

No uses `chmod 777` como solucion rapida. Primero responde:

- Quien necesita leer?
- Quien necesita escribir?
- Quien necesita ejecutar o entrar?
- El acceso debe ser para usuario, grupo u otros?

---

[Anterior: Identidad en Linux](./05-identidad-usuarios-grupos-sudo.md) | [Siguiente: Edicion de configuracion](./07-edicion-configuracion.md)

