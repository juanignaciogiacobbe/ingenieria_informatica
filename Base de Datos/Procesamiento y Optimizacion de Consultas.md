## <span style="color:#c00000">Esquema de Procesamiento</span>

	![[Pasted image 20240618200623.png]]

## <span style="color:#c00000">Información de catalogo</span> 
- Los [[DataBase Management System(DBMS)]] guardan distintos tipos de información de catalogo que es utilizada para estimar costos y optimizar las consultas.
- n(R): Cantidad de tuplas de la relación R.
- B(R): Cantidad de bloques de almacenamiento que ocupa R.
- V(A, R): Cantidad de valores distintos que adopta el atributo A en R(variabilidad).
- F(R): Cantidad de tuplas de R que entran en un bloque(factor de bloque).$F(R) = \frac{n(R)}{B(R)} \rightarrow B(R) = \frac{n(R)}{F(R)}$ 
- También se almacena información sobre la cantidad de niveles que tienen los indices cosntruidos, y la cantidad de bloques que ocupan sus hojas.
- Height(I(A, R)): Altura del indice de búsqueda I por el atributo A de la relación R.
- Length(I(A, R)): Cantidad de bloques que ocupan las hojas del indice I.

## <span style="color:#c00000">Plan de consulta y plan de ejecución</span> 
- La optimizacion de una consulta se inicia con una expresión en algebra relacional.
- La expresión se optimiza a través de una heuristica y utilizando reglas de equivalencia, obteniendo un plan de consulta.
- Luego, cada plan de consulta lógico se materializa para obtener un plan de ejecución en el que se indica el procedimiento físico: estructuras de datos a utilizar, indices, algoritmos a utilizar, etc.
- Para comparar distintos planes de ejecución, necesitamos estimar su costo. Algunos de los factores que inciden en la performance son:
	- El costo de acceso de disco(lectura o escritura).
	- El costo de procesamiento.
	- El costo de uso de memoria.
	- El costo de uso de red.