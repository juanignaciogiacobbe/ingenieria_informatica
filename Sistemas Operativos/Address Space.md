# <span style="color:#c00000">Address Space</span> 
- Es la abstracción "easy-to-use" de la memoria física que nos provee el SO.
- Contiene todo el memory state de el programa en ejecución(code, stack y heap). 

	![[Pasted image 20240503181002.png]]
	- El tamaño de code es estático(no va a necesitar mas memoria de la que tiene al iniciarse), por lo que lo podemos poner al inicio del address space por ejemplo.
	- El heap y el stack crecen en direcciones opuestas.
	- El programa no necesariamente esta en la dirección 0 de la memoria física(esta cargado en alguna dirección arbitraria).

> El SO esta virtualizando la memoria, debido a que el programa que se esta corriendo cree que esta cargado en una posición especifica de memoria(por ejemplo, en la posición 0), y que tiene toda la memoria para el(cuando obviamente no es así).
> Al aislar la memoria de los procesos, el SO se asegura que los programas en ejecución no afecten la operación del mismo SO.

- Transparencia: el SO debería implementar la memoria virtual de modo que sea invisible para los programas en ejecución(se comportan como si tuvieran su propia memoria física dedicada).
- Eficiencia: el SO debería asegurarse de manejar una virtualizacion lo mas eficientemente posible en términos de tiempo y espacio.
- Protección: se debería asegurar de proteger a los procesos de los demás. No se debería afectar la memoria de procesos ajenos.

## <span style="color:#c00000">Mecanismos de Virtualizacion</span> 
### <span style="color:#c00000">Address Translation</span> 
- Hardware-based address translation.
- El hardware transforma cada acceso de memoria, cambiando el virtual address dado por la instrucción a una physical address donde la información deseada esta guardada.
- Un address translation se realiza por hardware para redireccionar app memory references hacia su locación real en memoria.