# <span style="color:#c00000">Concurrencia</span> 
> La idea es escribir un programa concurrente(que tenga varias actividades en simultaneo) como un set de streams de ejecución secuenciales, llamados [[Theads]], que interactuan entre si y comparten resultados.

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
	- Este intercalamiento es arbitrario(lo decide el [[Sistemas Operativos(SO)]] a traves del [[Scheduler]]).
	- Cada vez que el SO cambia el proceso en ejecucion, ocurre un context-switch.


![[Pasted image 20240423082221.png]]

- Hay que tener en cuenta todos los <span style="color:#ffff00">intercalamientos</span> posibles de las instrucciones atomicas.
- Hay necesidad de <span style="color:#ffff00">sincronizar</span>(coordinacion temporal) y <span style="color:#ffff00">comunicar</span>(datos compartidos) procesos diferentes.

## <span style="color:#c00000">Problemas de la Concurrencia</span> 
- <span style="color:#ffff00">Condiciones de carrera</span>: Los hilos de ejecucion del programa acceden a datos o recursos de forma inconsistente. La salida del programa depende del orden de ejecucion de las instrucciones atomicas de los procesos, convirtiendose en una <span style="color:#ffff00">salida no deterministica</span>.
- <span style="color:#ffff00">Deadlocks</span>: Donde dos hilos de ejecucion estan esperando el uno por el otro para avanzar, requiriendo de un recurso que el otro tiene, previniendo que ambos avancen. No hay progreso productivo.

## <span style="color:#c00000">Concurrencia en Rust</span> 
- El mecanismo de Ownership y el sistema de tipos de Rust previene los problemas de la Concurrencia en tiempo de compilacion.
- Los errores se manifiestan en tiempo de compilacion -> fearless concurrency.
- Para mapear [[Theads]] existen dos modelos: green threads y los threads del SO.
- " Do not communicate by sharing memory; instead, share memory by communicating".