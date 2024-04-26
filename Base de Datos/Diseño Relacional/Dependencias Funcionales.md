# <span style="color:#c00000">Teoria de Dependencias Funcionales</span> 

>Dada una relación $R(A_1, A_2, ...)$, una dependencia funcional X -> Y, con X, Y contenidos en $A_1, A_2, ...$ es una restricción sobre las posibles tuplas de R que implica que dos tuplas con igual valor del conjunto de atributos X también deben tener igual valor del conjunto de atributos Y.
>Si Y esta contenido en X, se habla de una restricción trivial.
>Tiene como objetivo <span style="color:#ffff00">formalizar restricciones</span> que tienen nuestros datos a través de las formas normales.
><span style="color:#ffff00">Se definen a partir de la semantica de los datos, NO viendo los datos</span>.
>A partir de un relato que nos brindara el conocedor el dominio del problema, deberemos identificar las dependencias funcionales de ese dominio.

$$\forall s, t \in R: s[X] = t[X] \rightarrow s[Y] = t[Y]$$

- Ejemplo: Si tengo que una $R(A, B, C, D, E)$ con $X = \{C,D\}$ e $Y = {E}$, y la dependencia $X \rightarrow Y$ entonces a cada posible valor de X le corresponde un ÚNICO valor de Y.
- Es fácil ver en los datos que dependencias NO RIGEN, pero no podemos asegurar nada sobre las que SI RIGEN.


## <span style="color:#c00000">Axiomas de Armstrong(RAT)</span> 
- <span style="color:#ffff00">Reflexividad</span>: $Si \; Y \; \subseteq \; X \; inferir \; X \; \rightarrow \; Y$
- <span style="color:#ffff00">Aumento</span>: $Para \; cualquier \; conjunto \; W, \; de \; X \; \rightarrow \; Y \; inferir \; XW \; \rightarrow \; YW$ 
- <span style="color:#ffff00">Transitividad</span>: $De \; X \rightarrow \; Y \; e \; Y \; \rightarrow \; Z \; inferir \; X \; \rightarrow \; Z$ 