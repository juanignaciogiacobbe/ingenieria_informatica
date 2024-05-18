# <span style="color:#c00000">File System</span> 
> Las computadoras tienen que ser capaces de guardar data de una forma fiable.
> Por mas que haya un problema con el dispositivo, ciertos tipos de almacenamiento nos permite mantener de una forma persistente los datos. Estos almacenamiento se llaman non-volatile storage o persistent storage.
> Es una abstracción del SO que le permite a las aplicaciones acceder a non-volatile storage.<span style="color:#ffff00"> Permite a los usuarios organizar sus datos para que persistan a través de un largo periodo de tiempo</span>(es decir, que se almacenan hasta ser borrados explicitamente).
> <span style="color:#ffff00">Es una abstracción del SO que provee datos persistentes con un nombre.</span>

## <span style="color:#c00000">Objetivos de los sistemas de almacenamiento</span>
- Fiabilidad: Necesitamos que los datos sobrevivan por mas que los dispositivos de almacenamiento se dañen.
- Mucha capacidad y menor costo.
- Alta performance: El acceso a los datos debe poder darse de una forma rápida.
- Data nombrada: Se debe poder identificar a la data de interés.
- Controlled Sharing.

## <span style="color:#c00000">Caracteristicas de un File System</span> 
- Performance: Amortizan el costo de inicializar operaciones costosas.
- Naming: Agrupan data relacionada en directorios y archivos, y dan nombres descriptivos para los humanos. Ayuda a los usuarios para organizar grandes espacios de almacenamiento. <span style="color:#ffff00">El hecho de que los datos tengan un nombre, es con la intención de que un ser humano pueda acceder a ellos por un identificador que el sistema de archivos le asocia al archivo en cuestión.</span>
- Controlled sharing: Incluyen metadata sobre quien es dueño de cada cada archivo y los permisos que tienen sobre ellos.
- Fiabilidad: Usan transacciones para actualizar atomicamente multiples bloques de almacenamiento persistente de una forma similar a como los SO usan critical sections para actualizar atomicamente distintas estructuras de datos en memoria.

## <span style="color:#c00000">Abstraccion del File System</span> 
- Nos proveen una forma de organizar y guardar data por largos periodos de tiempo.
- El File System es una abstracción del SO que nos provee de data named(puede ser accedida mediante un identificador comprensible para los humanos) y persistente(se guarda hasta que es explicitamente borrada por el usuario).

## <span style="color:#c00000">Archivos</span> 
- Un archivo es una<span style="color:#ffff00"> named collection de data</span> en un file system. Proveen una abstracción de alto nivel(nos deja referirnos a una cantidad de data arbitraria a través de un nombre simple y descriptivo).
- Por ejemplo: /home/user/main.c -> Cada archivo tiene un nombre único y un significado para referirse a los datos. Estos nombres proveen la abstracción de mas alto nivel del dispositivo de almacenamiento.
- Cada archivo tiene dos partes:
	- Metadata: contiene información acerca del archivo(tamaño, fecha de modificación, propietario y seguridad).
	- Datos almacenados -> guardados en una data region.

## <span style="color:#c00000">Directorios</span> 
- Proveen los nombres para los archivos, es una lista de nombres human-friendly y un mapeo a un archivo o directorio.
- Cuando los links hacia un archivo llegan a 0, se borra el archivo.
	![[Pasted image 20240516072448.png]]

- <span style="color:#ffff00">Path</span>: El string que identifica a un archivo o directorio. La jerarquía de directorios forma un árbol.
	![[Pasted image 20240506130139.png]]

- <span style="color:#ffff00">Volume</span>: Es una colección de recursos de almacenamiento físico que forma un dispositivo de almacenamiento lógico. Es una abstracción que corresponde a un logical disk. 
	![[Pasted image 20240506130653.png]]
	- Una computadora puede usar multiples file systems guardados en multiples volúmenes montandolos en una misma jerarquía lógica simple.
	![[Pasted image 20240506130845.png]]


## <span style="color:#c00000">Virtual File System(VFS)</span> 
- Es el subsistema del [[Kernel]] que implementa las interfaces que tiene que ver con los archivos y el FS provistos a los programas corriendo en modo usuario.
- Todos los FS deben basarse en VFS para coexistir e inter-operar, y así poder utilizar las [[System Calls]] de UNIX para leer y escribir en diferentes FS, y diferente medios.
	![[Pasted image 20240516070526.png]]

- VFS es el pegamento que habilita a las system calls como por ejemplo `open()`, `read()` y `write()` a funcionar sin que estas necesiten tener en cuenta el hardware subyacente.
- Cualquier cosa que vaya a ser persistente va a pasar por el VFS -> actúa como proxy, para que el kernel pueda hablar con todos.

### <span style="color:#c00000">Capa de abstracción de un FS</span> 
- Es una interfaz genérica que para cualquier tipo de FS el kernel implementa con el sistema de archivos de bajo nivel -> habilita a Linux a soportar FS diferentes, incluso si estos difieren en características y comportamiento.
- VFS provee un modelo común de archivos que puede representar cualquier característica y comportamiento general de cualquier FS.
	![[Pasted image 20240516071036.png]]
- Esta capa de abstracción trabaja mediante la definición de interfaces conceptualmente básicas y de estructuras que cualquier FS soporta, por lo que cada FS adapta su forma de trabajo a lo que espera el VFS.
- El resultado es una capa de abstracción general que le permite al kernel manejar muchos tipos de sistemas de archivos de forma fácil y limpia.

## <span style="color:#c00000">Estructuras</span> 
- <span style="color:#ffff00">SuperBloque</span>: Representa a todo un FS.
- <span style="color:#ffff00">Inodo</span>: Representa a un determinado archivo dentro de un FS(físico en disco).
- <span style="color:#ffff00">Dentry</span>: Representa una entrada de directorio, que es un componente simple de un path.
- <span style="color:#ffff00">File</span>: Representa un archivo asociado a un determinado proceso(el proceso abrió un archivo).
	![[Pasted image 20240516071413.png]]
- Un directorio es tratado como un archivo normal, no hay un objeto especifico para directorio. En UNIX, los directorios son archivos normales que listan los archivos contenidos en ellos. Guardan la relación nombre del archivo-inodo(indica que archivos contiene el directorio).
- Abrir un directorio seria como ver un archivo binario, que tiene 4 bytes para ver el inodo, la longitud del archivo, la longitud del nombre, el tipo de archivo y el nombre.
- Todos los directorios tienen un . y .. para representar al actual y al padre.

## <span style="color:#c00000">Inodos</span>
- Es una de las estructuras mas importantes en el disco dentro de un FS.
- inode -> abreviación de index node.
- Describe la estructura que contiene la metadata de un archivo dado:
	- Su tipo(archivo regular, directorio, etc).
	- Tamaño.
	- El numero de bloques que ocupa en disco.
	- Información de protección(quien es el owner del archivo, quien puede acceder, etc).
	- Time information(Fechas de creación, modificación, accesos).
	- Información sobre donde residen en discos sus data blocks.
- Cada inodo es referido por un numero(inumber), que seria el equivalente al nombre en bajo nivel del archivo. Dado un inumber, deberías ser capaz de calcular en que parte del disco esta localizado el inodo.
	![[Pasted image 20240517094259.png]]

### <span style="color:#c00000">Multi-Level Index</span>
- Tiene el fin de soportar archivos grandes(no nos sirve un sistema de punteros directos a los bloques, porque podríamos tener un archivo que ocupa muchos bloques, y tendríamos muchos punteros).
- En cambio, se usa un sistema de punteros indirectos. En vez de apuntar a un bloque que contiene user data, se apunta a otro bloque que contiene mas punteros, y cada uno de ellos apunta a data de usuario.

## <span style="color:#c00000">System Calls sobre archivos</span> 
![[Pasted image 20240516072845.png]]
![[Pasted image 20240516072903.png]]

## <span style="color:#c00000">System Calls sobre Directorios</span> 
![[Pasted image 20240516073012.png]]

Con `dirent.h`:
![[Pasted image 20240516073044.png]]

## <span style="color:#c00000">System Calls sobre Metadatos</span> 
![[Pasted image 20240516073124.png]]