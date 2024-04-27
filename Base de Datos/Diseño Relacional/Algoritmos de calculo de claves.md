# <span style="color:#c00000">Algoritmo de calculo de claves
</span>
1. Calcular el cubrimiento minimal de dependencias funcionales. 
2. Detectar atributos independientes del calculo $A_i$, eliminar del conjunto, $C_a = C_a - A_i$ y reservar para después.
3. Eliminar atributos equivalentes. Se reemplazan en la Df por el/los atributos equivalentes que se conservan en $C_a$.
4. Se forma K con todos los elementos que sean solo implicantes $A_i$, se calcula $K^+$ si es todo R -> K es clave.
5. Si K no resulto clave, se busca el conjunto de elementos que esten entre los implicantes pero que puedan ser implicados $A_{id}$