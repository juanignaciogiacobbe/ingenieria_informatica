# <span style="color:#c00000">Address Space</span> (AS)
- Es la abstracción "easy-to-use" de la memoria física que nos provee el SO. Es la vista que tiene un programa en ejecución de la memoria en el sistema.
- Contiene todo el memory state de el programa en ejecución(code, stack y heap). 
- Al describir el AS, lo que se está describiendo es la abstracción que el SO le proporciona al programa en ejecución sobre la memoria de la computadora.

	![[Pasted image 20240503181002 1.png]]
	- El tamaño de code es estático(no va a necesitar mas memoria de la que tiene al iniciarse), por lo que lo podemos poner al inicio del address space por ejemplo.
	- El heap y el stack crecen en direcciones opuestas.
	- El programa no necesariamente esta en la dirección 0 de la memoria física(esta cargado en alguna dirección arbitraria).

> El SO esta virtualizando la memoria, debido a que el programa que se esta corriendo cree que esta cargado en una posición especifica de memoria(por ejemplo, en la posición 0), y que tiene toda la memoria para el(cuando obviamente no es así).
> Al aislar la memoria de los procesos, el SO se asegura que los programas en ejecución no afecten la operación del mismo SO.


## <span style="color:#c00000">Mecanismos de Address Translation</span> 
- Hardware-based address translation. El hardware nos da el mecanismo de bajo nivel para virtualizar eficientemente.
- El hardware transforma cada acceso de memoria, cambiando el virtual address dado por la instrucción a una physical address donde la información deseada esta guardada.
- Un address translation se realiza por hardware para redireccionar app memory references hacia su locación real en memoria.
- El SO debe meterse para setear el hardware de manera tal de hacer las traducciones correctamente. Esto significa que va a encargarse de trackear las locaciones libres y no libres, y va a intervenir para mantener control sobre como se esta usando la memoria.
- Con esto se logra que los programas se crean que tienen su propia memoria dedicada.
- Se busca que los procesos no sepan sus locaciones en memoria física, y que tampoco sepan del proceso de relocalizacion.

	![[Pasted image 20240505171901.png]]

## <span style="color:#c00000">Memory Management Unit(MMU)</span>
- Es la parte del procesador que nos ayuda en el address translation.
- Se traduce una virtual address en una dirección física a través del MMU.

	![[Pasted image 20240506134540.png]]

## <span style="color:#c00000">Dynamic(hardware-based) Relocation</span> 
- Se tienen dos registros en la CPU: base y bound(limit). Estos registros nos van a permitir colocar el address space en el lugar que queramos dentro de la memoria física, y asegurándonos que cada proceso solo pueda acceder a su AS.
- Podemos mover AS luego de que el proceso comience a ejecutarse.
- La traducción va a ocurrir en tiempos de ejecución(de ahí viene el dynamic), y se va a hacer de la siguiente manera:
	![[Pasted image 20240505172417.png]]
- Cada referencia creada por el proceso va a ser una virtual address.
- Base sirve para realizar las traducciones.
- Bound va a servirnos para asegurarnos que la virtual address es valida(no se sale del AS del proceso). *De acá sale el famoso error: index out of bounds*.
- Ambos registros nos van a permitir virtualizar la memoria de una manera simple y eficiente.
	![[Pasted image 20240505172857.png]]
- El SO debe encargarse de:
	- Buscarle espacio en la memoria física al AS de un proceso recién creado.
	- Debe reclamar la memoria de un proceso terminado.
	- Debe tomar acción al haber un context switch. Debería guardar los valores de base y bound de aquellos procesos que pasan a estar en estado `ready`, y debe reiniciar los valores de los mismos para acceder al AS del nuevo proceso en ejecución. Este acceso es privilegiado.

### <span style="color:#c00000">Issue con Dynamic Relocation</span>
- Puede pasar que se reserve un espacio fijo para un proceso, y que por ejemplo el mismo tenga espacios desperdiciados(ej: no usa el heap, y su stack no se llena). Esto se conoce como internal fragmentation.
- El problema de internal fragmentation es que se va a reservar memoria física por mas que no se use al 100%.

## <span style="color:#c00000">Dynamic Relocation con Tabla de Segmentos</span>
- En la técnica anterior, el problema es que solo hay un par base y bound -> se puede mejorar teniendo un registro de pares `[base, bound]` por cada proceso.
	![[Pasted image 20240513072032.png]]
	- Cada entrada en el arreglo controla una porción del virtual address space. La memoria física de cada segmento es almacenada continuamente, pero distintos segmentos pueden estar ubicados en distintas partes de la memoria física.
	- El número de segmento es el indicador de la tabla para ubicar el inicio del segmento en la memoria física.

- El problema con la relocation segmentada es que la memoria física se va a llenar espacios libres, y se va a generar una mayor dificultad para allocar nuevos segmentos o hacer crecer los ya existentes. Esto se llama external fragmentation.


## <span style="color:#c00000">Memoria paginada</span> 
- La memoria es reservada en pedazos de tamaño fijo llamados page frames.
- El address translation es similar a como se trabaja con la segmentación. En vez de tener una pagina de segmentos cuyas entradas tienen punteros a esos segmentos, hay una tabla de paginas por cada proceso cuyas entradas contienen punteros a las page frames.
- La page table va a trackear por cada proceso las address translations de cada virtual page del AS -> nos permite saber en que parte de la memoria física vive cada pagina.
- Teniendo en cuenta que los page frames tienen un tamaño fijo, y son potencia de 2, las entradas en la page table sólo tienen que proveer los bits superiores de la dirección de la page frame. De esta forma, van a ser más compactos. No es necesario tener un límite, la página entera se reserva como una unidad.

### <span style="color:#c00000">Ventajas</span> 
- La memoria se separa en piezas pequeñas de igual tamaño, llamadas pages.
- Una app puede ocupar multiples paginas, que pueden no ser contiguas.
- Cada programa de aplicación tiene su propia vista de la memoria, llamada memoria lógica.
- Una page table almacena donde están localizadas en memoria física las diferentes paginas de un programa.
- Las paginas no utilizadas se pueden mover al disco para hacer espacio en memoria para otras paginas -> vuelven a ser llamadas cuando se necesitan.
- Suplementar memoria física con un segundo almacenamiento se conoce como virtual memory.
- Cuando la memoria está baja, el cambio de memoria a disco y viceversa puede llegar a empeorar la performance.

## <span style="color:#c00000">Address Translation con Page Table</span> 
- Una dirección virtual esta compuesta por el numero de la pagina virtual, y el offset dentro de esa pagina.
![[Pasted image 20240516124305.png]]
- El numero de la pagina virtual es el indice en la page table para obtener el page frame en la memoria física. La dirección física esta compuesta por The Physical Frame Page que se obtiene de la page table, concatenando con el offset de la pagina que se obtiene de la virtual address.
- El SO maneja los accesos a memoria.
- La paginacion vuelve a tener el mismo problema que la segmentación, debido a que se vuelve muy complicado saber que espacio de la memoria esta vacío.

## <span style="color:#c00000">Translation Multilevel</span> 
- Se usa para implementar un mecanismo eficiente de paginacion -> se suelen utilizar arboles y hashes para implementarlo, no arreglos. 
- Los sistemas que usan técnicas de address translation basados en arboles soportan:
	- Protección de memoria de grano fino.
	- Memoria compartida.
	- Ubicación de memoria flexible.
	- Reserva eficiente de memoria.
	- Un sistema de búsqueda de espacio de direcciones eficiente.
- Todos los sistemas multilevel usan paginacion en el nivel mas bajo del árbol, pero la principal diferencia entre ellos es como se llega a la page table a nivel de las hojas del árbol.

### <span style="color:#c00000">Segmentación Paginada</span> 
- Dos niveles de un arbol.
- La memoria esta segmentada, pero cada entrada en la tabla de segmentos apunta a una tabla de paginas, que a su vez apunta a la memoria correspondiente a ese segmento.
- La virtual address se compone del numero de segmento, un numero de pagina virtual en ese segmento, y un offset.
	![[Pasted image 20240516125513.png]]

### <span style="color:#c00000">Address Translation con 3 Niveles de Page Tables</span> 
![[Pasted image 20240516125757.png]]

### <span style="color:#c00000">Address Translation con Tabla de Hash por Software</span> 
![[Pasted image 20240516125919.png]]