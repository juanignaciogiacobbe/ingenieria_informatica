## <span style="color:#c00000">Recuperabilidad</span> 
- Nos interesa asegurar que una vez que una transacción commiteo, la misma no deba ser deshecha -> Esto ayudara a implementar de una forma sencilla la propiedad de Durabilidad.
- Un solapamiento es recuperable si y solo si ninguna transacción T realiza el commit hasta tanto todas las transacciones que escribieron datos antes de que T los leyera hayan commiteado.
- Un DBMS no debería jamas permitir la ejecución de un solapamiento que no sea recuperable.

## <span style="color:#c00000">Fallas</span> 
- Los sistemas reales sufren multiples tipos de fallas:
	- De sistema: Por errores de software o hardware que detienen la ejecución de un programa(fallas de segmentación, division por 0, fallas de memoria).
	- De aplicación: Aquellas que provienen desde la aplicación que utiliza la DB. Por ejemplo, la cancelación o vuelta atrás de una transacción.
	- De dispositivos: Aquellas que provienen de un daño físico en dispositivos como discos rígidos o memoria.
	- Fallas naturales externas: Aquellas que provienen desde afuera del hardware en que se ejecuta nuestro [[DataBase Management System(DBMS)]]. Ejemplos: caídas de tension, terremotos, etc.

## <span style="color:#c00000">Tecnicas de volcado(flush) a disco</span> 
- Actualización inmediata: Los datos se guardan en disco lo antes posible, y necesariamente antes del commit de la transacción.
- Actualización diferida: Los datos se guardan en disco después del commit de la transacción.

## <span style="color:#c00000">Gestor de Recuperación</span>
- Dado un solapamiento recuperable, puede ser necesario deshacer(abortar) una transacción antes de llegado su commit, y para ello el DBMS deberá contar con una serie de información que es almacenada por su gestor de recuperación en un log.

	![[Pasted image 20240612134511.png]]

- El gestor de logs se guía por dos reglas básicas:
	- WAL(Write Ahead Log): Indica que antes de guardar un item modificado en disco, se debe escribir el registro de log correspondiente, en disco.
	- FLC(Force Log Commit): Antes de realizar el commit, el log debe ser volcado a disco.


## <span style="color:#c00000">Algoritmos de recuperación</span> 
- Se asume que los solapamientos de transacciones son recuperables, y que evitan rollbacks en cascada.

### <span style="color:#c00000">Regla de UNDO</span> 
- Antes de que una modificación sobre un item $X$ <- $v_{new}$ por parte de una transacción no commiteada sea guardada en disco(flushed), se debe salvaguardar en el log en disco el ultimo valor commiteado $v_{old}$ de ese item.

1. Cuando una transacción $T_i$ modifica el item X reemplazando un valor $v_{old}$ por $v$, se escribe(WRITE, $T_i$, X, $v_{old}$) en el log, y se hace flush del log a disco.
2. El registro (WRITE, $T_i$, X, $v_{old}$) debe ser escrito en el log en disco(flushed) antes de escribir(flush) el nuevo valor de X en disco(WAL).
3. Todo item modificado debe ser guardado en disco antes de hacer commit.
4. Cuando $T_i$ hace commit, se escribe(COMMIT, $T_i$) en el log y se hace flush del log a disco(FLC).

- Con los primeros 3 pasos nos aseguramos de que todas las modificaciones realizadas sean escritas a disco antes de que la transacción termine.
- De esta forma, una vez cumpliendo el paso 4, ya nunca sera necesario hacer REDO. Si la transacción falla antes o durante el punto 4, sera deshecha(UNDO) al reiniciar.
- Se considera que la transacción commiteó cuando el registro (COMMIT, $T_i$) quedo escrito en el log, en disco.