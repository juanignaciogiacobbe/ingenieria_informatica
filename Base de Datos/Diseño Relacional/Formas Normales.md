# <span style="color:#c00000">Formas Normales</span> 

> Son una serie de estructuras con las que un esquema de base de datos puede cumplir o no.
> Cada forma normal es mas fuerte que las anteriores.

S esta en 5FN -> S esta en 4FN -> ... -> S esta en 1FN

## <span style="color:#c00000">Normalizacion</span> 

> Proceso a traves del cual se convierte un esquema de base de datos en uno equivalente(que preserva toda la informacion) y que cumple con una determinada formal normal.

#### Objetivos:
- Preservar la informacion.
- Eliminar la redundancia.
- Evitar las anomalias de ABM.

## <span style="color:#c00000">1FN</span> 

> Cuando los dominios de todos sus atributos solo permiten valores atomicos y monovaluados.
> Actualmente se considera que en el modelo relacional todos los atributos deben ser monovaluados y atomicos.


## <span style="color:#c00000">2FN</span>

> Cuando todos los atributos no primos tienen dependencia funcional completa de las claves candidatas.
> Atributo primo de una relacion: es que es parte de alguna clave candidata de la relacion.  

![[Pasted image 20240421105812.png]]