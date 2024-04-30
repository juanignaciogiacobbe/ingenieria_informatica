# <span style="color:#c00000">Modelo Logico Relacional</span>

> Se vincula con la representación de los datos.
> Representación en tablas.
> Es una formalizacion matemática basada en el concepto de Relación.

### <span style="color:#c00000">Definiciones importantes</span> 
- <span style="color:#ffff00">Dominio</span>: Es el conjunto de valores homogéneos. Ej: $D = \{Bs As, Sevilla, Cordoba\}$.
- <span style="color:#ffff00">Producto cartesiano</span>: A x B se define como el conjunto de pares (a, b) que cumplen que $a \in A$ y $b \in B$.
- <span style="color:#ffff00">Relacion</span>: Es un subconjunto de un producto cartesiano. Las funciones de matemática son relaciones :D. Se las representan en tablas. 
- <span style="color:#ffff00">Esquema de Relacion</span>: Cuando se tiene una relación R y una lista de atributos. Se denota como $R(A_{1}, A_{2}, ..., A_{n})$ . Cada uno de los atributos esta asociado a un dominio particular. Los atributos representan en las columnas de las tablas.
- <span style="color:#ffff00">Tupla</span>: Un elemento de una relación. Son las filas de las tablas.


## <span style="color:#c00000">Restricciones</span> 
> Representan generalmente entidades o interrelaciones de nuestro modelo de datos.

### <span style="color:#c00000">Restricciones de Dominio</span> 
- Especifican que dado un atributo A de una relación R, <span style="color:#ffff00">el valor de A en una tupla t debe pertenecer al dominio Dom(A)</span>.
- Se puede permitir los valores <span style="color:#ffff00">NULL</span>.
- Los <span style="color:#ffff00">atributos</span> deben ser <span style="color:#ffff00">atomicos</span>(no se permiten compuestos o multivaluados).

### <span style="color:#c00000">Restricciones de Unicidad</span> 
- No pueden existir dos tuplas distintas que coincidan en los valores de todos sus atributos.
- Existe un conjunto SK del conjunto de atributos de R que cumple la condición de que dadas dos tuplas $s, t \in R$, las mismas difieren en al menos uno de los atributos de SK. SK se la llama <span style="color:#ffff00">superclave</span> de R.
- Las superclaves minimales se las llaman <span style="color:#ffff00">claves candidatas</span>.
- De entre todas las claves candidatas elegiremos una como <span style="color:#ffff00">clave primaria</span> de R.

### <span style="color:#c00000">Restricciones de Integridad</span> 
- Se tienen en cuenta para Esquemas de Base de Datos Relacional.
- <span style="color:#ffff00">Restriccion de Integridad de Entidad</span>: La PK de una relación no puede ser NULL.
- <span style="color:#ffff00">Restriccion de Integridad Referencial</span>: Cuando un conjunto de atributos FK de una relación R hace referencia a la clave primaria de otra relación S, entonces para toda tupla de R debe existir una tupla de S cuya PK sea igual al valor de FK, a menos que todos los atributos de FK sean NULL. Entonces, FK se la llama <span style="color:#ffff00">Clave Foranea</span>.  


## <span style="color:#c00000">Pasaje del Modelo Conceptual al Modelo Relacional</span> 
- Cada entidad del modelo ER producirá generalmente una relación del modelo relacional.
- Atributos multivaluados: Se crea una tabla para el atributo.

## <span style="color:#c00000">Problemas que se presentan en esquemas defectuosos</span>
> Se evitan utilizando conceptos del [[Diseño Relacional]]

- Incapacidad para almacenar ciertos hechos.
- Redundancias -> inconsistencias.
- Ambigüedades.
- Perdida de información y dependencias funcionales.
- Existencia de valores nulos.
- Aparición, en la DB, de estados que no son validos en el mundo real.