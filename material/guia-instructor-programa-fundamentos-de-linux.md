# Guia de instructor - Fundamentos de Linux

Esta guia acompana el PDF `Programa_Fundamentos_de_Linux.pdf`. La idea no es leer las diapositivas, sino usarlas como mapa visual mientras el instructor explica, demuestra y hace practicar comandos pequenos.

## Uso recomendado

- Mantener una terminal abierta en la VM Ubuntu Server durante toda la clase.
- Cada bloque debe alternar: explicacion breve, demostracion del instructor, practica del alumno, verificacion.
- Antes de cualquier comando destructivo, pedir que el alumno ejecute `pwd` y `ls`.
- Los micro-labs estan pensados para ejecutarse con el usuario normal del laboratorio, por ejemplo `pit`.
- Si se crean usuarios/grupos de prueba, limpiar al final del bloque.

---

## Portada: Fundamentos de Linux

### Para decir

Linux no se aprende solo como una lista de comandos. Se aprende como una forma de operar sistemas: entrar, entender donde estamos, cambiar lo necesario, validar y dejar evidencia. Durante el curso vamos a construir criterio operativo, no solo memoria.

Conectar Linux con DevOps, servidores, nube y ciberseguridad: casi todo lo que despues se automatiza, monitorea o protege empieza con saber moverse bien en una terminal Linux.

### Pregunta para activar

- Donde creen que se usa Linux aunque no lo veamos directamente?
- Que les da mas temor: usar terminal, romper algo o no entender los errores?

---

## Flujo de Cursos Orientado a DevOps

### Para decir

Este curso es la base. Git ayuda a controlar cambios, Docker ayuda a empaquetar aplicaciones, Ansible automatiza infraestructura, pero Linux es el terreno donde todo eso se ejecuta. Si no entiendes usuarios, permisos, procesos, red y archivos, las demas herramientas se vuelven cajas negras.

### Mini demostracion

Mostrar que una misma terminal puede revelar sistema, usuario, red y version.

```bash
whoami
hostname
uname -a
cat /etc/os-release
ip addr
```

### Idea clave

Cada curso posterior asume que el alumno ya puede leer una terminal y entender que esta modificando.

---

## Indice General

### Para decir

El programa esta organizado como una ruta continua. No vamos a pensar en clases aisladas, sino en capacidades acumulativas: primero comprender Linux y la terminal, luego controlar acceso con usuarios y permisos, despues procesos, servicios, automatizacion, red y proyecto final.

### Pregunta para activar

- Si tuvieran que administrar un servidor hoy, que seria lo primero que revisarian?

---

## Linux y Terminal desde Cero

### Para decir

El objetivo de este bloque es quitar la idea de que Linux es "solo comandos dificiles". Linux es un sistema operativo con una organizacion clara: usuarios, procesos, archivos, servicios y red. La terminal es simplemente la herramienta mas directa para hablar con ese sistema.

### Micro-lab: reconocer el entorno

```bash
whoami
hostname
pwd
date
uptime
cat /etc/os-release
```

### Verificacion

Pedir al alumno que explique:

- Que usuario esta usando.
- En que maquina esta.
- En que directorio se encuentra.
- Que distribucion esta ejecutando.

---

## Linux y su importancia actual

### Para decir

Linux domina servidores porque es estable, automatizable y administrable de forma remota. En una laptop uno puede depender de una interfaz grafica; en servidores reales normalmente se trabaja por SSH y terminal. Por eso el foco del curso no es "ver ventanas", sino operar con precision.

El kernel administra recursos; una distribucion agrega paquetes, instalador, configuraciones y herramientas. Ubuntu, Debian, Fedora o Rocky Linux comparten la idea central, pero cambian en gestion de paquetes, ciclo de soporte y enfoque.

### Micro-lab: kernel vs distribucion

```bash
uname -r
uname -m
cat /etc/os-release
lsb_release -a 2>/dev/null || echo "lsb_release no instalado"
```

### Para reforzar

- `uname -r` habla del kernel.
- `/etc/os-release` habla de la distribucion.
- La arquitectura (`x86_64`, `aarch64`) afecta compatibilidad de paquetes.

---

## Que es Linux

### Para decir

Linux no es una sola "version". En la practica usamos distribuciones. Una distribucion es Linux mas decisiones: que paquetes trae, como actualiza, como instala software y como configura el sistema.

Ejemplo: Ubuntu Server es amigable para aprender y muy usado en nube; Debian prioriza estabilidad; Rocky/RHEL se usa mucho en empresa; Kali esta orientado a seguridad ofensiva y laboratorios.

### Micro-lab: explorar componentes visibles

```bash
ls /
ls /boot
ls /etc | head
cat /etc/shells
echo $SHELL
```

### Frase util

"Linux es el motor; la distribucion es el vehiculo completo listo para usar."

---

## Por que Linux domina servidores, nube y ciberseguridad

### Para decir

En servidores interesa que el sistema sea repetible, administrable por scripts y estable durante mucho tiempo. Linux permite automatizar casi todo por comandos y archivos de configuracion. En nube, contenedores y herramientas de seguridad, esa capacidad es esencial.

### Micro-lab: observar recursos del servidor

```bash
uptime
free -h
df -h
ps aux | head
ss -tulpn 2>/dev/null || ss -tuln
```

### Preguntas

- Que comando muestra memoria?
- Que comando muestra disco?
- Que comando muestra procesos?
- Que comando muestra puertos?

---

## Distribuciones Linux

### Para decir

La familia de una distribucion define como instalamos software y como recibimos actualizaciones. No es lo mismo administrar Ubuntu que Fedora o Arch, aunque muchas ideas sean comunes.

### Micro-lab: identificar familia y gestor

```bash
cat /etc/os-release
command -v apt
command -v dnf
command -v pacman
command -v zypper
```

### Comparacion rapida para mencionar

- Debian/Ubuntu: `apt`, paquetes `.deb`.
- Red Hat/Fedora/Rocky: `dnf`, paquetes `.rpm`.
- Arch/Manjaro: `pacman`.
- openSUSE/SUSE: `zypper`.

---

## Entornos de escritorio vs gestores de ventanas

### Para decir

Un servidor no necesita escritorio grafico para funcionar. De hecho, muchas veces es mejor que no lo tenga: consume menos recursos, reduce superficie de ataque y obliga a administrar por terminal.

### Micro-lab: comprobar si hay entorno grafico

```bash
echo $XDG_CURRENT_DESKTOP
systemctl get-default
who
tty
```

### Interpretacion

- Si `systemctl get-default` devuelve `multi-user.target`, el sistema arranca sin GUI.
- Si devuelve `graphical.target`, arranca con entorno grafico.

---

## Paqueterias y gestores de paquetes

### Para decir

Instalar software no deberia ser descargar archivos al azar. Un gestor de paquetes descarga desde repositorios confiables, resuelve dependencias y registra lo instalado. Esto permite mantener y auditar el sistema.

### Micro-lab: consultar paquetes sin instalar nada peligroso

```bash
sudo apt update
apt search tree | head
apt show tree
dpkg -l | head
```

### Micro-lab opcional: instalar utilidad pequena

```bash
sudo apt install -y tree
tree --version
```

### Buen criterio

Antes de instalar, preguntarse: de que repositorio viene, para que lo necesito y como lo desinstalo?

---

## Formatos universales de instalacion

### Para decir

Snap, Flatpak y AppImage son formatos utiles, sobre todo en escritorio. En servidores se prefiere lo mas simple y auditable: repositorios oficiales o paquetes controlados. Menos formatos significa menos puntos de falla.

### Micro-lab: revisar si snap existe

```bash
command -v snap
snap list 2>/dev/null || echo "snap no disponible o no usado"
```

### Nota para clase

No convertir esto en una guerra de formatos. El criterio es: usar lo que el entorno requiere y lo que se pueda mantener.

---

## Ubuntu Server en VirtualBox

### Para decir

La VM es nuestro laboratorio seguro. Si rompemos algo, no afectamos el equipo principal. Esto permite aprender de verdad: probar, equivocarse, reconstruir y repetir.

### Checklist verbal

- La VM debe tener suficiente RAM y disco.
- La red NAT sirve para empezar.
- El usuario creado debe poder usar `sudo`.
- Instalar OpenSSH ayuda cuando practiquemos acceso remoto.

### Micro-lab: validar la VM

```bash
hostname
whoami
id
ip addr
ping -c 3 8.8.8.8
ping -c 3 google.com
```

### Interpretacion

- Si `8.8.8.8` responde pero `google.com` no, el problema probablemente es DNS.
- Si ninguno responde, revisar red de VirtualBox.

---

## Requisitos para la instalacion

### Para decir

Los recursos no tienen que ser enormes. Para aprender terminal, usuarios y archivos, 2 GB de RAM y 20 GB de disco dinamico son suficientes. Lo importante es que la VM arranque estable y tenga red.

### Micro-lab: revisar recursos desde Linux

```bash
free -h
df -h
lscpu | head
ip route
```

### Pregunta

- Que recurso se agotaria primero si instalamos muchos paquetes o generamos logs grandes?

---

## Crear la maquina virtual

### Para decir

Las decisiones iniciales importan: nombre de host, usuario, disco, red y SSH. En servidores reales documentar estas decisiones evita confusiones.

### Micro-lab: documentar la VM

```bash
mkdir -p ~/proyecto-linux/docs
{
  echo "Hostname: $(hostname)"
  echo "Usuario: $(whoami)"
  echo "Fecha: $(date)"
  echo "IP:"
  ip -brief addr
} > ~/proyecto-linux/docs/vm-info.txt
cat ~/proyecto-linux/docs/vm-info.txt
```

### Evidencia

El alumno debe dejar un archivo con datos basicos de su laboratorio.

---

## Primer ingreso al servidor

### Para decir

Al entrar a un servidor, no se empieza cambiando cosas. Primero se observa: quien soy, donde estoy, que maquina es, que red tiene y que privilegios tengo.

### Micro-lab: rutina de ingreso

```bash
whoami
hostname
pwd
id
groups
ip -brief addr
sudo -l
```

### Regla

"Observar antes de modificar."

---

## Terminal, shell y sistema de archivos

### Para decir

La terminal es la interfaz. La shell es quien interpreta comandos. El sistema de archivos es el arbol donde vive todo. En Linux no pensamos en `C:` o `D:`, pensamos en rutas que cuelgan de `/`.

### Micro-lab: rutas absolutas y relativas

```bash
pwd
cd /
pwd
cd /home
pwd
cd ~
pwd
mkdir -p practica/rutas
cd practica
pwd
cd rutas
pwd
cd ..
pwd
```

### Pregunta

- Cual fue una ruta absoluta?
- Cual fue una ruta relativa?

---

## Estructura basica del sistema

### Para decir

Cada directorio tiene una intencion. `/home` guarda trabajo de usuarios, `/etc` configuracion, `/var` datos variables como logs, `/tmp` temporales. No hay que memorizar todo el arbol, pero si reconocer los lugares importantes.

### Micro-lab: recorrido controlado

```bash
ls /
ls /home
ls /etc | head
ls /var
ls /tmp
ls /bin | head
```

### Reto corto

Pedir que encuentren:

- Donde esta su carpeta personal.
- Donde suelen vivir configuraciones.
- Donde se guardan datos variables.

---

## Comandos para navegar

### Para decir

Navegar bien es una habilidad base. Muchos errores graves pasan porque el usuario no sabe donde esta antes de ejecutar un comando.

### Micro-lab: navegacion

```bash
cd ~
pwd
ls
mkdir -p lab-navegacion/uno/dos/tres
cd lab-navegacion
pwd
ls
cd uno/dos
pwd
cd ..
pwd
cd ~
pwd
```

### Verificacion

Pedir que expliquen que hizo cada `cd`.

---

## Comandos para crear y gestionar

### Para decir

Crear, copiar, mover y borrar son operaciones diarias. El riesgo esta en borrar o mover desde la ruta equivocada. Por eso repetimos `pwd` y `ls` como habito.

### Micro-lab: crear y mover sin riesgo

```bash
cd ~
mkdir -p lab-archivos/{entrada,procesado,backup}
touch lab-archivos/entrada/datos.txt
echo "linea inicial" > lab-archivos/entrada/datos.txt
cp lab-archivos/entrada/datos.txt lab-archivos/backup/datos.bak
mv lab-archivos/entrada/datos.txt lab-archivos/procesado/datos-final.txt
ls -R lab-archivos
cat lab-archivos/procesado/datos-final.txt
```

### Micro-lab: borrado seguro

```bash
pwd
ls lab-archivos/backup
rm lab-archivos/backup/datos.bak
ls lab-archivos/backup
```

### Advertencia para decir

No usar `rm -rf` como reflejo. Primero verificar ruta.

---

## Ver contenido de archivos

### Para decir

No siempre abrimos un editor. Muchas veces solo necesitamos ver el inicio, el final o navegar un archivo largo. `cat`, `head`, `tail` y `less` resuelven situaciones distintas.

### Micro-lab: lectura

```bash
cd ~
seq 1 50 > numeros.txt
cat numeros.txt
head numeros.txt
tail numeros.txt
less numeros.txt
```

Dentro de `less`:

```text
q   salir
/10 buscar 10
n   siguiente coincidencia
```

### Pregunta

- Que comando usarias para ver las ultimas lineas de un log?

---

## Laboratorio: estructura de proyecto en Linux

### Para decir

Este laboratorio convierte comandos sueltos en una estructura real. La idea es ordenar archivos por proposito: documentacion, scripts, datos y respaldos.

### Laboratorio guiado completo

```bash
cd ~
mkdir -p proyecto-linux/{docs,scripts,data,backups}
cd proyecto-linux
touch README.txt docs/notas.txt scripts/inicio.sh
echo "Proyecto Linux - Bloque inicial" > README.txt
echo "Comandos practicados:" > docs/notas.txt
echo "pwd, ls, cd, mkdir, touch, cp, mv" >> docs/notas.txt
cp README.txt backups/README.bak
mv docs/notas.txt docs/comandos-basicos.txt
ls -R
```

### Validacion

```bash
pwd
tree . 2>/dev/null || find . -maxdepth 3 -type f -o -type d
cat README.txt
cat docs/comandos-basicos.txt
```

### Pregunta de cierre

- Que comandos modificaron el sistema?
- Que comandos solo consultaron informacion?

---

## Usuarios, Permisos y Sistema de Archivos

### Para decir

Hasta ahora trabajamos como un usuario. En sistemas reales hay muchos usuarios, procesos y servicios compartiendo recursos. Linux protege esos recursos con identidad, propiedad y permisos.

La pregunta central del bloque es: quien puede leer, escribir o ejecutar que?

### Micro-lab de apertura

```bash
whoami
id
groups
ls -ld ~
ls -l ~ | head
```

### Idea clave

Un permiso no es decoracion: es una regla de acceso.

---

## Como Linux decide quien puede hacer que

### Para decir

Linux evalua tres categorias: usuario propietario, grupo propietario y otros. Cada archivo tiene propietario y grupo. Cuando un proceso intenta acceder, el sistema compara la identidad del proceso con esos datos y aplica los permisos correspondientes.

### Micro-lab: observar propietario y grupo

```bash
cd ~
touch permisos-demo.txt
ls -l permisos-demo.txt
id
groups
```

### Pregunta

- El archivo pertenece al usuario actual?
- Cual es el grupo propietario?
- Que permisos tienen otros usuarios?

---

## Usuarios, root y sudo

### Para decir

`root` puede hacer todo. Justamente por eso no se usa para todo. La practica profesional es operar con usuario normal y elevar con `sudo` solo para acciones administrativas.

`sudo` tambien deja trazabilidad: quien ejecuto que comando y cuando.

### Micro-lab: identidad y privilegios

```bash
whoami
id
groups
sudo -l
sudo whoami
```

### Interpretacion

- `whoami` muestra el usuario normal.
- `sudo whoami` debe mostrar `root` si el usuario tiene permiso.
- `sudo -l` muestra que puede ejecutar el usuario.

---

## Gestion basica de cuentas y grupos

### Para decir

Usuarios y grupos permiten modelar roles. No damos permisos archivo por archivo a personas aisladas si podemos trabajar por grupos: `devops`, `soporte`, `auditoria`, etc.

### Micro-lab: crear usuarios de practica

```bash
sudo adduser ana
sudo adduser luis
sudo groupadd devops
sudo usermod -aG devops ana
sudo usermod -aG devops luis
id ana
id luis
groups ana
groups luis
```

### Punto critico

Explicar `usermod -aG`:

- `-G` define grupos suplementarios.
- `-a` agrega sin borrar los grupos existentes.
- Omitir `-a` puede quitar grupos previos por accidente.

---

## Archivos del sistema relacionados con identidad

### Para decir

Linux guarda identidades en archivos de texto administrados por el sistema. No significa que debamos editarlos a mano siempre. Para usuarios usamos comandos como `adduser`; para `sudoers`, usamos `visudo`.

### Micro-lab: leer sin modificar

```bash
getent passwd ana
getent group devops
sudo tail -n 5 /etc/passwd
sudo tail -n 5 /etc/group
sudo ls -l /etc/passwd /etc/shadow /etc/group /etc/sudoers
```

### Advertencia

No editar `/etc/shadow` manualmente. No editar `/etc/sudoers` con `nano` directo; usar `sudo visudo`.

---

## Permisos, propietarios y modos

### Para decir

La salida de `ls -l` es una radiografia del acceso. Si el alumno aprende a leerla, puede diagnosticar la mayoria de errores de permisos.

### Micro-lab: crear archivo y ver permisos

```bash
cd ~
mkdir -p lab-permisos
cd lab-permisos
echo "secreto de prueba" > reporte.txt
ls -l reporte.txt
stat reporte.txt
```

### Para explicar

En `-rw-r--r--`, el primer caracter indica tipo. Luego vienen tres grupos: usuario, grupo y otros.

---

## Leer permisos con ls -l

### Para decir

No hay que adivinar. `ls -l` nos dice tipo, permisos, enlaces, propietario, grupo, tamano, fecha y nombre. Cada columna ayuda a diagnosticar.

### Micro-lab: comparar archivo y directorio

```bash
cd ~/lab-permisos
mkdir carpeta
touch archivo.txt
ls -ld carpeta
ls -l archivo.txt
```

### Pregunta

- Por que un directorio necesita permiso `x`?

---

## Permisos rwx

### Para decir

En archivos, `r` permite leer, `w` modificar, `x` ejecutar. En directorios, `r` permite listar nombres, `w` crear/borrar/renombrar y `x` entrar o atravesar.

### Micro-lab: permiso de ejecucion

```bash
cd ~/lab-permisos
echo 'echo "Hola desde script"' > hola.sh
ls -l hola.sh
./hola.sh
chmod u+x hola.sh
ls -l hola.sh
./hola.sh
```

### Interpretacion

El contenido era correcto, pero sin `x` el sistema no lo trataba como ejecutable.

---

## Modo simbolico y modo octal

### Para decir

El modo simbolico es expresivo: "agrega ejecucion al usuario". El modo octal es compacto: `755`, `644`, `700`. Ambos son utiles. Lo importante es entender que permiso resulta.

### Micro-lab: practicar conversion

```bash
cd ~/lab-permisos
touch archivo-640.txt archivo-600.txt archivo-755.sh
chmod 640 archivo-640.txt
chmod 600 archivo-600.txt
chmod 755 archivo-755.sh
ls -l
```

### Pregunta rapida

- Que significa `640`?
- Que significa `755`?
- Por que `600` sirve para archivos sensibles?

---

## chmod: cambiar permisos

### Para decir

`chmod` cambia quien puede leer, escribir o ejecutar. No cambia propietario. Si algo "no funciona por permisos", primero leer con `ls -l`, luego decidir el cambio minimo.

### Micro-lab: permisos minimos

```bash
cd ~/lab-permisos
echo "privado" > privado.txt
chmod 600 privado.txt
ls -l privado.txt
chmod g+r privado.txt
ls -l privado.txt
chmod o-r privado.txt
ls -l privado.txt
```

### Advertencia para decir

`chmod 777` es una salida facil pero insegura. Antes de usarlo, preguntar: quien necesita leer, escribir o ejecutar?

---

## chown y chgrp: cambiar propiedad

### Para decir

`chmod` define permisos; `chown` y `chgrp` definen propiedad. Si el archivo pertenece al usuario o grupo equivocado, cambiar permisos no siempre es la solucion correcta.

### Micro-lab: propiedad con grupo devops

```bash
sudo mkdir -p /srv/demo-propiedad
sudo touch /srv/demo-propiedad/reporte.txt
sudo chown root:devops /srv/demo-propiedad/reporte.txt
sudo chmod 660 /srv/demo-propiedad/reporte.txt
ls -l /srv/demo-propiedad/reporte.txt
```

### Interpretacion

El propietario es `root`, el grupo es `devops`, y solo usuario/grupo pueden leer y escribir.

---

## Permisos recomendados en situaciones comunes

### Para decir

No existe un permiso universal. Elegimos segun uso: archivo publico, script, archivo sensible, carpeta privada o carpeta compartida.

### Micro-lab: aplicar casos

```bash
cd ~/lab-permisos
touch publico.txt secreto.txt
mkdir privada compartida
echo 'echo script' > ejecutar.sh
chmod 644 publico.txt
chmod 600 secreto.txt
chmod 700 privada
chmod 755 ejecutar.sh
ls -ld publico.txt secreto.txt privada ejecutar.sh
```

### Reto

Pedir que propongan permisos para:

- Una llave privada SSH.
- Un archivo HTML publico.
- Una carpeta de trabajo compartida por equipo.

---

## Enlaces simbolicos y enlaces duros

### Para decir

Un enlace simbolico apunta a una ruta. Es como un acceso directo visible. Un enlace duro apunta al mismo contenido a nivel de inodo. Para configuraciones y administracion diaria, el simbolico suele ser mas facil de entender.

### Micro-lab: enlaces

```bash
cd ~/lab-permisos
echo "contenido original" > original.txt
ln -s original.txt enlace-simbolico.txt
ln original.txt enlace-duro.txt
ls -li original.txt enlace-simbolico.txt enlace-duro.txt
cat enlace-simbolico.txt
cat enlace-duro.txt
rm original.txt
ls -li enlace-simbolico.txt enlace-duro.txt
cat enlace-duro.txt
cat enlace-simbolico.txt
```

### Interpretacion

El enlace simbolico queda roto si desaparece el destino. El enlace duro conserva acceso al contenido.

---

## Edicion de configuracion

### Para decir

Administrar Linux implica editar archivos. La diferencia entre principiante y operador cuidadoso es que el segundo hace copia, cambia poco, valida y recien despues reinicia servicios.

### Micro-lab: editar archivo seguro

```bash
cd ~
mkdir -p lab-config
echo "PUERTO=8080" > lab-config/app.conf
cp lab-config/app.conf lab-config/app.conf.bak
nano lab-config/app.conf
diff lab-config/app.conf.bak lab-config/app.conf
```

### Mensaje

Nunca editar configuracion critica sin copia.

---

## Nano

### Para decir

Nano es ideal para empezar porque muestra los atajos. `Ctrl+O` guarda, `Enter` confirma, `Ctrl+X` sale. No hay que tenerle miedo al editor; hay que saber guardar y salir.

### Micro-lab

```bash
nano ~/lab-config/notas.conf
cat ~/lab-config/notas.conf
```

Contenido sugerido para escribir:

```text
SERVICIO=demo
AMBIENTE=lab
ACTIVO=true
```

---

## Vim basico

### Para decir

Vim aparece en muchos servidores. No hace falta dominarlo hoy, pero si sobrevivir: entrar, insertar, guardar y salir.

### Micro-lab

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

Validar:

```bash
cat ~/lab-config/vim-demo.txt
```

### Rescate

Si se equivocan:

```text
Esc
:q!
```

---

## Buenas practicas al editar configuracion

### Para decir

La configuracion vive en archivos, pero el impacto vive en servicios. Cambiar un archivo no siempre aplica inmediatamente. A veces se requiere validar, recargar o reiniciar.

### Micro-lab: flujo seguro simulado

```bash
cd ~/lab-config
cp app.conf app.conf.$(date +%Y%m%d%H%M%S).bak
nano app.conf
grep "PUERTO" app.conf
ls -l app.conf*
```

### Pregunta

- Que evidencia queda de que hicimos backup?
- Como sabriamos que el cambio es correcto?

---

## Laboratorio multiusuario

### Para decir

Ahora juntamos identidad, grupos, propiedad y permisos. El objetivo no es solo ejecutar comandos, sino justificar el modelo de acceso: quien trabaja, quien administra y quien queda fuera.

### Laboratorio completo: entorno por rol

```bash
sudo adduser ana
sudo adduser luis
sudo groupadd devops
sudo usermod -aG devops ana
sudo usermod -aG devops luis
sudo mkdir -p /srv/proyecto
sudo chown root:devops /srv/proyecto
sudo chmod 770 /srv/proyecto
ls -ld /srv/proyecto
```

### Validacion

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

### Preguntas

- Por que el propietario es `root`?
- Por que el grupo es `devops`?
- Que logra `770`?

---

## Limpieza del laboratorio multiusuario

### Para decir

Todo laboratorio debe tener limpieza. En entornos reales, dejar usuarios, grupos o carpetas de prueba puede convertirse en riesgo.

### Comandos

```bash
sudo ls -ld /srv/proyecto
sudo rm -rf /srv/proyecto
sudo deluser ana
sudo deluser luis
sudo groupdel devops
getent passwd ana
getent passwd luis
getent group devops
```

### Cuidado

Antes de `rm -rf`, confirmar la ruta exacta. El comando no pregunta dos veces.

---

## Checklist de aprendizaje

### Para decir

El checklist no es decorativo. Sirve para que el alumno se autoevalúe. Si no puede explicar un punto con sus palabras, aun no esta listo para pasar al siguiente bloque.

### Dinamica

Pedir a cada alumno que elija un punto y lo demuestre con un comando. Ejemplos:

```bash
id
ls -l
chmod 640 archivo.txt
sudo chown root:devops archivo.txt
nano archivo.txt
```

---

## Resumen: usuarios, permisos y archivos

### Para decir

El bloque cierra con una idea profesional: seguridad minima necesaria. No se trata de bloquear todo ni abrir todo. Se trata de dar a cada usuario y grupo el acceso que realmente necesita.

### Cierre practico

Pedir que expliquen este comando:

```bash
sudo chown root:devops /srv/proyecto
sudo chmod 770 /srv/proyecto
```

Respuesta esperada:

- `root` administra la carpeta.
- `devops` es el grupo autorizado.
- Usuario y grupo tienen acceso total.
- Otros no tienen acceso.

---

## Banco de comandos rapidos para clase

### Diagnostico inicial

```bash
whoami
id
groups
hostname
pwd
ip -brief addr
cat /etc/os-release
```

### Archivos y directorios

```bash
ls
ls -la
mkdir -p ruta/subruta
touch archivo.txt
cp origen destino
mv origen destino
rm archivo.txt
```

### Lectura

```bash
cat archivo.txt
head archivo.txt
tail archivo.txt
less archivo.txt
```

### Usuarios y grupos

```bash
sudo adduser usuario
sudo groupadd grupo
sudo usermod -aG grupo usuario
id usuario
groups usuario
```

### Permisos

```bash
ls -l
chmod 644 archivo.txt
chmod 755 script.sh
chmod u+x script.sh
sudo chown usuario:grupo archivo.txt
sudo chgrp grupo archivo.txt
```

### Edicion

```bash
nano archivo.conf
vim archivo.conf
cp archivo.conf archivo.conf.bak
diff archivo.conf.bak archivo.conf
```

