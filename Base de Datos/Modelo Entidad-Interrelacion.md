# <span style="color:#c00000">Modelo Entidad-Interrelacion</span>

- <span style="color:#ffff00">Tipo de Entidad</span>: Tipo o clase de objeto en particular. **PROTOTIPO**
- <span style="color:#ffff00">Entidad</span>: Instancia de un tipo de entidad. **INSTANCIA**
- <span style="color:#ffff00">Atributo</span>: Una propiedad que describe a la entidad.
- <span style="color:#ffff00">Tipo de Interrelacion</span>: Definicion de un conjunto de relaciones o asociaciones similares entre dos o mas tipos de entidades.

## <span style="color:#c00000">Atributos</span>

> Cada entidad tendra valores particulares para cada uno de los atributos del tipo de entidad al que corresponde.

- <span style="color:#ffff00">Dominio de un atributo</span>: Conjunto de valores que el mismo puede tomar.
- En ciertos casos puede permitirse que un atributo de un tipo de entidad no tome ningun valor concreto de ciertas instancias. En este caso toma un valor **NULL**. 
- Todo tipo de entidad debe tener un subconjunto del conjunto de atributos, cuyos valores sean necesariamente distintos para cada una de las entidades en el conjunto de entidades. Estos atributos son los <span style="color:#c00000">atributos clave o identificadores unicos</span>. Me aseguran que no hayan dos filas con los mismos valores.
- El conjunto de atributos clave debe ser <span style="color:#ffff00">minimal</span>, es decir que ningun subconjunto del mismo sea capaz de identificar univocamente a las entidades.
- La <span style="color:#ffff00">cardinalidad</span> es la maxima cantidad de instancias de cada tipo de entidad que pueden relacionarse con una instancia concreta de los tipos de entidades restantes.