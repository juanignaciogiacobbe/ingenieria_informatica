# <span style="color:#c00000">Base de Datos(DB)</span>

> Conjunto de Datos interrelacionados.
> Las DB tradicionales almacenan datos de texto o numéricos, que pueden enunciarse a través de proposiciones. Solo almacenan proposiciones verdaderas.

## <span style="color:#c00000">Dato</span>

> Es un hecho que puede ser representado y almacenado de alguna forma, y que tiene un sentido implícito. 
> Ej: La mesa consumió 5 napos y 1 botella de vino.

# <span style="color:#c00000">Arquitectura de 3 capas ANSI/SPARC</span>

> Es una arquitectura de <span style="color:#ffff00">3 niveles de abstracción para la descripción y representación de los datos en una DB</span>.
> <span style="color:#ffff00">Asegura la independencia de datos</span>, tanto física como lógica.

![[Pasted image 20240420091405.png]]

- <span style="color:#ffff00">Modelo interno</span>: Representa la forma en que los datos se almacenan utilizando estructuras de datos y organizaciones de archivos. Representa como perciben los datos los [[Sistemas Operativos(SO)]] y el [[DataBase Management System(DBMS)]].
- [[Modelo Conceptual]]: Describe la semántica de los datos, incluyendo sus características tanto estáticas como dinámicas.
- [[Modelo Logico Relacional]]: Es un paso intermedio entre el modelo conceptual y el modelo interno, que formaliza las descripciones del modelo conceptual.
- <span style="color:#ffff00">Modelo externo</span>: Representa la forma en que los usuarios perciben los datos.
## <span style="color:#c00000">Como interactuamos con los modelos</span>
- Lo hacemos a través de un <span style="color:#ffff00">lenguaje</span>.
- Los <span style="color:#ffff00">lenguajes de manipulacion de datos</span>(DML) nos permiten extraer información de un modelo de datos.

	![[Pasted image 20240423144550.png]]
	
- Los <span style="color:#ffff00">lenguajes procedurales</span>(de bajo nivel) indican un propósito a seguir, utilizando operaciones que indican como manipular los datos. Ejemplos:
	- [[Algebra Relacional]]
- Los <span style="color:#ffff00">lenguajes declarativos</span> indican que resultado se quiere obtener, sin especificar como hacerlo.

