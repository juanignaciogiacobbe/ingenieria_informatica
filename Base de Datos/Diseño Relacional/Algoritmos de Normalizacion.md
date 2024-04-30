# <span style="color:#c00000">Algoritmos de Normalizacion</span> 
> Supongamos que el diseñador de la DB definió un conjunto de dependencias funcionales F a partir de la semántica. A partir de esas dependencias, nos interesa generar una descomposición lo menos redundante posible, preservando la información y las dependencias funcionales.

## <span style="color:#c00000">Inferencia de Dependencias Funcionales</span>
> Pueden ser probados a partir de la definición de dependencias funcionales.
> Los 3 axiomas son completos: toda dependencia funcional que se puede inferir de F se puede inferir a través de los <span style="color:#c00000">Axiomas de Armstrong</span>:
- <span style="color:#ffff00">Reflexividad</span>: $Si \; Y \; \subseteq \; X \; inferir \; X \; \rightarrow \; Y$
- <span style="color:#ffff00">Aumento</span>: $Para \; cualquier \; conjunto \; W, \; de \; X \; \rightarrow \; Y \; inferir \; XW \; \rightarrow \; YW$ 
- <span style="color:#ffff00">Transitividad</span>: $De \; X \rightarrow \; Y \; e \; Y \; \rightarrow \; Z \; inferir \; X \; \rightarrow \; Z$ 

### <span style="color:#c00000">Reglas útiles</span> 
- <span style="color:#ffff00">Regla de union</span>: X -> Y y X -> Z entonces X -> YZ
- <span style="color:#ffff00">Regla de pseudotransitividad</span>:  Para todo W: X -> Y y YW -> Z entonces XW -> Z
- <span style="color:#ffff00">Regla de descomposicion</span>: X -> YZ entonces X -> Y y y X -> Z

## <span style="color:#c00000">Clausuras F+</span>
> Dado un conjunto de dependencias funcionales F, sea la clausura $F^+$ el conjunto de todas las dependencias funcionales que pueden inferirse usando los Axiomas de Armstrong.
> F y G son equivalentes si y solo si $F^+ = G^+$.

## <span style="color:#c00000">Clausura de un conjunto de atributos</span> 
> Dado un esquema de relación R, un conjunto de dependencias funcionales F y un conjunto de atributos $X \subseteq R$, se define como clausura de X con respecto a F, indicada como $X_{F^+}$, como el conjunto de todos los atributos $A \subseteq R$ tal que X -> A puede ser derivado desde F utilizando los axiomas de todas las formas posibles. 

## <span style="color:#c00000">Cubrimientos Minimales</span> 
- Todo implicado de una dependencia funcional de $F_M$ tiene un único atributo(es simple).
- Todo determinante de una dependencia funcional de $F_M$ es reducido(no tiene atributos redundantes).
- $F_M$ no contiene dependencias funcionales redundantes.

### <span style="color:#c00000">Algoritmo para hallar un cubrimiento minimal</span> 
1. Se dejan todos los lados derechos de las dependencias funcionales con un único atributo.
2. Eliminar los atributos redundantes del lado izquierdo.
3. Eliminar las dependencias funcionales redundantes.