# <span style="color:#c00000">Structured Query Language(SQL)</span>
- Es una gramática libre de contexto -> su sintaxis puede ser descrita a través de reglas de producción.

## Diferencias con [[Modelo Logico Relacional]]
- En el modelo relacional una relación es un conjunto cuyos elementos son las tuplas por lo que, una tupla no puede estar repetida en una relación.
- En SQL se permite que una fila este repetida muchas veces en una tabla(esto se conoce como <span style="color:#ffff00">multiset o bag of tuples</span>). Lo podemos evitar utilizando DISTINCT.

## <span style="color:#c00000">Definición de Datos</span> 

### <span style="color:#c00000">CREATE_SCHEMA nombre [authorization autId]</span>
- Para crear un nuevo esquema de DB dentro de nuestro [[DataBase Management System(DBMS)]] .
- Authorization indica al dueño del esquema.
- Los esquemas se agrupan en colecciones llamadas catálogos. Todo catalogo contiene un esquema llamado INFORMATION_SCHEMA que describe a todos los esquemas contenidos en el.

### <span style="color:#c00000">Tipos de variables SQL</span>
- INTEGER.
- SMALLINT.
- FLOAT(n): n indica la precision.
- DOUBLE PRECISION.
- NUMERIC(i, j): i para precision, j para escala.
- String:
	- CHARACTER(n): De longitud fija.
	- CHARACTER VARYING(n): De longitud variable(VARCHAR).
- Fecha y hora:
	- DATE: Precision de días.
	- TIME(i): Precision de hasta microsegundos.
	- TIMESTAMP(i): Combina un DATE y un TIME.
- BOOLEAN: TRUE, FALSE O UNKNOWN(lógica de 3 variables).
- CLOB: Character Large Object.
- BLOB: Binary Large Object.
- CREATE DOMAIN tipo_nuevo as tipo: Permite definir nuevos tipos. 

## <span style="color:#c00000">CREATE_TABLE mi_tabla</span>
> Nos permite definir la estructura de una tabla.
> Siempre es recomendable poner una clave primaria(nunca debería ser NULL).
> Con la palabra clave UNIQUE, se indica que una columna o conjunto de columnas no puede estar repetido en dos filas distintas.
> 
> ![[Pasted image 20240429113726.png]]

![[Pasted image 20240429113551.png]]
![[Pasted image 20240429113652.png]]


## <span style="color:#c00000">Manipulación de Datos</span> 

### <span style="color:#c00000">Esquema básico de una consulta</span>
![[Pasted image 20240429114823.png]]

- $A_1, ..., A_n$ es una lista de nombres de columnas. 
- $T_1, ..., T_m$ es una lista de nombres de tablas. El FROM se podría pensar como un producto cartesiano en [[Algebra Relacional]].
- $condition$ es una condición sobre las tuplas.
- En FROM es posible indicar un alias para las tablas(ej: Persona p). Es util cuando hay ambigüedad. En SELECT también es posible poner alias: es util para redenominar los resultados(se pueden hacer operaciones en el SELECT).
- DISTINCT después de la clausula SELECT elimina los duplicados en el resultado.

### <span style="color:#c00000">Funciones de agregación</span>
> Se aplican a cada una de las columnas del resultado. Al usarlas, el resultado se colapsa a una única fila.
- SUM(A)
- COUNT([DISTINCT] A | $*$)
	- COUNT(A): Cuenta la cantidad de filas no nulas de A.
	- COUNT(DISTINCT A): Cuenta la cantidad de valores distintos de A, sin contar el NULL.
	- COUNT($*$): Cuenta la cantidad de filas en el resultado.
- AVG(A): Promedio de los valores de A, descartando los NULL.
- MAX(A), MIN(A): Solo para dominios ordenados.

### <span style="color:#c00000">Operaciones de conjuntos</span> 
- R UNION [ALL] S
- R INTERSECT [ALL] S
- R EXCEPT [ALL] S (Diferencia)
- Si no se agrega la palabra clave ALL, el resultado sera un set en vez de un multiset, y entonces no habrán filas repetidas.

### <span style="color:#c00000">Ordenamiento y Paginacion</span> 
- Las columnas de ordenamiento $A_{K_1}, ...,$ deben pertenecer a dominios ordenados, y deben estar incluidas dentro de las columnas de la proyección en la clausura SELECT.
- Si no se especifica, cada columna es ordenada en forma ascendente,
- La paginacion es la posibilidad de escoger un rango $[t_{inicio}, t_{fin}]$ del listado de filas del resultado.
	- La forma estándar es $[OFFSET..ROWS] \; FETCH \; FIRST..ROWS \; ONLY$ 
	
	![[Pasted image 20240429122445.png]]

### <span style="color:#c00000">Agregación</span>
- Colapsa las tuplas que coinciden en una serie de atributos, en una única tupla que las representa a todas.
- En SQL se puede hacer utilizando la clausula GROUP_BY. 
	- HAVING es opcional, y nos permite seleccionar solo algunos de los grupos del resultado.
	![[Pasted image 20240429123242.png]]


### <span style="color:#c00000">Inserciones</span> 
- Sirve para insertar el resultado de una consulta(debe devolver una tabla con k columnas, y las columnas deben ser union compatibles).
	![[Pasted image 20240429124938.png]]

### <span style="color:#c00000">Modificaciones</span> 
- Se realizan con el comando UPDATE.
- $condition$ puede ser una combinación de condiciones atómicas.
- Un único UPDATE puede modificar muchas filas.
	![[Pasted image 20240429125155.png]]

## <span style="color:#c00000">WITH RECURSIVE</span> 
- Amplia el poder expresivo de SQL permitiendo encontrar la clausura transitiva de una consulta.
- Dada una tabla T que es input de una consulta, permite que el resultado de la misma sea utilizado en el lugar de T para volver a ejecutar la misma consulta. Esto se repite hasta encontrar un punto fijo.
- <initial_value_query> no puede depender de T.
- Tanto en WITH como en WITH RECURSIVE puede definirse mas de una tabla auxiliar antes de la consulta.
- Por cada iteración no se pierde información, sino que se gana.

![[Pasted image 20240430081806.png]]

## <span style="color:#c00000">Funciones de Ventana</span> 
> Permiten aplicar un procesamiento final a los resultados de una consulta, siguiendo estos pasos:
1.  Dividiéndolos en grupos, llamados particiones.
2. Ordenando internamente cada partición.
3. Cruzando información entre las filas de cada partición.

- A cada atributo del SELECT de una consulta se le puede aplicar una función de ventana distinta, o bien puede no aplicarsele función alguna.

### <span style="color:#c00000">Funciones de Ventana de única partición</span> 
- Se considera a todo el resultado como una única partición.
	![[Pasted image 20240430083450.png]]
- Esto ordena el resultado de la consulta por el atributo $A_j$ y para cada fila imprime el resultado de una función de agregación $f(A_i)$ o de una función de ventana, $w([A_i], ...)$.
- Se pueden utilizar las funciones de ventana RANK, ROW_NUMBER, $LAG(A_i, offset)$, etc.
- Para cada columna a la que queremos aplicar una función de ventana debemos repetir la estructura OVER (ORDER BY ...), a la que llamamos ventana.
- A diferencia del GROUP BY, el OVER (ORDER BY ...) no agrupa, con lo cual no cambiara la cantidad de filas en el resultado.

### <span style="color:#c00000">Funciones de Ventana con multiples particiones</span>
- Antes de aplicar cada ventana se puede agrupar el resultado por el valor de un conjunto de atributos.
- A cada uno de estos grupos se lo denomina partición.
	![[Pasted image 20240430084604.png]]