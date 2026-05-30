# Edicion De Configuracion En Linux

## Objetivo

Editar archivos de configuracion desde terminal de forma segura: hacer copia, modificar poco, validar y conservar evidencia del cambio.

## Flujo Seguro De Edicion

Antes de modificar configuracion:

1. Identificar el archivo exacto.
2. Hacer copia de respaldo.
3. Editar solo lo necesario.
4. Validar el contenido.
5. Recargar o reiniciar servicios solo si corresponde.

```mermaid
flowchart LR
    A["Identificar archivo"] --> B["Hacer backup"]
    B --> C["Editar"]
    C --> D["Validar"]
    D --> E["Aplicar cambio"]
```

## Nano

Nano es directo para empezar.

```bash
nano archivo.conf
```

| Accion | Atajo |
|---|---|
| Guardar | `Ctrl + O` |
| Confirmar nombre | `Enter` |
| Salir | `Ctrl + X` |
| Buscar | `Ctrl + W` |

Practica:

```bash
mkdir -p ~/lab-config
echo "PUERTO=8080" > ~/lab-config/app.conf
cp ~/lab-config/app.conf ~/lab-config/app.conf.bak
nano ~/lab-config/app.conf
diff ~/lab-config/app.conf.bak ~/lab-config/app.conf
```

## Vim Basico

Vim aparece en muchos servidores. No hace falta dominarlo al inicio, pero si saber insertar, guardar y salir.

```bash
vim ~/lab-config/vim-demo.txt
```

Secuencia dentro de Vim:

```text
i
Texto escrito desde Vim
Esc
:wq
```

Salir sin guardar:

```text
Esc
:q!
```

## Micro-Lab: Cambio Con Respaldo

```bash
cd ~/lab-config
cp app.conf app.conf.$(date +%Y%m%d%H%M%S).bak
nano app.conf
grep "PUERTO" app.conf
ls -l app.conf*
```

Verifica:

- Existe un backup.
- El archivo editado conserva una linea `PUERTO=...`.
- Puedes explicar que cambiaste y por que.

## Buenas Practicas

- No editar archivos criticos sin copia.
- No reiniciar servicios sin validar sintaxis cuando exista comando de prueba.
- No usar `sudo` si el archivo esta en tu carpeta personal.
- Documentar cambios relevantes en un archivo de notas o commit.

---

[Anterior: Permisos, propietarios y modos](./06-permisos-propietarios-modos.md) | [Laboratorio multiusuario](../laboratorios/entorno-multiusuario-roles.md)

