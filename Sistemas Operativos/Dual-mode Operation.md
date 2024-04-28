# <span style="color:#c00000">Dual-Mode Operation</span>
- Es un mecanismo para evitar la ejecución directa.

![[Pasted image 20240418203842.png]]

# <span style="color:#c00000">User-Mode y Kernel-Mode</span>
 
 - En user-mode, se ejecutan instrucciones en nombre del usuario.
 - En kernel-mode, se ejecutan instrucciones en nombre del [[Kernel]] del SO de <span style="color:#ffff00">forma privilegiada</span>(protege la memoria, los puertos de I/O y la posibilidad de ejecutar ciertas instrucciones).
 - <span style="color:#ffff00">Modo dual</span>: Permite que los distintos modos posean cada uno su propio set de instrucciones.
 - Para diferenciar estos dos modos operacionales, se utiliza un bit en el registro de control del procesador, que permite diferenciar entre tipos de instrucciones(privilegiadas vs no privilegiadas).
 - El SO y los programas viven en memoria al mismo tiempo, y el SO debe poder configurar el hardware de forma tal que cada proceso pueda leer y escribir su propia porción de memoria.


![[Pasted image 20240427181302.png]]

## <span style="color:#c00000">User a Kernel Mode</span>

- <span style="color:#ffff00">Interrupts</span>: Señales asíncronas que se envían al procesador para avisarle que cierto evento ocurrió y que requiere su atención. El procesador esta constantemente alerta de estas señales. Permiten que periódicamente el kernel pueda tomar control de la computadora, desalojando al proceso de usuario en ejecución y poder tomar control del procesador(el hardware counter funciona de cuenta regresiva para pasar a kernel mode).
- <span style="color:#ffff00">Processor Exceptions</span>: Es un evento de hardware causado por un user program, que causa la transferencia de control al kernel. Algunas causas de arrojo de exceptions:
	- Acceder fuera de la memoria del proceso.
	- Intentar ejecutar una instrucción privilegiada en modo user.
	- Dividir por 0.
- [[System Calls]]

## <span style="color:#c00000">Kernel a User mode</span>

- <span style="color:#ffff00">Nuevo proceso</span>: Para comenzar un nuevo proceso, el kernel copia el programa en memoria, setea el PC a la primera instrucción del proceso, setea el SP a la base del stack de usuario, y cambia a user mode.
- Retomar luego de un interrupt, un processor exception o una syscall.
- Cambiando a un proceso diferente.
- User-level up call.