# Laboratorio: Entorno Multiusuario Por Roles

## Objetivo

Crear un entorno donde dos usuarios comparten una carpeta mediante un grupo, usando propiedad y permisos para controlar el acceso.

## Escenario

| Elemento | Valor |
|---|---|
| Grupo | `devops` |
| Usuarios | `ana`, `luis` |
| Carpeta compartida | `/srv/proyecto` |
| Acceso esperado | El grupo puede trabajar; otros no entran |

## Paso 1: Crear Usuarios, Grupo Y Carpeta

```bash
sudo adduser ana
sudo adduser luis
sudo groupadd devops
sudo usermod -aG devops ana
sudo usermod -aG devops luis
sudo mkdir -p /srv/proyecto
```

Validar:

```bash
id ana
id luis
getent group devops
```

## Paso 2: Asignar Propiedad Y Permisos

```bash
sudo chown root:devops /srv/proyecto
sudo chmod 770 /srv/proyecto
ls -ld /srv/proyecto
```

Interpretacion:

- `root` administra la carpeta.
- `devops` es el grupo autorizado.
- `770` permite acceso total al propietario y al grupo.
- Otros usuarios no tienen acceso.

## Paso 3: Validar Como Usuarios Autorizados

```bash
sudo -u ana bash
cd /srv/proyecto
touch ana.txt
ls -l
exit

sudo -u luis bash
cd /srv/proyecto
touch luis.txt
ls -l
exit

sudo ls -la /srv/proyecto
```

## Paso 4: Probar Un Usuario No Autorizado

```bash
sudo adduser invitado
sudo -u invitado bash
cd /srv/proyecto
exit
```

El acceso debe fallar porque `invitado` no pertenece a `devops`.

## Paso 5: Limpieza

Antes de borrar, confirma la ruta:

```bash
sudo ls -ld /srv/proyecto
```

Limpiar:

```bash
sudo rm -rf /srv/proyecto
sudo deluser ana
sudo deluser luis
sudo deluser invitado
sudo groupdel devops
```

Confirmar que ya no existen:

```bash
getent passwd ana
getent passwd luis
getent passwd invitado
getent group devops
```

## Checklist

- Puedo crear usuarios y grupos de laboratorio.
- Puedo agregar usuarios a un grupo con `usermod -aG`.
- Puedo asignar propietario y grupo con `chown`.
- Puedo aplicar permisos `770`.
- Puedo validar acceso con usuarios distintos.
- Puedo limpiar recursos de laboratorio al finalizar.

---

[Anterior: Edicion de configuracion](../clases/07-edicion-configuracion.md) | [Volver al indice](../README.md)

