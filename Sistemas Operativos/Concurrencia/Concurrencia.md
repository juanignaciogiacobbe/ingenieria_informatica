# <span style="color:#c00000">Concurrencia</span> 
> La idea es escribir un programa concurrente(que tenga varias actividades en simultaneo) como un set de streams de ejecución secuenciales, llamados [[Theads]], que interactuan entre si y comparten resultados.

## <span style="color:#c00000">Concurrencia VS Paralelismo</span> 

- En <span style="color:#ffff00">programacion concurrente</span>, diferentes partes de un programa se ejecutan independientemente. Hay overlapping(los procesos se pisan) entre tiempos de ejecución de procesos.
- En <span style="color:#ffff00">programacion paralela</span>, diferentes partes de un programa se ejecutan exactamente al mismo tiempo, mientras que a la vez es tener todas las operaciones activas, pero intercambiando su ejecución por períodos de tiempo.

	![[Pasted image 20240423081103.png]]

- Existen programas cuya performance puede ser mejorada utilizando concurrencia. Generalmente son aquellos que realizan alguna operación de I/O.
	- Leer y escribir datos de memoria.
	- Comunicarse con dispositivos de hardware.
	- Servidores que atienden solicitudes de distintos clientes.

### <span style="color:#c00000">Definiciones importantes</span> 
- <span style="color:#ffff00">Programa concurrente</span>: un conjunto finito de procesos secuenciales. Se escribe como una secuencia de streams de ejecución o threads que interactuan y comparten datos de una manera muy precisa.
	![[Pasted image 20240515124236.png]]
- El [[Proceso]] esta compuesto por un conjunto finito de instrucciones atómicas.
- Al ejecutar una secuencia de instrucciones atómicas que se obtiene al intercalar arbitrariamente las instrucciones atómicas de los procesos que lo componen se da la <span style="color:#ffff00">ejecucion del programa concurrente</span>. 
	- Este intercalamiento es arbitrario(lo decide el SO a través del [[Scheduler]]).
	- Cada vez que el SO cambia el proceso en ejecución, ocurre un context-switch.


![[Pasted image 20240423082221.png]]

- Hay que tener en cuenta todos los <span style="color:#ffff00">intercalamientos</span> posibles de las instrucciones atómicas.
- Hay necesidad de <span style="color:#ffff00">sincronizar</span>(coordinación temporal) y <span style="color:#ffff00">comunicar</span>(datos compartidos) procesos diferentes.

## <span style="color:#c00000">Concurrencia en Rust</span> 
- El mecanismo de Ownership y el sistema de tipos de Rust previene los problemas de la Concurrencia en tiempo de compilación.
- Los errores se manifiestan en tiempo de compilación -> fearless concurrency.
- Para mapear [[Theads]] existen dos modelos: green threads y los threads del SO.
- " Do not communicate by sharing memory; instead, share memory by communicating".