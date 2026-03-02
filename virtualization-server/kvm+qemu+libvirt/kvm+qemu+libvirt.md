

# KVM + QEMU + LIBVIRT

## 1. INSTALL KVM + QEMU + LIBVIRT

-

    $ sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients virt-manager

### KVM (El Motor)

¿Qué es?: Un módulo del núcleo (kernel) de Linux.
¿Para qué sirve?: Convierte a Linux en un "Hipervisor". Permite que el software acceda directamente a la potencia del procesador (aceleración por hardware). Sin KVM, las máquinas virtuales serían increíblemente lentas porque el procesador no las ayudaría.

### QEMU (El Chasis y Componentes)

¿Qué es?: Un emulador de hardware.
¿Para qué sirve?: KVM solo maneja el procesador y la memoria, pero una PC necesita más cosas (tarjeta de video, puertos USB, discos duros, tarjetas de red). QEMU emula todos esos componentes físicos para que el sistema operativo que instales crea que está corriendo en una computadora real.

### Libvirt (El Volante y Tablero)

¿Qué es?: Una API o capa de gestión.
¿Para qué sirve?: KVM y QEMU son muy complejos de configurar manualmente con comandos gigantescos. Libvirt es la herramienta que organiza todo: guarda la configuración de tus máquinas en archivos XML y te da comandos sencillos (como virsh) para encenderlas, apagarlas o clonarlas.

<hr>

## 2. ADD USER TO KVM

- 

    $ sudo adduser $USER kvm



## 3. NET CONFIGURATION (Bridge Networking)

- Para que tus máquinas virtuales (VMs) se comporten como equipos reales en tu red y no solo "detrás" del servidor, debes configurar un Bridge en Netplan:

Edita tu archivo en /etc/netplan/.
Define una interfaz br0 que contenga tu interfaz física (ej. eth0 o enp3s0).
Esto permite que las VMs obtengan su propia IP de tu router.


## 4. GUI GESTION

- Tienes tres formas principales de administrar tus máquinas virtuales:

* CLI (Línea de comandos): Usando el comando virsh para encender, apagar o configurar.
Virt-Manager: Una interfaz gráfica excelente si te conectas desde otro Linux con escritorio.
Cockpit: Una interfaz web moderna para Ubuntu. Instálala con sudo apt install cockpit cockpit-machines y accede desde tu navegador en el puerto 9090.

* Virt-Manager: Una interfaz gráfica excelente si te conectas desde otro Linux con escritorio.
Cockpit: Una interfaz web moderna para Ubuntu. Instálala con sudo apt install cockpit cockpit-machines y accede desde tu navegador en el puerto 9090.

* Cockpit: Una interfaz web moderna para Ubuntu. Instálala con sudo apt install cockpit cockpit-machines y accede desde tu navegador en el puerto 9090.


### 4.1 Virt Manager

- Para instalar Virt-Manager en Ubuntu Server 24.04 tienes dos escenarios. Como Virt-Manager es una aplicación gráfica, lo ideal es instalarla en tu computadora personal (si usas Linux) para controlar el servidor de forma remota.
Aquí tienes los pasos para ambos casos:

1. Instalación en el Servidor (Host)

- Primero, asegúrate de que el servidor tenga los componentes básicos que explicamos antes:

    Comando: 
    
    $ sudo apt update && sudo apt install -y virt-manager libvirt-daemon-system libvirt-clients
    
    Permisos: Agrega tu usuario al grupo de virtualización para no usar sudo siempre:
    
    $ sudo adduser $USER libvirt y sudo adduser $USER kvm
    
    (Debes cerrar sesión y volver a entrar para que aplique).

2. Cómo usarlo (El servidor no tiene pantalla)
Como Ubuntu Server no tiene escritorio, no puedes "abrir" la ventana ahí. Tienes dos opciones:

* Opción A (Desde otra PC con Linux): Instala Virt-Manager en tu laptop con Linux. Ábrelo, ve a Archivo 

    $ 
    
    > Añadir conexión, elige SSH y escribe la IP de tu servidor. Podrás crear máquinas virtuales en el servidor desde tu laptop.
    
* Opción B (X11 Forwarding): Si usas Windows o Mac, puedes conectar por SSH usando el parámetro -X (ej. ssh -X usuario@ip-servidor). Si tienes un servidor de ventanas instalado, al escribir virt-manager en la terminal, la ventana se "teletransportará" a tu escritorio.


### 4.2 Alternativa Web (Recomendada para Server)
- Si no quieres lidiar con aplicaciones gráficas remotas, lo más sencillo para Ubuntu Server 24.04 es Cockpit. Te permite crear VMs desde el navegador:

    Instala: sudo apt install cockpit cockpit-machines
    Accede: Entra en tu navegador a https://tu-ip-servidor:9090

¿Quieres que te explique cómo configurar la conexión remota desde Virt-Manager en otra PC o prefieres probar la interfaz web?


## REBOOT SYSTEM

-