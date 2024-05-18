## <span style="color:#c00000">Multilevel Feedback Queue(MLFQ)</span> 

> Es una extension de RR. En lugar de tener una única queue, MLFQ tiene multiples RR queues, cada una con un diferente nivel de prioridad y con un distinto time quantum.
> Intenta optimizar el $T_{around}$, que se realiza mediante la ejecución de la tarea mas corta primero.(A priori el SO no sabe cuanto va a tardar en correr una tarea).
> Intenta que el scheduler haga sentir al sistema con un tiempo de respuesta interactivo para los usuarios, por ende minimizar el response time.
> Round Robin reduce el response time pero tenia un mal turnaround time.


![[Pasted image 20240421183512.png]]

![[Pasted image 20240421191037.png]]
- Si una determinada tarea repetidamente no utiliza la CPU mientras espera que un dato sea ingresado por el teclado, MLFQ va a mantener su prioridad alta, así es como un proceso interactivo debería comportarse.
- Si una tarea usa intensivamente por largos periodos de tiempo la CPU, MLFQ reducirá su prioridad. De esta forma MLFQ va a aprender mientras los procesos se ejecutan y entonces va a usar la historia de esa tarea para predecir su futuro comportamiento.

1. Tiene un numero de queues, cada una con un nivel de prioridad asignado.
2. Un job listo para ejecutarse se encuentra en una única queue.
3. MLFQ usa las prioridades para decidir que job debe correr en un tiempo determinado.
4. La tarea con mayor prioridad(la primera en la cola mas alta) sera elegida para ser corrida.
5. La clave esta en como el scheduler setea las prioridades. En vez de dar una prioridad fija a cada tarea, MLFQ varia la prioridad de la tarea basándose en su comportamiento observado.

## <span style="color:#c00000">Reglas a seguir</span> 

1. Si prioridad(A) > Prioridad(B) -> A corre(B no)
2. Si prioridad(A) = Prioridad(B) -> A y B corren en RR.
3. Cuando un job ingresa al sistema, se coloca con la mayor prioridad.
4. Si un job consume todo su time slice durante su ejecución, se reduce su prioridad.
5. Si un job deja la CPU antes de que termine su time slice, queda en el mismo nivel de prioridad.
6. Luego de un periodo S, se mueven todos los jobs del sistema a la queue mas alta.