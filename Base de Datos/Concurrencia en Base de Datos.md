# <span style="color:#c00000">Concurrencia en Base de Datos</span> 
- En las bases de datos reales multiples usuarios realizan operaciones de consulta y/o actualización simultáneamente.
- Nos gustaría aprovechar la capacidad de procesamiento lo mejor posible al atender a los usuarios.
- Es la posibilidad de ejecutar multiples transacciones en forma simultanea.
- El problema que se genera es la gestión de recursos compartidos. Al nivel de las [[DataBase Management System(DBMS)]], los recursos compartidos son los datos, a los cuales distintas transacciones querrán acceder en forma simultanea.

## <span style="color:#c00000">Sistemas monoprocesador</span> 
- Permiten hacer multitasking. Varios [[Theads]] o [[Proceso]] pueden estar corriendo simultáneamente.
- No es deseable que la ejecución de una transacción lenta demore a otras de ejecución rápida.
- Mientras una [[Transaccion]] espera que el SO escriba una pagina en disco, otra transacción podría realizar una operación en memoria.

## <span style="color:#c00000">Sistemas multiprocesador y sistemas distribuidos</span> 
- Disponen de varias unidades de procesamiento que funcionan en forma simultanea.
- Suelen replicar la DB, disponiendo de varias copias de algunas tablas(fragmentos de tabla), en distintas unidades de procesamiento.
- Aquí también vamos a querer aprovechar toda la capacidad de computo:
	- Si dos transacciones utilizan sets de datos distintos, deberían poder ejecutarse concurrentemente en distintos procesadores.

## <span style="color:#c00000">Modelo de procesamiento concurrente: Concurrencia solapada</span> 
- Hipótesis:
	- Disponemos de un único procesador que puede ejecutar multiples transacciones simultáneamente.
	- Cada transacción esta formada por una secuencia de instrucciones atómicas, que el procesador ejecuta de a una a la vez.
	- En cualquier momento el [[Scheduler]] puede suspender la ejecución de una transacción, e iniciar o retomar la ejecución de otra.

	![[Pasted image 20240608164455.png]]

- Si tuviéramos multiples unidades de procesamiento, el modelo a utilizar seria el de procesamiento paralelo.
- Nuestra DB esta formada por items, y cada item puede representar:
	- El valor de un atributo en una fila determinada de una tabla.
	- Una fila de una tabla.
	- Un bloque del disco.
	- Una tabla.
- Las instrucciones atómicas básicas de una transacción sobre la DB serán:
	- leer_item(X): lee el valor del item X, cargándolo en una variable en memoria.
	- escribir_item(X): ordena escribir el valor que esta en memoria del item X en la DB.
	- El tamaño de item escogido se conoce como granularidad, y afecta sustancialmente al control de concurrencia.


## <span style="color:#c00000">Anomalías</span>

### <span style="color:#c00000">Problema de la lectura sucia</span>
- Cuando una transacción $T_2$ lee un item que ha sido modificado por otra transacción $T_1$.
- Si luego $T_1$ se deshace, la lectura que hizo $T_2$ no es valida en el sentido de que la ejecución resultante puede no ser equivalente a una ejecución serial de las transacciones.
- Es un conflicto de tipo WR: $$W_{T_1}(X)...R_{T_2}(X)...(a_{T_1} \ o \ c_{T_1})$$

	![[Pasted image 20240609181607.png]]

### <span style="color:#c00000">Lost update</span> 
- Cuando una transacción modifica un item que fue leído anteriormente por una primera transacción que aun no terminó.
- Si la primera transacción luego modifica y escribe el item que leyó, el valor escrito por la segunda se perderá.

	![[Pasted image 20240609182523.png]]

### <span style="color:#c00000">Escritura sucia</span> 
- Cuando una transacción $T_2$ escribe un item que ya había sido escrito por otra transacción $T_1$ que luego se deshace.
- El problema se dará si los mecanismos de recuperación vuelven al item a su valor inicial, deshaciendo la modificación realizada por $T_2$.

### <span style="color:#c00000">Problema del Fantasma</span> 
- Cuando una transacción $T_1$ observa un conjunto de items que cumplen determinada condición, y luego dicho conjunto cambia porque algunos de sus items son modificados/creados/eliminados por otra transacción $T_2$.
- Si esta modificación se hace mientras $T_1$ aun se esta ejecutando, $T_1$ podría encontrarse con que el conjunto de items que cumplen la condición cambio.
## <span style="color:#c00000">Equivalencia de solapamientos</span> 
- De resultados: Dado un estado inicial particular, ambos ordenes de ejecución dejan a la DB en el mismo estado.
- De conflictos: Cuando ambos ordenes de ejecución poseen los mismos conflictos entre instrucciones.
## <span style="color:#c00000">Conflictos</span> 
- Tenemos un conflicto cuando dos transacciones distintas ejecutan instrucciones sobre un mismo item X, y al menos una de las dos instrucciones es una escritura.
- Dado un orden de ejecución, un conflicto es un par de instrucciones ($I_1, I_2$) ejecutadas por dos transacciones distintas $T_i$ y $T_j$, tales que $I_2$ se encuentra mas tarde que $I_1$ en el orden, y que responde a alguno de los siguientes esquemas:
	- ($R_{T_i}(X), W_{T_j}(X)$): Una transacción escribe un item que otra leyó.
	- ($W_{T_i}(X), R_{T_j}(X)$): Una transacción lee un item que otra escribió.
	- ($W_{T_i}(X), W_{T_j}(X)$): Dos transacciones escriben un mismo item.
- Todo par de instrucciones consecutivas($I_1, I_2$) de un solapamiento que no constituye un conflicto puede ser invertido en su ejecución(es decir, reemplazado por el par ($I_2, I_1$)), obteniendo un solapamiento equivalente por conflictos al inicial.

## <span style="color:#c00000">Grafo de precedencias</span> 
- La serializabilidad por conflictos puede ser evaluada a través del grafo de precedencias.
- Dado un conjunto de transacciones $T_i$ que acceden a determinados items $X_i$, el grafo de precedencias es un grafo dirigido que se construye de la siguiente forma:
	- Se crea un nodo por cada transacción $T_i$.
	- Se agrega un arco entre los nodos $T_i \ y \ T_j \ (con \ i \neq j)$ si y solo si existe algún conflicto de la forma ($R_{T_i}(X), W_{T_j}(X)$), ($W_{T_i}(X), R_{T_j}(X)$) o ($W_{T_i}(X), W_{T_j}(X)$)).
- Cada arco indica una precedencia entre $T_i \ y \ T_j$, e indica que para que el resultado sea equivalente por conflictos a una ejecución serial, entonces en dicha ejecución serial $T_i$ debe $T_j$ preceder a (ejecutarse antes que) $T_j$.
- Agrego un arco dirigido entre los nodos $T_i \ y \ T_j$ si existe algún conflicto de la forma vista antes.

	![[Pasted image 20240610134654.png]]

- Un orden de ejecución es serializable por conflictos si y solo si su grafo de precedencias no tiene ciclos.
- Si un orden de ejecución es serializable por conflictos, el orden de ejecución serial equivalente puede ser calculado a partir del grafo de precedencias, utilizando el algoritmo de ordenamiento topológico.
	- Dado un grafo dirigido aciclico, un orden topologico es un ordenamiento de los nodos del grafo tal que para todo arco ($x, y$), nodo $x$ precede al nodo $y$.
	- Es sencillo encontrar uno eliminando los nodos que no poseen predecesores en forma recursiva y de a uno a la vez, hasta que no quede ninguno. El orden en que los nodos fueron eliminados constituirá un orden topologico del grafo.


## <span style="color:#c00000">Control de Concurrencia</span> 
- Enfoque pesimista: Busca garantizar que no se produzcan conflictos:
	- Control de concurrencia basado en locks.
- Enfoque optimista: Consiste en "dejar hacer" a las transacciones, y deshacer(rollback) una de ellas si en fase de validación se descubre un conflicto. Conveniente cuando la probabilidad de conflicto es baja.
	- Control de concurrencia basado en timestamps.
	- Snapshot isolation.
	- Control de concurrencia multiversion.


### <span style="color:#c00000">Control de concurrencia basado en locks</span> 
- Se utilizan locks para bloquear a los recursos(items) y no permitir que mas de una transacción los use en forma simultanea.
- Los locks son insertados por el DBMS como instrucciones especiales en medio de la transacción.
- Una vez insertados, las transacciones compiten entre ellas por su ejecución.
- Veremos que es posible(aunque no trivial) garantizar la serializabilidad utilizando locks.
- Un lock debe disponer de dos primitivas de uso, que permiten tomar y liberar el recurso X asociado al mismo:
	- Acquire(X) o Lock(X) (L(X).
	- Release(X) o Unlock(X) (U(X)).
- Cuando una transacción tiene un lock sobre un item X, ninguna otra transacción puede adquirir un lock sobre el mismo hasta tanto la primera no lo libere.
- L(X) requiere escribir y leer una variable, por lo tanto no puede estar solapada con una ejecución similar en otra transacción.
- El empleo de locks por si solos no basta. Una transacción podría adquirir un lock sobre un item para leerlo y modificarlo. Si en el intervalo otra transacción lo lee y escribe(aun tomando un lock), podría producirse la anomalía de la lectura no repetible.
### <span style="color:#c00000">Protocolo de locks de dos fases 2PL</span>
- Es el protocolo mas comúnmente utilizado para la adquisición y liberación de locks es el protocolo de locks de dos fases(2PL, two-phase-lock), el cual se rige por la siguiente regla: 
$$Una \ transaccion \ no \ puede\ adquirir\ un\ lock\ luego \ de\ haber\ liberado\ un \ lock \ que \ habia \ aquirido.$$

	![[Pasted image 20240611160850.png]]

- La regla divide naturalmente en dos fases a la ejecución de la transacción:
	- Una fase de adquisición de locks, en la que la cantidad de locks adquiridos crece.
	- Una fase de liberación de locks, en que la cantidad de locks adquiridos decrece.
- <span style="color:#ffff00">El cumplimiento de este protocolo es condición suficiente para garantizar que cualquier orden de ejecución de un conjunto de transacciones sea serializable.</span>
- Sin embargo, la utilización de locks introduce otros dos problemas potenciales que antes no teníamos:
	- Deadlocks.
	- Inanición o postergacion indefinida(livelock).

### <span style="color:#c00000">Acceso a estructuras de árbol</span>
- Generalmente los DBMS cuentan con estructuras de búsqueda de tipo árbol B+, tales que los bloques de datos se encuentran en las hojas.
- A los locks que se aplican sobre los nodos de un indice se los denomina index locks.
- Para mantener la serializabilidad en el acceso a estas estructuras, es necesario seguir las siguientes reglas:
	- Todos los nodos accedidos deben ser lockeados.
	- Cualquier nodo puede ser el primero en ser lockeado por la transacción(aunque generalmente es la raíz).
	- Cada nodo subsecuente puede ser lockeado solo si se posee un lock sobre su nodo padre.
	- Los nodos pueden ser deslockeados en cualquier momento.
	- Un nodo que fue deslockeado no puede volver a ser lockeado.

#### <span style="color:#c00000">Protocolo del Cangrejo(Crabbing protocol)</span>
- Protocolo para el acceso concurrente a estructuras del árbol:
	1. Comenzar obteniendo un lock sobre el nodo root.
	2. Hasta llegar a el/los nodo/s deseado/s, adquirir un lock sobre el/los hijo/s que se quiere acceder, y liberar el lock sobre el padre si los nodos hijo son seguros(es decir, el nodo hijo no esta lleno si estamos haciendo una inserción, ni esta justo por la mitad en el caso de una eliminación).
	3. Una vez terminada la operación, deslockear todos los nodos.

### <span style="color:#c00000">Control de Concurrencia utilizando timestamps</span> 
- Se asigna a cada transacción $T_i$ un timestamps $TS(T_i)$.
- Los timestamps deben ser únicos, y determinaran el orden serial respecto al cual el solapamiento deberá ser equivalente.
- Se permite la ocurrencia de conflictos, pero siempre que las transacciones de cada conflicto aparezcan de acuerdo al orden serial equivalente:
	-  ($W_{T_i}(X), R_{T_j}(X)$) -> $TS(T_i) < TS(T_j)$
- Al no emplear locks, este método esta exento de deadlocks.
- Se debe mantener en todo instante, para cada item X, la siguiente información:
	- `read_TS(X)`: Es el TS(T) correspondiente a la transacción mas joven(de mayor TS(T)) que leyó el item X.
	- `write_TS(X)`: es el TS(T) correspondiente a la transacción mas joven(de mayor TS(T)) que escribió el item X.

- Lógica de funcionamiento:
	1. Cuando una transacción $T_i$ quiere ejecutar un R(X):
		-  Si una transacción $T_j$ modifico el item $T_i$ deberá ser abortada(read too late).
		- De lo contrario, actualiza `read_TS(X)` y lee.
	2. Cuando una transacción $T_i$ quiere ejecutar un W(X):
		- Si una transacción posterior $T_j$ leyó o escribió el item, $T_i$ deberá ser abortada(write too late).
		- De lo contrario, actualiza `write_TS(X)` y escribe.
- La ejecución de los R(X) y W(X), y actualización de `read_TS(X)` y `write_TS(X)` se centraliza en el [[Scheduler]].    

## <span style="color:#c00000">Snapshot Isolation</span> 
- Cada transacción ve una snapshot de la DB correspondiente al instante de su inicio.
	- Permite un mayor solapamiento, ya que lecturas que hubieran sido bloqueadas mediante locks, ahora siempre pueden realizarse.
	- Requiere de mayor espacio en disco o memoria, al tener que mantener multiples versiones de los mismos items.
	- Cuando ocurren conflictos del tipo WW entre transacciones, obliga a deshacer una de ellas.
- Cuando dos transacciones intentan modificar un mismo item de datos, generalmente gana aquella que hace primero su commit, mientras que la otra deberá ser abortada(first-committer-wins).
- Esto por si solo no alcanza para garantizar la serializabilidad -> debe combinarse con dos elementos mas:
	- Validación permanente con el grafo de precedencias buscando ciclos de conflictos RW.
	- Locks de predicados en el proceso de detección de conflictos, para detectar precedencias.
