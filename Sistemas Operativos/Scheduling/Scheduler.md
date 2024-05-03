# <span style="color:#c00000">Scheduling</span> 

> Es un mecanismo que le permite al SO determinar cuanto tiempo de CPU le toca a cada [[proceso]](también llamados *jobs*).
> Los schedulers modernos son <span style="color:#ffff00">preventivos</span>: son capaces de parar un proceso en ejecución para correr otro. Es decir, puede realizar un context switch, parando temporalmente un proceso en ejecución y resumir(o comenzar) la ejecución de otro.

## <span style="color:#c00000">Scheduling Metrics</span> 

- <span style="color:#ffff00">Turnaround Time</span>: es el tiempo que tarda en completarse un job menos el tiempo en el cual arriba al sistema. Es una métrica de performance.
	$T_{turnaround} = T_{completion} - T_{arrival}$
	
- <span style="color:#ffff00">Response time</span>: Es el tiempo desde que llega un job a un sistema hasta que es scheduled.
	$T_{response} = T_{firstrun} - T_{arrival}$

[[Uniprocessor Scheduling]]
[[Multi-level Feedback Queue]]


