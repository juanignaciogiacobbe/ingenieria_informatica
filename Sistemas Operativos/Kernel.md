# <span style="color:#c00000">El Kernel</span>

> Corre directamente en el procesador con derechos irrestringidos(<span style="color:#ffff00">es un programa</span>).
> Cumple el rol de mediador entre los procesos y el hardware -> básicamente, <span style="color:#ffff00">es el encargado de que el SO brinde protección a si mismo y a los programas.</span>
> <span style="color:#ffff00">Puede ser equivalente al termino Sistema Operativo</span>(es la capa de software de mas bajo nivel en la computadora).
> Chequea cada acceso del [[Proceso]] al hardware.

- Es capaz de performar cualquier operación disponible en el hardware, ya que corre directamente en el procesador con permisos ilimitados.
- Las apps también corren en el procesador, pero con derechos restringidos.
- Contiene una capa para la gestión de dispositivos específicos.
- Contiene una serie de servicios para la gestión de dispositivos agnósticos del hardware que son utilizado por las apps. 

![[Pasted image 20240427182354.png]]

## <span style="color:#c00000">Tareas del Kernel
</span>
- Planificar la ejecución de las apps.
- Gestionar la memoria.
- Proveer un file system.
- Creación y planificación de [[Proceso]].
- Acceder a los dispositivos.
- Comunicaciones.
- Proveer un API.

## <span style="color:#c00000">El Kernel de Linux(de tipo monolitico)</span>
- No tiene acceso a la biblioteca C ni a los encabezados C estándar.
- Esta codificado en GNU C.
- Carece de protección de memoria internamente, no se proteje de si mismo.
- No puede ejecutar fácilmente operaciones de floats.
- Tiene un pequeño stack de tamaño fijo y no es dinámica.
- Problemas con sincronizacion y concurrencia.

## <span style="color:#c00000">Tipos de Kernel</span>
- Monolítico: el kernel es un único programa que se ejecuta continuamente en la memoria de la computadora intercambiándose con la ejecución de los procesos de usuario.
- Micro Kernel: el kernel sigue existiendo pero solo implementa funcionalidad básica en el ring 0. Otros servicios se implementan en ring 1 o ring 2, estos servicios no son imprescindibles que se ejecuten en modo kernel exclusivamente.

## <span style="color:#c00000">Iniciando el SO y el kernel</span>
1. Booteo: depende del hardware de la computadora. En el se realizan los chequeos de hardware y se carga el bootloader, que es el único programa encargado de cargar el kernel del SO(carga la BIOS, crea la Interrupt Vector Table y ejecuta el servicio de interrupciones).
2. Una tabla de vectores de interrupción (IVT) es una estructura de datos que asocia una lista de manejadores de interrupciones con una lista de solicitudes de interrupción en una tabla de vectores de interrupción. Cada entrada de la tabla de vectores de interrupción, llamada vector de interrupción, es la dirección de un manejador de interrupciones -> El BIOS genera una interrupción (19), la cual hace ejecutar el servicio de interrupciones.
3. El Kernel inicializa el sistema y setea el ambiente para correr procesos. -> crea algunos procesos iniciales, los cuales a su vez crean otros procesos. -> administra los procesos y les provee de varios servicios (acceso a disco, acceso a network, acceso a usb, etc).
4. Carga del kernel: se pasa a modo supervisor, y se busca al kernel en el dispositivo en el que este almacenado, se carga en memoria principal, se setea el IR, y se ejecuta la primera instrucción del kernel.
5. Inicio de las apps de users: se carga en memoria la app a ejecutar(normalmente la [[Shell]]), se setea el IR en la primera instrucción de esa app, y se switchea a modo usuario.

## <span style="color:#c00000">Informacion guardada en el PCB</span> 
- <span style="color:#ffff00">Identificacion del proceso</span>(PID, PPID, PGID).
- <span style="color:#ffff00">Datos de estado del proceso</span>: Registros de propósito general de la CPU, SP, Instruction pointer.
- <span style="color:#ffff00">Datos de control del proceso</span>: Estado del proceso y otra información de [[Scheduler]], ID de los hijos, datos de IPC(signals y messages), y contadores de tiempo de uso de la CPU.


## <span style="color:#c00000">Kernel Threads</span> 
![[Pasted image 20240427180207.png]]

- Los kernel [[Theads]] ejecutan código del kernel y modifican las estructuras de datos del mismo.
- 