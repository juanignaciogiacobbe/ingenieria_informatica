# <span style="color:#c00000">Threads</span> 

> Un thread es una unidad de ejecución que vive dentro de un proceso, y representa una task scheduleable. 
> Podemos representar cada tarea concurrente como un thread.
> Nos permite definir un set de tareas que corren concurrentemente mientras el código para cada task es secuencial. Cada thread se comporta como si tuviera si propio procesador dedicado(esta abstracción nos permite crear los threads que queramos sin preocuparnos por la cantidad de procesadores físicos que tengamos).

- El sistema operativo cumple el rol de Ilusionista, ya que nos hace creer que tenemos un numero ilimitado de procesadores.
- El SO puede correr, suspender, o resumir la ejecución de un thread en un tiempo determinado.
- Un proceso con varios threads es un <span style="color:#ffff00">proceso multithread</span>. Cada thread sigue una secuencia de pasos.
- Los threads que viven dentro de un proceso <span style="color:#ffff00">se ejecutan de forma concurrente</span> y comparten contexto entre si.
- Un thread <span style="color:#ffff00">es similar a un proceso pero con una menor carga de contexto propio</span>.
- Comparten recursos de un mismo proceso, entre ellos el espacio de memoria. Cada uno mantiene su propia información de estado(stack, PC, registros).

![[Pasted image 20240427173558.png]]

![[Pasted image 20240423091057.png]]

## <span style="color:#c00000">Razones para usar threads</span> 
- Estructura del programa: expresando lógicamente a las tareas concurrentes.
- Cambiando de jobs para correr en el background.
- Explotación de multiples procesadores.
- Managing de dispositivos de I/O.

## <span style="color:#c00000">Corriendo, suspendiendo y resumiendo threads</span> 
- Para darnos la ilusión de tener un numero infinito de procesadores, el SO ejecuta las instrucciones de cada thread de forma tal que cada uno progresa en sus tareas.
- Para mapear un set de threads arbitrario para un set reducido de procesadores, los SO utilizan un thread [[Scheduler]] que permite switchear entre los threads que están corriendo, y aquellos que están listos para correr.
- Cada thread corre en un procesador virtual dedicado con una velocidad impredecible y variable. Parece que cada instrucción se ejecuta inmediatamente después de su predecesora. Esto se hace para que los programas con multiples threads no asuman comportamientos del scheduler.

	![[Pasted image 20240427175056.png]]
	![[Pasted image 20240427175227.png]]


## <span style="color:#c00000">Thread Control Block(TCB)</span> 
- Es una estructura de datos que permite representar el estado de un thread. Cada vez que se crea un thread, el SO crea un TCB.
- TCB contiene informacion del estado de la computacion siendo corrida por el thread, y metadata sobre el thread que es utilizado para controlar ese thread.


## <span style="color:#c00000">Ciclo de vida de un thread</span> 
![[Pasted image 20240427175959.png]]