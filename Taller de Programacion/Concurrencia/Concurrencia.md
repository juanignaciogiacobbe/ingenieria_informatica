# <span style="color:#c00000">Concurrencia</span> 

## <span style="color:#c00000">Concurrencia VS Paralelismo</span> 

- En <span style="color:#ffff00">programacion concurrente</span>, diferentes partes de un programa se ejecutan independientemente. Hay overlapping(los procesos se pisan) entre tiempos de ejecucion de procesos.
- En <span style="color:#ffff00">programacion paralela</span>, diferentes partes de un programa se ejecutan exactamente al mismo tiempo.

	![[Pasted image 20240423081103.png]]

- Existen programas cuya performance puede ser mejorada utilizando concurrencia. Generalmente son aquellos que realizan alguna operacion de I/O.
	- Leer y escribir datos de memoria.
	- Comunicarse con disps de hardware.
	- Servidores que atienden solicitudes de distintos clientes.


### <span style="color:#c00000">Definiciones importantes</span> 
- <span style="color:#ffff00">Programa concurrente</span>: un conjunto finito de procesos secuenciales.
- El [[Proceso]] esta compuesto por un conjunto finito de instrucciones atomicas.
- Al ejecutar una secuencia de instrucciones atomicas que se obtiene al intercalar arbitrariamente las instrucciones atomicas de los procesos que lo componen se da la <span style="color:#ffff00">ejecucion del programa concurrente</span>. 
	- Este intercalamiento es arbitrario(lo decide el [[Sistemas Operativos(SO)]] a traves del [[Scheduling]]).
	- Cada vez que el SO cambia el proceso en ejecucion, ocurre un context-switch.


![[Pasted image 20240423082221.png]]

Hay que tener en cuenta todos los intercalamientos posibles de las instrucciones atomicas.