# <span style="color:#c00000">Threads</span> 

> Un thread es una unidad de ejecucion que vive dentro de un proceso.

- Un proceso con varios threads es un <span style="color:#ffff00">proceso multithread</span>.
- Los threads que viven dentro de un proceso <span style="color:#ffff00">se ejecutan de forma concurrente</span> y comparten contexto entre si.
- Un thread <span style="color:#ffff00">es similar a un proceso pero con una menor carga de contexto propio</span>.
- Comparten recursos de un mismo proceso, entre ellos el espacio de memoria. Cada uno mantiene su propia informacion de estado(stack, PC, registros).

![[Pasted image 20240423091057.png]]