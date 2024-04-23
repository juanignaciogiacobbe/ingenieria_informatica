## <span style="color:#c00000">Multilevel Feedback Queue(MLFQ)</span> 

> Es una extension de RR. En lugar de tener una unica queue, MFQ tiene multiples RR queues, cada una con un diferente nivel de prioridad y con un distinto time quantum.


![[Pasted image 20240421183512.png]]

![[Pasted image 20240421191037.png]]

1. Tiene un numero de queues, cada una con un nivel de prioridad asignado.
2. Un job listo para ejecutarse se encuentra en una unica queue.
3. MLFQ usa las prioridades para decidir que job debe correr en un tiempo determinado.

## <span style="color:#c00000">Reglas a seguir</span> 

1. Si prioridad(A) > Prioridad(B) -> A corre(B no)
2. Si prioridad(A) = Prioridad(B) -> A y B corren en RR.
3. Cuando un job ingresa al sistema, se coloca con la mayor prioridad.
4. Si un job consume todo su time slice durante su ejecucion, se reduce su prioridad.
5. Si un job deja la CPU antes de que termine su time slice, queda en el mismo nivel de prioridad.
6. Luego de un periodo S, se mueven todos los jobs del sistema a la queue mas alta.