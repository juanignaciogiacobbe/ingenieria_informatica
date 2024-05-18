# <span style="color:#c00000">El proceso</span>
> <span style="color:#ffff00">Es la abstracción para una ejecución protegida brindada por el kernel del SO para protegerse a si mismo: es la ejecución de un programa con derechos restringidos</span>.
> 
> Un proceso necesita permiso del kernel antes de acceder a la memoria de otro proceso, antes de leer el disco, antes de cambiar configuraciones del hardware, etc. 

## <span style="color:#c00000">De Programa a Proceso</span>
> Un programa es un archivo que posee toda la información de como construir un proceso en memoria.

1. Un programador crea código en un lenguaje de alto nivel.
2. El compilador convierte ese código en una secuencia de instrucciones de maquina, y las guarda en un archivo exe image.
3. Para empezar a correr el programa, el SO copia las instrucciones del mismo, junto con su data de la exe img, en la memoria física. También se inicializa para el stack de ejecución(heap) y otra data o estructuras que puedan ser necesarias.
4. El SO puede comenzar a correr el programa seteando el stack pointer y saltando a la primera instrucción. 

	![[Pasted image 20240427190447.png]]

## <span style="color:#c00000">Que contienen los programas</span>
- Formato de identificación binaria: meta-información describiendo el exe.
- Instrucciones en lenguaje de maquina.
- Dirección del punto de entrada del programa.
- Datos.
- Símbolos y tablas de realocacion.
- Bibliotecas compartidas.
## <span style="color:#c00000">Process Control Block(PCB)</span>
- Es una estructura de datos que sirve para que el SO lleve la contabilidad de todos los procesos que se están ejecutando en la computadora.
- Guarda el estado de los procesos ⇒ Ready, blocked, running. En definitiva, es una tabla de procesos.
	![[Pasted image 20240418211849.png]]
- Es un arreglo de procesos en donde cada elemento es un struct que guarda el pid, la memoria, los registros, el estado, etc. -> Toda la información que el SO necesita acerca de un proceso en particular(donde reside en memoria, donde esta su exe img en el disco, que usuario solicito ejecutarlo, que privilegios tiene el proceso, etc).
- JOS mantiene un arreglo en memoria con PCBs (Process Control Blocks), aunque llama environment a los procesos. De aquí en más se usarán las palabras proceso y environment como sinónimos siempre que hablemos en contexto de JOS.
	![[Pasted image 20240511151506.png]]


## <span style="color:#c00000">Contexto del proceso</span>
- Cada proceso tiene un contexto bien definido que comprende la información necesaria para describir completamente al mismo:
	- User-level context([[Address Space]] del proceso): text, data, stack y heap.
	- Register context: Program Counter(Reg de estado del procesador, SP y los registros de propósito general).
	- System-level context: La entrada en la Process Table Entry, la u area, la Process Region Entry, Region Table y Page Table(definen el mapeo de la memoria virtual vs memoria física del proceso).
		![[Pasted image 20240513065250.png]]

## <span style="color:#c00000">Permisos necesarios del Kernel</span>
- Accesos a memoria perteneciente a otro proceso.
- Antes de escribir/leer del disco.
- Antes de cambiar algún seteo del hardware del equipo.
- Antes de enviar información a otro proceso.

## <span style="color:#c00000">Partes de un proceso</span>
- <span style="color:#ffff00">Programa</span>: instrucciones que conforman el programa a ejecutar.
- <span style="color:#ffff00">Datos del usuario</span>: espacio de memoria modificable por el usuario. Ej: datos del programa y heap.
- <span style="color:#ffff00">Stack del sistema</span>: para almacenar parámetros y direcciones de retorno durante el llamado a subrutinas.
- <span style="color:#ffff00">Estructuras de datos del</span> [[Kernel]]: PCB(process control block).
- Uno o mas [[Theads]] de ejecución.
- Una sección de datos globales.
- Signals pendientes.

![[Pasted image 20240418211755.png]]

![[Pasted image 20240423090432.png]]


