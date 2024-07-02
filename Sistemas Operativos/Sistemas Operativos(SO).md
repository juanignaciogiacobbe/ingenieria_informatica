# <span style="color:#c00000">Sistemas Operativos</span> 

## <span style="color:#c00000">Que es un Sistema Operativo
</span>

> Es la capa de software mas baja, encargada de manejar los recursos de una computadora para sus usuarios y aplicaciones. 
> 
> Debe ser confiable: la <span style="color:#ffff00">proteccion</span> impide que los bugs que aparecen en algún programa corrompa a los demás programas o al mismo SO.
> <span style="color:#ffff00">Seguridad</span>: SO debe limitar a aquellos programas y usuarios que no generan confianza.
> <span style="color:#ffff00">Privacidad</span>: En un sistema multi-user, cada usuario debe ser limitado a ver ciertos datos.

	![[Pasted image 20240418195516.png]]

- En sistemas de propósito general, los usuarios interactuan con aplicaciones, las cuales se ejecutan en un ambiente provisto por el SO, y <span style="color:#ffff00">el SO hace de mediador con la capa de hardware</span>.

	![[Pasted image 20240418195730.png]]

# <span style="color:#c00000">Roles de un SO</span>
## <span style="color:#c00000">Referee</span>
- Deben ser capaces de<span style="color:#ffff00"> manejar los recursos compartidos entre aplicaciones</span> en una misma maquina.
- <span style="color:#ffff00">Aislamiento</span> de cada aplicación de las demás, de forma tal que un bug en una aplicación no corrompa a las demás aplicaciones que corren en la misma maquina(<span style="color:#ffff00">fault isolation</span>).
- Si el SO le da muy poca memoria a un programa, puede que no sólo ralentice a ese programa en particular sino también a la performance de toda la máquina.
- Debe <span style="color:#ffff00">protegerse a si mismo y a las aplicaciones</span> de virus maliciosos.
- Decide cuando y que recursos brindarles a las aplicaciones.
- <span style="color:#ffff00">Resource allocation</span>: Debe mantener todas las actividades corriendo en simultaneo, allocando recursos apropiadamente de una manera separada. Incluso, cada una de las apps que tenga corriendo pueden estar corriendo multiples tareas.
- Se debe mantener a todas las actividades separadas, dejando al mismo tiempo que cada una use la capacidad total de la máquina si las otras no están corriendo.
## <span style="color:#c00000">Ilusionista</span>
- El hardware esta necesariamente limitado por las restricciones físicas del mismo. <span style="color:#ffff00">El SO debe decidir como dividir sus recursos físicos entre todas las aplicaciones corriendo en un momento determinado.</span> La [[Virtualizacion]] nos permite darle a las aplicaciones la ilusión de tener recursos que no están presentes físicamente, ademas de que al usuario se le da la ilusión de estar corriendo varias aplicaciones al mismo tiempo.
- Una misma aplicación puede tener distinta cantidad de recursos asignados en dos tiempos distintos, aún cuando se está corriendo en el mismo hardware.
- Los SO deben brindar una <span style="color:#ffff00">abstracción</span>(enmascaramiento) <span style="color:#ffff00">del hardware físico para simplificar el diseño de las aplicaciones</span>.
- Nos dan la ilusión de "tener memoria infinita", o de tener todos los procesadores de la maquina enteramente para nosotros.
- <span style="color:#ffff00">Con esta abstracción, los SO permiten invisibilizar las reasignaciones de recursos para las distintas aplicaciones corriendo</span>. El SO es libre de cambiar los recursos asignados para cada aplicación desde el momento que se inicia hasta que se termina.
- Los SO pueden enmascarar o disimular otras limitaciones relacionadas al hardware físico, <span style="color:#ffff00">proveyendo a las aplicaciones de la ilusión de capacidades de hardware que no están realmente físicamente presentes</span>.
- <span style="color:#ffff00">Virtual Machine</span>: Cuando el SO virtualiza la computadora por completo, corriendo el SO como una aplicación por arriba de otro SO. El SO corriendo en la VM, es el <span style="color:#ffff00">guest operating system</span>, y cree que esta corriendo en una maquina real, pero esto no es mas que una ilusión provista el verdadero SO que corre por debajo. La máquina virtual huésped podría ser anfitrión o hostear aplicaciones de un sistema operativo anterior, corriendo sobre una versión más nueva del mismo sistema.
	![[Pasted image 20240509081715.png]]
## <span style="color:#c00000">Pegamento</span>
- <span style="color:#ffff00">Los SO proveen un set de servicios comunes para que se puedan compartir recursos de una forma sencilla, y que se pueda simplificar y estandarizar el diseño de las aplicaciones.</span>
- Proveen una interfaz de rutinas comunes para el usuario, para tener el mismo "look and feel". 
- Los SO además, proveen de una capa de separación entre las aplicaciones y el hardware de los dispositivos de input/output.
- Si las aplicaciones van a compartir archivos, por ejemplo, deben poder guardarse en un formato estándar, con un sistema estándar de administración de directorios. De la misma forma, la mayoría de los sistemas operativos provee de una forma estándar para que las aplicaciones se pasen mensajes y compartan memoria, facilitando la compartición.
	![[Pasted image 20240511142845.png]]

-----
## <span style="color:#c00000">Ejecución directa</span>
- El programa se corre directamente en la CPU.
	![[Pasted image 20240506132918.png]]
	- Como ventaja podemos destacar la rapidez de ejecución.
	- Pero no podemos asegurarnos de que el programa haga algo que el user no quiere que se haga.
	- Se le complica al SO el pausado de este programa y hacer que otro se ejecute.

### <span style="color:#c00000">Como limitar la ejecución directa</span>
- [[Dual-mode Operation]]

## <span style="color:#c00000">Administracion de Memoria</span>
### <span style="color:#c00000">Multiprogramacion</span> 
- Mas de un proceso esta preparado para ser ejecutado en algún momento determinado, y el SO intercala dicha ejecución según la circunstancia.
- En base a ciertas políticas del [[Scheduler]] que usen, los SO determinan que proceso es el siguiente.

#### <span style="color:#c00000">Utilizacion de la CPU</span>
- Si se asume que el 20% del tiempo de ejecución de un programa es solo cómputo y el 80% son operaciones de entrada y salida, con tener 5 procesos en memoria se estaría utilizando el 100% de la CPU.
- Siendo un poco más realista se supone que las operaciones de E/S son bloqueantes (una operación de lectura a disco tarda 10 miliseg y una instrucción registro registro tarda 1-2 nanoseg), es decir, paran el procesamiento hasta que se haya realizado la operación de E/S.
- Entonces, el cálculo es más realista si se supone que un proceso gasta una **fraccción p**, bloqueado en E/S. De esta manera, si tenemos **n procesos** esperando para hacer operaciones de entrada y salida, la probabilidad de que los **n procesos** estén haciendo E/S es $p^n$.
- Por ende la probabilidad de que se esté ejecutando algún proceso es $1-p^n$, esta fórmula es conocida como utilización de CPU.
	![[Pasted image 20240515121520.png]]
		corrección: si tenes 3 procesos corriendo un 80% del tiempo en E/S -> $1 - 0.8^3 = 0.488$ es el grado de utilización de la CPU.

#### <span style="color:#c00000">Multiple Variable Partitions</span>
- Trataba a toda la memoria no utilizada por el SO como un único gran espacio desde el cual se podían asignar regiones contiguas tanto como lo requiera un numero ilimitado de aplicaciones y programas simultáneamente.
- Cada tarea podía tener cualquier tamaño, la limitante era la memoria física de la maquina.
- Una única cola de procesos listos para correr.
- La tarea podría ser movida.
- Se elimina la fragmentacion interna -> pero se introduce la fragmentacion externa.
	![[Pasted image 20240515122005.png]]

### <span style="color:#c00000">Time Sharing</span> 
1. Se tiene un proceso corriendo por un determinado `time slice` de tiempo al cual se le da acceso a toda la memoria y recursos.
2. Al final el slice, graba su estado en algún lugar.
3. Se carga un proceso, se ejecuta por otro slice, y así sucesivamente.

- Este método es demasiado lento -> mas aun cuando la memoria comienza a crecer.
- Teniendo en cuenta que hacer un cambio de contexto a nivel registros es relativamente rápido, no tiene sentido grabar información de memoria en disco como mencionamos arriba.
- Es más fácil mantener los procesos en memoria mientras se realizan los cambios de quien se está ejecutando, de esa forma, se permite implementar de forma eficiente time sharing.
- La idea es, entonces, darle a cada proceso una pequeña parte de la memoria física. -> Se pasa a la idea del [[Address Space]].

- [[Dual-mode Operation]]
- [[Proceso]]
- [[Kernel]]
- [[Scheduler]]
- [[Sistemas Operativos/Concurrencia/Concurrencia]]
- [[File System]]
## <span style="color:#c00000">Trabajos Practicos</span> 
- [[Shell]]