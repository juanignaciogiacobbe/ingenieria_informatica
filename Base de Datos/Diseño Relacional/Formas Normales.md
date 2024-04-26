# <span style="color:#c00000">Formas Normales</span> 

> Son una serie de estructuras con las que un esquema de base de datos puede cumplir o no.
> Cada forma normal es mas fuerte que las anteriores.

S esta en 5FN -> S esta en 4FN -> ... -> S esta en 1FN

## <span style="color:#c00000">Normalizacion</span> 

> Proceso a través del cual se convierte un esquema de base de datos en uno equivalente(que preserva toda la información) y que cumple con una determinada formal normal.

#### Objetivos:
- Preservar la información.
- Eliminar la redundancia.
- Evitar las anomalías de ABM.

## <span style="color:#c00000">1FN</span> 

> Cuando los dominios de todos sus atributos <span style="color:#ffff00">solo permiten valores atómicos y monovaluados</span>.
> Actualmente se considera que en el modelo relacional todos los atributos deben ser monovaluados y atómicos.
## <span style="color:#c00000">2FN</span>

>  Una <span style="color:#ffff00">dependencia funcional</span> $X \rightarrow Y$ <span style="color:#ffff00">es parcial</span> cuando existe un subconjunto propio $A \subset X, A \neq X$ para el cual $A \rightarrow Y$
> <span style="color:#ffff00">Una dependencia funcional es completa</span> si y solo si no es parcial.
> <span style="color:#ffff00">Atributo primo de una relación</span>: es aquel que es parte de alguna clave candidata de la relación.  
> Una relación esta en 2FN cuando todos sus atributos no primos tienen dependencia funcional completa de las claves candidatas.


![[Pasted image 20240421105812.png]]