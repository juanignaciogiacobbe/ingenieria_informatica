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
- <span style="color:#ffff00">One thread per process</span>: Un proceso con una única secuencia de instrucciones ejecutándose de inicio a fin. Es equivalente a un bloque de instrucciones delimitado por llaves.
- <span style="color:#ffff00">Many thread per process</span>: Un programa es visto como threads ejecutándose dentro de un proceso con derechos restringidos. En un dado $t_i,$ algunos threads pueden estar corriendo y otros estar suspendidos. Cuando se detecta, por ejemplo, una operación de I/O por alguna interrupción, el kernel desaloja a algunos de los threads, atiende la interrupción y al terminar vuelve a correr dichos threads.
- <span style="color:#ffff00">Many single-threaded processes</span>: Limitación de algunos sistemas operativos que permitían varios procesos, pero cada uno con un único thread, lo que implica que puede haber varios threads ejecutándose en kernel mode.
- <span style="color:#ffff00">Many kernel threads</span>: Para aprovechar recursos, también el kernel puede ejecutar varios threads en kernel mode.

## <span style="color:#c00000">Abstracción de los Threads</span>
- thread_id
- Conjunto de valores de los registros.
- Un stack propio.
- Una política y prioridad de ejecución.
- Un propio errno.
- Datos específicos del thread.

## <span style="color:#c00000">Thread Scheduler</span>
- Para darnos la ilusión de tener un numero infinito de procesadores, el SO ejecuta las instrucciones de cada thread de forma tal que cada uno progresa en sus tareas.
- Para mapear un set de threads arbitrario para un set reducido de procesadores, los SO utilizan un thread [[Scheduler]] que permite switchear entre los threads que están corriendo, y aquellos que están listos para correr.
- Es necesario tener un sched de threads, ya que el SO podría estar trabajando con un único procesador.
- El cambio entre threads es transparente, es decir que el programador debe preocuparse de la secuencia de instrucciones y no cuando un thread esta suspendido o no -> los threads proveen un modelo de ejecución en el cual cada uno corre en un procesador virtual dedicado con una velocidad variable e impredecible. Esto se hace para que los programas con multiples threads no asuman comportamientos del scheduler


## <span style="color:#c00000">API de Threads</span>
- Se utiliza la biblioteca `pthread.h`, donde la p se corresponde a POSIX threads.

### <span style="color:#c00000">Creacion de un Thread</span>
![[Pasted image 20240516094450.png]]
- thread es un puntero a la estructura del tipo `pthread_t`.
- attr se utiliza para especificar los ciertos atributos que el thread debería tener.
- start_routine es un puntero a una función.
- arg es un puntero a void que debe apuntar a los argumentos de la función.

### <span style="color:#c00000">Terminación de un Thread</span>
![[Pasted image 20240516094635.png]]
- thread es el thread por el que hay que esperar y es de tipo `pthread_t`.
- value_ptr es el puntero al valor esperado de retorno.

## <span style="color:#c00000">Razones para usar threads</span> 
- Estructura del programa: expresando lógicamente a las tareas concurrentes.
- Cambiando de jobs para correr en el background.
- Explotación de multiples procesadores.
- Managing de dispositivos de I/O.

## <span style="color:#c00000">Estructura y ciclo de vida de un Thread</span>
- Un thread es una representación de una secuencia de ejecución de un conjunto de instrucciones -> para que la ilusión sea creíble, el SO debe guardar y cargar el estado de cada thread. Como cualquier thread puede correr en el procesador o en el [[kernel]], se deben soportar estados compartidos, que no deberían cambiar entre modos.

## <span style="color:#c00000">Thread Control Block(TCB)</span> 
- Es una estructura de datos que permite representar el estado de un thread. Cada vez que se crea un thread, el SO crea una entrada en esta estructura.
- TCB contiene información del estado de la computación siendo corrida por el thread, y metadata sobre el thread que es utilizado para controlar ese thread.
- Para poder crear multiples threads, pararlos y re-arrancarlos, el SO debe poder almacenar en la TCB el estado actual del bloque de ejecución(puntero al stack del thread, y una copia de sus registros en el procesador).
- Por cada thread se guarda su ID, su prioridad de scheduling y su status.

	![[Pasted image 20240516095210.png]]
- También, se debe guardar cierta información que es compartida por varios threads:
	- Código.
	- Variables globales.
	- Variables del heap.
- Los threads por defecto:
	- Comparten memoria, los fds, el contexto del [[File System]], y el manejo de señales.
- Los procesos por defecto no hacen NADA de eso.
## <span style="color:#c00000">Ciclo de vida de un thread</span> 

![[Pasted image 20240427175959.png]]
![[Pasted image 20240516095522.png]]

## <span style="color:#c00000">Sincronizacion de Threads</span> 
- La programación multithread extiende el modelo secuencial de programación de un hilo único de ejecución:
	- Un programa puede estar compuesto por un conjunto de threads independientes que operan sobre un conjunto de datos que están completamente separados entre si y son independientes.
	- Un programa puede estar compuesto por un conjunto de threads que trabajan en forma cooperativa sobre un set de memoria y datos que son compartidos.
- Al utilizar threads cooperativos, la forma de pensar secuencial no sirve -> el orden de ejecución de los hilos puede no ser siempre la misma -> va a influir en los accesos a memoria de recursos compartidos.
	- La ejecución de los threads es NO deterministica -> diferentes corridas de un mismo programa multithread producen distintos resultados.
	- Los compiladores y el procesador físico pueden reordenar las instrucciones.
- Para crear programas con multithreads es necesario tener en cuenta los posibles [[Problemas de la Concurrencia]] que pueden aparecernos.

	![[Pasted image 20240427175056.png]]
	![[Pasted image 20240427175227.png]]


