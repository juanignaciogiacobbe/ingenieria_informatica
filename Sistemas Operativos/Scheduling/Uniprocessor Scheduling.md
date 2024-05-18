# <span style="color:#c00000">Uniprocessor Scheduling</span> 

## <span style="color:#c00000">First-in-First-out (FIFO)</span> 

> **Hace todas las tareas por orden de llegada**. Al comenzar a trabajar en una tarea, seguimos trabajando en ella hasta que termine. Solo va a cambiar de tarea a medida que va completándolas.
> También se llama First Come, First Served.

![[Pasted image 20240515122817.png]]

- <span style="color:#ffff00">Al aparecer jobs que tengan distintos tiempos para completarse, el sistema da la impresión de ineficiencia</span>(El turnaround time en promedio se hace muy alto). -> Se produce un <span style="color:#ffff00">Convoy effect</span>: literalmente es el camión que te tapa el paso cuando vas a la costa.

![[Pasted image 20240421182113.png]]

## <span style="color:#c00000">Shortest Job First(SJF)</span> 

> Primero ejecutamos aquellos jobs que tengan el menor tiempo para terminar. Con esto, reducimos el turnaround promedio.

![[Pasted image 20240515123003.png]]

- Puede pasar que, al tener muchos jobs cortos, los mismos jobs largos pueden nunca completarse(literalmente se le cuelan siempre los jobs cortos).

![[Pasted image 20240421182629.png]]

## <span style="color:#c00000">Shortest Time-to-Completion(STCF)</span>
![[Pasted image 20240515123342.png]]

## <span style="color:#c00000">Round Robin(RR)</span> 

> Los jobs que se tienen que ejecutar corren en el procesador por un tiempo determinado. El scheduler asigna al procesador el primer job para ejecutar, seteando también un timer interrupt para pasar a otro job(esto se llama <span style="color:#ffff00">time quantum o time slice</span>). Al final del quantum, si la tarea no se ha completado, la tarea se adelanta y el procesador pasa a la siguiente tarea de la lista de tareas listas.

![[Pasted image 20240517091220.png]]
- El time slice debe amortizar el cambio de contexto sin hacer que esto resulte en que el sistema no responda mas.

![[Pasted image 20240421183102.png]]


El time slice es crucial para RR, debido a que, a medida que vayamos reduciéndolo, vamos a tener mejor performance si nos basamos en la métrica del response-time. Pero al reducirlo tanto, el costo del context switch va a hacer que nuestra performance se caiga.
La clave esta en determinar un time slice que amortice el costo del context switch, y que no perdamos esa performance.