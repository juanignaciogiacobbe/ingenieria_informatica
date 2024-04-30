# <span style="color:#c00000">Algebra Relacional</span>

- Provee un marco formal de operaciones para el [[Modelo Logico Relacional]].
- Se emplea como base para optimizar la ejecución de consultas en los DBMS.
- Especifica los procedimientos de consulta de datos a partir de un conjunto de operaciones.
- Algunos de sus conceptos se han incorporado a [[SQL]].

## <span style="color:#c00000">Operaciones</span> 
> Una operación en el contexto del modelo relacional, es una función cuyos operandos son una o mas relaciones, y cuyo resultado es también una relación.
> La <span style="color:#ffff00">aridad</span> es la cantidad de operandos que toma una operación.
> <span style="color:#ffff00">Las operaciones</span> del algebra relacional <span style="color:#ffff00">pueden combinarse entre ellas para formar una expresion</span>.
> $O: R_1 \; x \; R_2 \; x \; ... \; x \; R_n \; \rightarrow \; S$

### <span style="color:#c00000">Seleccion</span> $\sigma$
> $\sigma_{cond} (R)$ selecciona aquellas tuplas de R para las cuales la condición es verdadera.
   $\sigma_{cond}:\; R \;\rightarrow \;S$

### <span style="color:#c00000">Proyeccion</span> $\pi$
> $\pi_{L} (R)$ devuelve una relación cuyas tuplas representan los posibles valores de los atributos de L en R. Siempre remueve tuplas duplicadas.
> Podemos pensar que proyecta cada tupla de R a un espacio de menor dimension en que solo se conservan los atributos que están en L.
> $\pi_{L}:\; R \;\rightarrow \;S$

### <span style="color:#c00000">Asignacion</span> $\leftarrow$ 
> $\leftarrow$  Permite dividir la expresión(básicamente sirve para declarar variables y que la query sea mas legible).

### <span style="color:#c00000">Redenominacion</span> $\rho$  
> $\rho$ permite modificar los nombres de los atributos de una relación y/o el de la relación misma.
> Permite preparar el resultado para la realización de una operación posterior. 
   $\rho_{S(B_1, ..., B_n)}(R)$

### <span style="color:#c00000">Union</span> $\cup$    
> Dadas dos relaciones R y S, $R \cup S$ es una relación que contiene a todas las tuplas de R y S.
> Es necesario que R y S tengan = grado.
> <span style="color:#ffff00">Compatibilidad de union o tipo</span>: las relaciones deben coincidir en sus atributos en lo que respecta al dominio.

### <span style="color:#c00000">Interseccion</span> $\cap$    
> Dadas dos relaciones R y S, $R \cap S$ es una relación que conserva las tuplas que se encuentran tanto en R como en S.
> Es necesario que R y S tengan = grado.
> <span style="color:#ffff00">Requiere compatibilidad de union o tipo</span>.

### <span style="color:#c00000">Diferencia</span> $-$    
> Dadas dos relaciones R y S, $R - S$ es una relación que conserva aquellas tuplas de R que no pertenecen a S.
> Es necesario que R y S tengan = grado.
> <span style="color:#ffff00">Requiere compatibilidad de union o tipo</span>.

### <span style="color:#c00000">Producto Cartesiano</span> $x$    
> Dadas dos relaciones R y S, $R \; x \; S$ es una relación T cuyas tuplas son todas aquellas de la forma: $(t_1, ..., t_n, t_{n+1}, ..., t_{n+m})$ con $(t_1, ..., t_n) \in R$ y $(t_{n+1}, ..., t_{n+m}) \in S$

### <span style="color:#c00000">Junta</span> $\bowtie$     
> Combina un producto cartesiano con una selección. 
> Dadas dos relaciones R y S y una condición, la junta $R \bowtie (cond) \; S$ selecciona del producto cartesiano $R \; x \; S$ las tuplas que cumplen la condición.
> Cuando las comparaciones son de igualdad en sus condiciones atómicas, es una <span style="color:#ffff00">junta por igual</span>.
> En la junta por igual, el resultado dispondrá de pares de atributos distintos que poseerán información redundante. Para librarse de uno de ellos, se utiliza la <span style="color:#ffff00">junta natural</span>.

### <span style="color:#c00000">Division</span> $÷$     
> Es una operación inversa al producto cartesiano. Muestra como resultado los elementos del conjunto A que se relacionan con todos los elementos del conjunto B.
> Partimos de dos relaciones $R(A_1, ..., A_n) \; y \; S(B_1, ..., B_n)$ cuyos atributos están incluidos en los de R. $B \subset A$.
> $Y = A - B$
> Se define a la division $R \; ÷ \; S$ como la relación T(Y) que contiene a todas las tuplas t que pertenecen a $\pi_Y (R)$ y para cada tupla $t_S \in S$ existe una tupla $t_R \in R$ tal que $t_R[Y] = t$ y $t_R[B] = t_S$






