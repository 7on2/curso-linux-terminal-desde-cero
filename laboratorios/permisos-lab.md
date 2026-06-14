# Laboratorio: Permisos en Linux

## Objetivo

Practicar la gestión de permisos en Linux usando `chmod`, `chown` y `chgrp`. Aprender a interpretar permisos simbólicos y octales, y aplicarlos de forma segura.

---

## Parte 1: Entender los Permisos

### Paso 1: crear archivos de práctica

```bash
mkdir -p lab-permisos
cd lab-permisos

echo "Archivo publico" > publico.txt
echo "Archivo privado" > privado.txt
echo "Archivo secreto" > secreto.txt
```

### Paso 2: ver permisos actuales

```bash
ls -la
```

Salida esperada:

```text
total 12
drwxr-xr-x 2 usuario usuario 4096 jun 13 10:00 .
drwxr-xr-x 3 usuario usuario 4096 jun 13 10:00 ..
-rw-r--r-- 1 usuario usuario   16 jun 13 10:00 privado.txt
-rw-r--r-- 1 usuario usuario   17 jun 13 10:00 publico.txt
-rw-r--r-- 1 usuario usuario   18 jun 13 10:00 secreto.txt
```

### Paso 3: interpretar los permisos

| Permiso | Octal | Descripción |
|---------|-------|-------------|
| `rwx` | 7 | Lectura, escritura y ejecución |
| `rw-` | 6 | Lectura y escritura |
| `r-x` | 5 | Lectura y ejecución |
| `r--` | 4 | Solo lectura |
| `---` | 0 | Sin permisos |

Estructura: `rwxrwxrwx` = `propietario` `grupo` `otros`

---

## Parte 2: Permisos Simbólicos

### Paso 1: dar permisos de ejecución al propietario

```bash
chmod u+x publico.txt
ls -la publico.txt
```

Salida esperada:

```text
-rwxr--r-- 1 usuario usuario 17 jun 13 10:00 publico.txt
```

### Paso 2: quitar permisos de lectura a otros

```bash
chmod o-r privado.txt
ls -la privado.txt
```

Salida esperada:

```text
-rw-r----- 1 usuario usuario 16 jun 13 10:00 privado.txt
```

### Paso 3: dar permisos de lectura y ejecución al grupo

```bash
chmod g+rx secreto.txt
ls -la secreto.txt
```

Salida esperada:

```text
-rw-r-xr-- 1 usuario usuario 18 jun 13 10:00 secreto.txt
```

### Paso 4: quitar todos los permisos a otros

```bash
chmod o= secreto.txt
ls -la secreto.txt
```

Salida esperada:

```text
-rw-r----- 1 usuario usuario 18 jun 13 10:00 secreto.txt
```

---

## Parte 3: Permisos Octales

### Paso 1: establecer permisos con octal

```bash
chmod 755 publico.txt
ls -la publico.txt
```

Salida esperada:

```text
-rwxr-xr-x 1 usuario usuario 17 jun 13 10:00 publico.txt
```

Explicación: `755` = `rwxr-xr-x`

### Paso 2: permisos estrictos

```bash
chmod 600 privado.txt
ls -la privado.txt
```

Salida esperada:

```text
-rw------- 1 usuario usuario 16 jun 13 10:00 privado.txt
```

Explicación: `600` = `rw-------`

### Paso 3: permisos de solo lectura para todos

```bash
chmod 444 secreto.txt
ls -la secreto.txt
```

Salida esperada:

```text
-r--r--r-- 1 usuario usuario 18 jun 13 10:00 secreto.txt
```

---

## Parte 4: Cambiar Propietario y Grupo

### Paso 1: crear usuario y grupo de prueba

```bash
sudo useradd -m testuser
sudo groupadd testgroup
```

### Paso 2: cambiar propietario

```bash
sudo chown testuser publico.txt
ls -la publico.txt
```

Salida esperada:

```text
-rwxr-xr-x 1 testuser usuario 17 jun 13 10:00 publico.txt
```

### Paso 3: cambiar grupo

```bash
sudo chgrp testgroup privado.txt
ls -la privado.txt
```

Salida esperada:

```text
-rw------- 1 usuario testgroup 16 jun 13 10:00 privado.txt
```

### Paso 4: cambiar propietario y grupo a la vez

```bash
sudo chown testuser:testgroup secreto.txt
ls -la secreto.txt
```

Salida esperada:

```text
-r--r--r-- 1 testuser testgroup 18 jun 13 10:00 secreto.txt
```

### Paso 5: cambiar recursivamente

```bash
sudo chown -R testuser:testgroup lab-permisos/
ls -la
```

---

## Parte 5: Permisos Especiales

### Paso 1: bit SUID

El bit SUID permite ejecutar un programa con los permisos del propietario.

```bash
ls -l /usr/bin/passwd
```

Salida esperada:

```text
-rwsr-xr-x 1 root root 68208 ... /usr/bin/passwd
```

La `s` en lugar de `x` indica SUID.

### Paso 2: bit SGID

El bit SGID permite ejecutar con los permisos del grupo.

```bash
chmod g+s publico.txt
ls -la publico.txt
```

Salida esperada:

```text
-rwxr-sr-x 1 testuser usuario 17 jun 13 10:00 publico.txt
```

### Paso 3: bit Sticky

El bit Sticky restringe la eliminación de archivos en un directorio.

```bash
chmod +t /tmp
ls -ld /tmp
```

Salida esperada:

```text
drwxrwxrwt 15 root root 4096 jun 13 10:00 /tmp
```

La `t` al final indica Sticky.

---

## Parte 6: Permisos en Directorios

### Paso 1: crear directorio con permisos específicos

```bash
mkdir directorio-secreto
chmod 700 directorio-secreto
ls -ld directorio-secreto
```

Salida esperada:

```text
drwx------ 2 usuario usuario 4096 jun 13 10:00 directorio-secreto
```

### Paso 2: crear archivo dentro

```bash
echo "contenido" > directorio-secreto/archivo.txt
ls -la directorio-secreto/
```

### Paso 3: probar acceso

```bash
# Como usuario normal
cat directorio-secreto/archivo.txt

# Cambiar a otro usuario
sudo -u testuser cat directorio-secreto/archivo.txt
```

El segundo comando debe fallar porque `testuser` no tiene permisos.

---

## Parte 7: Ejercicios

### Ejercicio 1: configurar permisos para un proyecto

```bash
mkdir proyecto
cd proyecto

echo "README" > README.md
echo "config=true" > config.ini
echo "#!/bin/bash\necho 'Hola'" > script.sh
```

Configurar:

- `README.md`: lectura para todos (644)
- `config.ini`: lectura y escritura solo para propietario (600)
- `script.sh`: ejecutable para todos (755)

```bash
chmod 644 README.md
chmod 600 config.ini
chmod 755 script.sh
ls -la
```

### Ejercicio 2: configurar un directorio compartido

```bash
mkdir compartido
sudo chown usuario:usuarios compartido
chmod 775 compartido
chmod g+s compartido
ls -ld compartido
```

---

## Comandos Útiles

| Comando | Descripción |
|---------|-------------|
| `chmod <modo> <archivo>` | Cambiar permisos |
| `chown <usuario> <archivo>` | Cambiar propietario |
| `chgrp <grupo> <archivo>` | Cambiar grupo |
| `chown <usuario>:<grupo> <archivo>` | Cambiar propietario y grupo |
| `chmod -R <modo> <directorio>` | Cambiar recursivamente |
| `ls -la` | Ver permisos detallados |

---

## Errores Frecuentes

| Error | Causa | Solución |
|-------|-------|----------|
| Permission denied | Sin permisos de lectura | `chmod +r <archivo>` |
| No se puede ejecutar | Sin permisos de ejecución | `chmod +x <archivo>` |
| No se puede escribir | Sin permisos de escritura | `chmod +w <archivo>` |
| Cambio no aplica | Error de sintaxis | Verificar orden: `u`, `g`, `o`, `a` |

---

## Limpieza

```bash
cd ..
rm -rf lab-permisos
sudo userdel -r testuser
sudo groupdel testgroup
```
