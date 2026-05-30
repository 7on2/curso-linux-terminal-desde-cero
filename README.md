# Linux y la Terminal Desde Cero

![Linux](https://img.shields.io/badge/Linux-Fundamentos-yellow)
![Terminal](https://img.shields.io/badge/Terminal-Desde%20Cero-black)
![Nivel](https://img.shields.io/badge/Nivel-Inicial-brightgreen)
![Estado](https://img.shields.io/badge/Programa-En%20progreso-blue)

Aprende los fundamentos de Linux y la terminal desde cero, usando Ubuntu Server en VirtualBox como laboratorio seguro. El curso avanza de forma continua: primero terminal y sistema de archivos, luego usuarios, grupos, permisos y edicion de configuracion.

## Ruta De Aprendizaje

| Bloque | Tema | Ir |
|---|---|---|
| 01 | Linux y su importancia actual | [Abrir](./clases/01-linux-importancia.md) |
| 02 | Ubuntu Server en VirtualBox | [Abrir](./clases/02-ubuntu-server-virtualbox.md) |
| 03 | Terminal, shell y sistema de archivos | [Abrir](./clases/03-terminal-sistema-archivos.md) |
| 04 | Comandos esenciales | [Abrir](./clases/04-comandos-esenciales.md) |
| 05 | Identidad en Linux: usuarios, grupos y sudo | [Abrir](./clases/05-identidad-usuarios-grupos-sudo.md) |
| 06 | Permisos, propietarios y modos | [Abrir](./clases/06-permisos-propietarios-modos.md) |
| 07 | Edicion de configuracion | [Abrir](./clases/07-edicion-configuracion.md) |

> El indice sigue el programa completo: Linux y terminal, sistema de archivos, usuarios, permisos, configuracion y laboratorios guiados.

### Mapa Rapido De La Guia

```mermaid
flowchart LR
    A["Linux"] --> B["Distribuciones"]
    B --> C["Ubuntu Server"]
    C --> D["VirtualBox"]
    D --> E["Terminal y Bash"]
    E --> F["Sistema de archivos"]
    F --> G["Comandos esenciales"]
    G --> H["Usuarios y grupos"]
    H --> I["Permisos"]
    I --> J["Configuracion"]
    J --> K["Laboratorios"]

    style A fill:#1f6feb,stroke:#58a6ff,color:#fff
    style B fill:#238636,stroke:#3fb950,color:#fff
    style C fill:#8957e5,stroke:#bc8cff,color:#fff
    style D fill:#30363d,stroke:#8b949e,color:#fff
    style E fill:#9e6a03,stroke:#d29922,color:#fff
    style F fill:#1f6feb,stroke:#58a6ff,color:#fff
    style G fill:#238636,stroke:#3fb950,color:#fff
    style H fill:#8957e5,stroke:#bc8cff,color:#fff
    style I fill:#da3633,stroke:#f85149,color:#fff
    style J fill:#9e6a03,stroke:#d29922,color:#fff
    style K fill:#30363d,stroke:#8b949e,color:#fff
```

## Laboratorio

| Laboratorio | Descripcion | Ir |
|---|---|---|
| Estructura de proyecto en Linux | Crear carpetas, archivos, contenido, copias y validacion desde terminal | [Abrir](./laboratorios/estructura-proyecto-linux.md) |
| Entorno multiusuario por roles | Crear usuarios, grupos, propiedad y permisos para una carpeta compartida | [Abrir](./laboratorios/entorno-multiusuario-roles.md) |

## Material De Apoyo

| Material | Descripcion |
|---|---|
| [Guia visual completa](./material/presentacion-linux-terminal-sesion-1.pdf) | Presentacion principal de la sesion 1: Linux y terminal. |
| [Programa completo en PDF](./material/programa-fundamentos-de-linux.pdf) | Presentacion integrada del programa de Fundamentos de Linux. |
| [Fuente Beamer del programa](./material/programa-fundamentos-de-linux.tex) | Archivo editable para regenerar el PDF del programa. |
| [Guia de instructor](./material/guia-instructor-programa-fundamentos-de-linux.md) | Notas para explicar cada seccion y ejecutar micro-labs durante clase. |

## Recursos Complementarios

| Recurso | Enlace |
|---|---|
| Ubuntu Server | [ubuntu.com/server](https://ubuntu.com/server) |
| Oracle VirtualBox | [virtualbox.org](https://www.virtualbox.org/) |
| Ubuntu CLI Cheat Sheet | [assets.ubuntu.com](https://assets.ubuntu.com/v1/d00791ae-ubuntu_cli_cheat_sheet_2025.pdf) |

## Como Usar Este Repositorio

1. Lee cada clase en orden.
2. Ejecuta los comandos en una VM Ubuntu Server o entorno Linux controlado.
3. Completa los laboratorios y conserva evidencia de la salida.
4. Usa la guia de instructor para ampliar explicaciones y practicar micro-labs.

Al completar estos bloques deberias poder explicar que es Linux, moverte por la terminal, crear estructuras de archivos, gestionar usuarios y grupos, aplicar permisos con criterio y editar configuraciones basicas de forma segura.
