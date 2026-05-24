# Terminal, Shell Y Sistema De Archivos

## Terminal Y Shell

La **terminal** es la interfaz donde escribimos comandos.

La **shell** es el programa que interpreta esos comandos. En Ubuntu normalmente se usa **Bash**.

```mermaid
flowchart LR
    A["Persona"] --> B["Terminal"]
    B --> C["Shell / Bash"]
    C --> D["Sistema Linux"]

    style A fill:#30363d,stroke:#8b949e,color:#fff
    style B fill:#1f6feb,stroke:#58a6ff,color:#fff
    style C fill:#8957e5,stroke:#bc8cff,color:#fff
    style D fill:#238636,stroke:#3fb950,color:#fff
```

Analogia: la terminal es la ventanilla donde escribes una orden; la shell es quien entiende esa orden y la ejecuta en el sistema.

## Rutas Absolutas Y Relativas

Una **ruta absoluta** empieza desde la raiz del sistema:

```text
/home/pit/documentos/notas.txt
```

Una **ruta relativa** parte desde la ubicacion actual:

```text
documentos/notas.txt
```

En Linux todo vive dentro de un arbol que empieza en `/`. No existen unidades `C:` o `D:` como en Windows.

## Estructura Basica Del Sistema

| Directorio | Uso principal |
|---|---|
| `/` | Raiz del sistema |
| `/home` | Carpetas de usuarios |
| `/etc` | Configuracion del sistema |
| `/var` | Datos variables como logs |
| `/tmp` | Archivos temporales |
| `/bin` | Comandos esenciales |

```mermaid
flowchart TB
    R["/"] --> H["/home"]
    R --> E["/etc"]
    R --> V["/var"]
    R --> T["/tmp"]
    R --> B["/bin"]
    H --> U["/home/pit"]

    style R fill:#1f6feb,stroke:#58a6ff,color:#fff
    style H fill:#238636,stroke:#3fb950,color:#fff
    style U fill:#8957e5,stroke:#bc8cff,color:#fff
```

La primera practica se concentra en moverse por este arbol y crear una estructura propia.

## Idea Clave

Para usar Linux con confianza no necesitas memorizar todo el arbol del sistema desde el primer dia. Necesitas saber donde estas, como moverte y como leer rutas.

---

[Anterior: Ubuntu Server en VirtualBox](./02-ubuntu-server-virtualbox.md) | [Siguiente: Comandos esenciales](./04-comandos-esenciales.md)
