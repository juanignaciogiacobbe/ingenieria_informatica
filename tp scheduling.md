# TP Scheduling

- se usa JOS -> un exokernel de MIT
- se programa en el lado del kernel. Hay que implementar el context switch. 
- compilacion "condicional" para usar RR o PR.

![[Pasted image 20240427100136.png]]

el heap ta al pedo
no vamos a usar fds -> no hace falta conectarse al file system.
el malloc no esta implementado :(
se le dice cpu a los cores



![[Pasted image 20240427100412.png]]
- trapframe es la clave para hacer el context switch
-  marco de traps -> interrupciones(syscalls)




![[Pasted image 20240427102500.png]]



![[Pasted image 20240427100626.png]]

env_free_list tiene a todos los procesos libres(para esto sirve el campo env_list de los env)

![[Pasted image 20240427102544.png]]

entry es la primera instruccion del kernel(entry.S) -> init
qemu hace el boot inicial y carga el kernel en memoria para que se pueda ejecutar(3 ctes magicas en init.c)


![[Pasted image 20240427213927.png]]


![[Pasted image 20240427214334.png]]