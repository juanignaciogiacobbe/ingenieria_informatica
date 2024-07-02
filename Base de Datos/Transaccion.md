# <span style="color:#c00000">Transacciones</span> 
> Unidad lógica de trabajo en los [[DataBase Management System(DBMS)]]. -> algo que tengo que hacer.
> Secuencia ordenada de instrucciones atómicas(deben ser ejecutadas en su totalidad o bien no ser ejecutadas, al margen de la interferencia con otras transacciones simultaneas).

- Una misma transacción puede realizar varias operaciones de consulta/ABM durante su ejecución.
- Antes de existir el multitasking, las transacciones se serializaban. Hasta tanto no terminara una, no se iniciaba la siguiente.
- Serializar en general es una mala idea. Nos gustaría poder ejecutarlas en forma simultanea, aunque garantizando ciertas propiedades básicas.

## <span style="color:#c00000">Propiedades ACID</span> 
- <span style="color:#ffff00">Atomicidad</span>: Desde el punto de vista del user, las transacciones deben ejecutarse de manera atómica. Esto quiere decir que, o bien la transacción se realiza por completo, o bien no se realiza. El gestor tiene un log de todo lo que esta haciendo, para poder deshacer tareas hechas por la mitad.
- <span style="color:#ffff00">Consistencia</span>: Cada ejecución, por si misma, debe preservar la consistencia de los datos. La consistencia se define a través de reglas de integridad: condiciones que deben verificarse sobre los datos en todo momento. 
- <span style="color:#ffff00">Aislamiento(isolation)</span>: El resultado de la ejecución concurrente de las transacciones debe ser el mismo que si las transacciones se ejecutaran en forma aislada una tras otra, es decir en forma serial. La ejecución concurrente debe entonces ser equivalente a alguna ejecución serial. 
- <span style="color:#ffff00">Durabilidad</span>: Una vez que el DBMS informa que la transacción se ha completado, debe garantizarse la persistencia de la misma, independientemente de toda falla que pueda ocurrir. 


## <span style="color:#c00000">Notación</span> 
- Para analizar la serializabilidad de un conjunto de transacciones en nuestro modelo de concurrencia solapada, utilizaremos la siguiente notación breve para las instrucciones:
	- $R_T(X)$: La transacción T lee al item X.
	- $W_T(X)$: La transacción T escribe al item X.
	- $b_T$: Comienzo de la transacción T.
	- $c_T$: La transacción T realiza el commit. -> final feliz
	- $a_T$: Se aborta la transacción T(abort). -> final feo

- Un solapamiento entre dos transacciones $T_1 \ y \ T_2$ es una lista de $m(T_1) + m(T_2)$ instrucciones, en donde cada instrucción de $T_1$ y $T_2$ aparece una única vez, y las instrucciones de cada transacción conservan el orden entre ellas dentro del solapamiento.
- Dado un conjunto de transacciones $T_i$, una <span style="color:#ffff00">ejecución serial</span> es aquella en que las transacciones se ejecutan por completo una detrás de otra, en base a algún orden $T_{I_1}, T_{I_2}, ..., T_{I_n}$.
- Dado un conjunto de transacciones $T_i$, es <span style="color:#ffff00">serializable</span> cuando la ejecución de sus instrucciones en dicho orden deja a la DB en un estado equivalente a aquel en que la hubiera dejado alguna ejecución serial $T_{I_1}, T_{I_2}, ..., T_{I_n}$. 