# <span style="color:#c00000">Scheduling</span> 

> Es un mecanismo que le permite al SO determinar cuanto tiempo de CPU le toca a cada [[proceso]](también llamados *jobs*).
> Los schedulers modernos son <span style="color:#ffff00">preventivos</span>: son capaces de parar un proceso en ejecución para correr otro. Es decir, puede realizar un context switch, parando temporalmente un proceso en ejecución y resumir(o comenzar) la ejecución de otro.


## <span style="color:#c00000">Numeros y Workload</span>
- <span style="color:#ffff00">Scheduling overhead</span>: El tiempo que tardo en switchear de job.
- <span style="color:#ffff00">Starvation</span>: La falta de progreso de una tarea, debido a los recursos asignados a una tarea de mayor prioridad.
- <span style="color:#ffff00">Workload</span>: es la carga de un proceso corriendo en el sistema. -> Su calculo es fundamental para determinar partes de las políticas de planificación. Cuanto mejor es el calculo, mejor es la política. 
- Básicamente, define el input para un algoritmo de Scheduling.
- Suposiciones para calcularlo:
	1.  Cada job se ejecuta la misma cantidad de tiempo.
	2. Todos los jobs llegan al mismo tiempo para ser ejecutados.
	3. Una vez que empieza un job sigue hasta completarse.
	4. Todos los jobs utilizan únicamente CPU.
	5. El run-time de cada job es conocido.
## <span style="color:#c00000">Scheduling Metrics</span> 
- Estas métricas estandarizadas nos permiten comparar las distintas políticas de scheduling.
- <span style="color:#ffff00">Turnaround Time</span>: es el tiempo que tarda en completarse un job menos el tiempo en el cual arriba al sistema. Es una métrica de performance.
	$T_{turnaround} = T_{completion} - T_{arrival}$
	- Debido a la regla 2, $T_{arrival} = 0$.
	
- <span style="color:#ffff00">Response time</span>: Es el tiempo desde que llega un job a un sistema hasta que es scheduled. Surge con el advenimiento del time-sharing ya que los usuarios se sientan en una terminal de una computadora y pretenden una interacción con rapidez.
	$T_{response} = T_{firstrun} - T_{arrival}$

	![[Pasted image 20240517090816.png]]


## <span style="color:#c00000">Politicas para Sistemas Mono-Procesador</span>
[[Uniprocessor Scheduling]]
[[Multi-level Feedback Queue]]


