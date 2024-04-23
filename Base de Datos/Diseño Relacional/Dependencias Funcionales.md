## <span style="color:#c00000">Teoria de Dependencias Funcionales</span> 

>Dada una relacion R(A1, A2, ...), una dependencia funcional X -> Y, con X, Y contenidos en A1, A2, ... es una restriccion sobre las posibles tuplas de R que implica que dos tuplas con igual valor del conjunto de atributos X tambien deben tener igual valor del conjunto de atributos Y.
>Si Y esta contenido en X, se habla de una restriccion trivial.
>Tiene como objetivo <span style="color:#ffff00">formalizar restricciones</span> que tienen nuestros datos a traves de las formas normales.
><span style="color:#ffff00">Se definen a partir de la semantica de los datos, NO viendo los datos</span>.

$$\forall s, t \in R: s[X] = t[X] \rightarrow s[Y] = t[Y]$$

Ejemplo: Si tengo que una R(A, B, C, D, E) con X = {C,D} e Y = {E}, y la dependencia X -> Y
entonces a cada posible valor de X le corresponde un UNICO valor de Y.