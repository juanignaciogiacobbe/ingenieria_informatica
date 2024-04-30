# <span style="color:#c00000">Diseño Relacional</span> 

## <span style="color:#c00000">Criterios de un buen Diseño Relacional</span> 
- <span style="color:#ffff00">"Hechos distintos se deben almacenar en objetos distintos"</span>. 
- Preservación de información.
- Minima redundancia.
- Al partir de un correcto diseño conceptual y se hace un correcto pasaje al modelo lógico, se obtiene un esquema sin redundancia y se preserva toda la información del mundo real que se quería modelar.
- Se formalizan estos requisitos a través de las [[Formas Normales]].

## <span style="color:#c00000">Teoria de Dependencias Funcionales</span> 

>Dada una relación $R(A_1, A_2, ...)$, una dependencia funcional X -> Y, con X, Y contenidos en $A_1, A_2, ...$ es una restricción sobre el conjunto de tuplas que pueden aparecer en una relación.
>Si Y esta contenido en X, se habla de una restricción trivial.
>Tiene como objetivo <span style="color:#ffff00">formalizar restricciones</span> que tienen nuestros datos a través de las formas normales.
><span style="color:#ffff00">Se definen a partir de la semantica de los datos, NO viendo los datos</span>.
>A partir de un relato que nos brindara el conocedor el dominio del problema, deberemos identificar las dependencias funcionales de ese dominio.

$$\forall s, t \in R: s[X] = t[X] \rightarrow s[Y] = t[Y]$$

- Ejemplo: Si tengo que una $R(A, B, C, D, E)$ con $X = \{C,D\}$ e $Y = {E}$, y la dependencia $X \rightarrow Y$ entonces a cada posible valor de X le corresponde un ÚNICO valor de Y.
- Es fácil ver en los datos que dependencias NO RIGEN, pero no podemos asegurar nada sobre las que SI RIGEN.
- Cuando $Y \subseteq X$ decimos que $X \rightarrow Y$ es trivial.