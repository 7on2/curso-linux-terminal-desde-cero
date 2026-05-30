# Laboratorio: Estructura De Proyecto En Linux

## Objetivo

Crear una estructura de proyecto desde la terminal usando comandos basicos de navegacion, creacion, escritura, copia, movimiento y validacion.

Al finalizar tendras esta estructura:

```text
proyecto-linux/
|-- README.txt
|-- backups/
|   `-- README.bak
|-- data/
|-- docs/
|   `-- comandos-basicos.txt
`-- scripts/
    `-- inicio.sh
```

## Requisitos

- Ubuntu Server instalado o una terminal Linux disponible.
- Usuario con acceso a su carpeta personal.
- Conocer comandos basicos: `pwd`, `ls`, `cd`, `mkdir`, `touch`, `cat`, `cp`, `mv`.

## Paso 1: Crear Carpetas Y Archivos

```bash
cd ~
mkdir -p proyecto-linux/{docs,scripts,data,backups}
cd proyecto-linux
touch README.txt docs/notas.txt scripts/inicio.sh
pwd
ls -la
```

La opcion `-p` permite crear carpetas intermedias sin error si ya existen.

## Paso 2: Escribir Y Revisar Contenido

```bash
echo "Proyecto Linux - Bloque inicial" > README.txt
echo "Comandos practicados:" > docs/notas.txt
echo "pwd, ls, cd, mkdir, touch" >> docs/notas.txt
cat README.txt
cat docs/notas.txt
```

En este bloque usamos escritura basica para documentar el laboratorio.

## Paso 3: Copiar, Mover Y Validar

```bash
cp README.txt backups/README.bak
mv docs/notas.txt docs/comandos-basicos.txt
ls -R
```

Resultado esperado: un proyecto ordenado, navegable y documentado desde la terminal.

## Validacion Opcional

```bash
pwd
tree . 2>/dev/null || find . -maxdepth 3 -type f -o -type d
cat README.txt
cat docs/comandos-basicos.txt
```

## Checklist

- Puedo ubicarme con `pwd`.
- Puedo listar archivos con `ls` y `ls -la`.
- Puedo crear carpetas con `mkdir` y `mkdir -p`.
- Puedo crear archivos con `touch`.
- Puedo escribir contenido con `echo`.
- Puedo leer archivos con `cat`.
- Puedo copiar con `cp`.
- Puedo mover o renombrar con `mv`.
- Puedo validar una estructura con `ls -R`.

---

[Anterior: Comandos esenciales](../clases/04-comandos-esenciales.md) | [Siguiente: laboratorio multiusuario](./entorno-multiusuario-roles.md) | [Volver al indice](../README.md)

