# <span style="color:#c00000">Formas Normales</span> 

> Son una serie de estructuras con las que un esquema de base de datos puede cumplir o no.
> Cada forma normal es mas fuerte que las anteriores.<span style="color:#ffff00"> A medida que avanzamos en la normalización, se minimiza la redundancia de datos</span>, una propiedad deseable en todo esquema de DB.

S esta en 5FN -> S esta en 4FN -> ... -> S esta en 1FN

## <span style="color:#c00000">Normalizacion</span> 

> Proceso a través del cual se convierte un esquema de base de datos en uno equivalente(que preserva toda la información) y que cumple con una determinada formal normal.
> <span style="color:#ffff00">Busca preservar la información, eliminar la redundancia, y evitar las anomalías de ABM.</span>
> Se parte de un conjunto de dependencias funcionales que supondremos definido por el diseñador de la DB.
> A partir de estas dependencias, nos interesa generar una descomposición lo menos redundante posible, preservando la información y las dependencias funcionales. Se utilizaran [[Algoritmos de Normalizacion]] para convertir un esquema de DB a 3FN y a FNBC.

## <span style="color:#c00000">1FN</span> 

> Cuando los dominios de todos sus atributos <span style="color:#ffff00">solo permiten valores atómicos y monovaluados</span>.
> Actualmente se considera que en el modelo relacional todos los atributos deben ser monovaluados y atómicos.
## <span style="color:#c00000">2FN</span>

>  Una <span style="color:#ffff00">dependencia funcional</span> $X \rightarrow Y$ <span style="color:#ffff00">es parcial</span> cuando existe un subconjunto propio $A \subset X, A \neq X$ para el cual $A \rightarrow Y$
> <span style="color:#ffff00">Una dependencia funcional es completa</span> si y solo si no es parcial.
> <span style="color:#ffff00">Atributo primo de una relación</span>: es aquel que es parte de alguna clave candidata de la relación.  
> Una relación esta en 2FN cuando todos sus atributos no primos tienen dependencia funcional completa de las claves candidatas.
> Para ver si estas en 2FN o no: primero se obtiene la clave de la relación, y luego se ve si hay dependencias parciales de la clave.


![[Pasted image 20240421105812.png]]

$$\forall \; dependencia \; funcional \; no \; trivial \; X \rightarrow Y \in F:$$
$$ X \; es\; superclave \; o \; Y-X \; contiene \; solo \; atributos \; primos \; o \; X \; no \; es  \; subclave.$$

- La idea seria descomponer la relación para que quede en 2FN. Si una descomposición cumple que para toda instancia posible de R, la junta de las proyecciones sobre los $R_i$ permite recuperar la misma instancia de relación, entonces decimos que la descomposición preserva la información.
- La descomposición preserva las dependencias funcionales cuando toda dependencia funcional X -> Y en R puede inferirse a partir de dependencias funcionales definidas en los $R_i$.

## <span style="color:#c00000">3FN</span> 
> No hay dependencias funcionales transitivas de atributos no primos de una clave candidata.

$$\forall \; dependencia \; funcional \; no \; trivial \; X \rightarrow Y \in F:$$
$$ X \; es\; superclave \; o \; Y-X \; contiene \; solo \; atributos \; primos.$$
## <span style="color:#c00000">Forma Normal de Boyce-Codd(FNBC)</span> 
> No hay dependencias funcionales transitivas de una clave candidata.
> Una relación esta en FNBC cuando para toda dependencia funcional no trivial X -> Y, X es superclave.

$$\forall \; dependencia \; funcional \; no \; trivial \; X \rightarrow Y \in F: X \; es\; superclave.$$