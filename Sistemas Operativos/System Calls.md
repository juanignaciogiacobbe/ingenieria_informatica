# <span style="color:#c00000">System Calls</span>

> Es un procedimiento brindado por el kernel que puede ser llamado desde el user level.
> Es cualquier función que el kernel expone, y que puede ser utilizada a nivel usuario.
> Es un punto de entrada controlado al kernel.

![[Pasted image 20240427183833.png]]

- Proveen la ilusión de que el kernel del SO es simplemente una librería de rutinas disponibles para los programas de usuario.
- Al cambiar de user a kernel mode, la CPU podrá acceder al area protegida del kernel.
- El conjunto de syscalls es fijo, y cada una es identificada por un único numero(invisible al programa).
- Cada syscall debe tener un conjunto de parámetros que especifican información que debe ser transferida desde el user space al kernel space.


## <span style="color:#c00000">Llamando a una syscall</span>
1. El programa llama a una syscall mediante la invocación de una función wrapper en la biblioteca de C(este wrapper brinda todos los argumentos a la syscall trap_handling).
2. El wrapper copia el numero de la syscall a un determinado registro de la CPU.
3. Wrapper ejecuta una instrucción de código llamada trap machine instruction, que causa que el procesador pase de user a kernel mode.
	![[Pasted image 20240427184802.png]]

## <span style="color:#c00000">API de Syscalls</span>

![[Pasted image 20240427184117.png]]
![[Pasted image 20240427184132.png]]