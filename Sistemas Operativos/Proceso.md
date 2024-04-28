# <span style="color:#c00000">El proceso</span>

> Es la ejecución de un programa con derechos restringidos. 
> Es la abstracción para una ejecución protegida brindada por el kernel del sistema.

## <span style="color:#c00000">De Programa a Proceso</span>
> Un programa es un archivo que posee toda la información de como construir un proceso en memoria.

![[Pasted image 20240427190447.png]]

## <span style="color:#c00000">Que contienen los programas</span>
- Formato de identificación binaria: meta-información describiendo el exe.
- Instrucciones en lenguaje de maquina.
- Dirección del punto de entrada del programa.
- Datos.
- Símbolos y tablas de realocacion.
- Bibliotecas compartidas.

## <span style="color:#c00000">Conexion con el kernel</span>
- Carga las instrucciones y datos de un programa exe en memoria.
- Crea el stack y el heap.
- Transfiere el control al programa.
- Protege al SO y al programa.

## <span style="color:#c00000">Partes de un proceso</span>
- <span style="color:#ffff00">Programa</span>: instrucciones que conforman el programa a ejecutar.
- <span style="color:#ffff00">Datos del usuario</span>: espacio de memoria modificable por el usuario. Ej: datos del programa y heap.
- <span style="color:#ffff00">Stack del sistema</span>: para almacenar parámetros y direcciones de retorno durante el llamado a subrutinas.
- <span style="color:#ffff00">Estructuras de datos del</span> [[Kernel]]: PCB(process control block).
- Uno o mas [[Theads]] de ejecución.
- Una sección de datos globales.
- Signals pendientes.


## <span style="color:#c00000">Virtualizacion de memoria</span>
- Le hace creer al proceso que este tiene toda la memoria disponible para ser reservada y usada como si este estuviera siendo ejecutado solo en la computadora.
- Los procesos se dividen en 4 segmentos: instrucciones del programa, variables globales, heap y stack. Todos estos segmentos pertenecientes a un proceso se denomina address space del proceso.

	![[Pasted image 20240418203152.png]]

### <span style="color:#c00000">Proteccion de memoria</span>
- El SO debe iniciar la ejecución del programa, debe manejar las interrupciones y atender las syscalls.
- Podríamos tener varios procesos en memoria, y que quieran compartir la memoria de forma segura, por lo que el SO debe configurar el hardware de forma tal que cada proceso pueda leer y escribir solo su propia memoria. Para ello el hardware provee un mecanismo de protección de memoria.

![[Pasted image 20240418211755.png]]

![[Pasted image 20240423090432.png]]


![[Pasted image 20240418211849.png]]