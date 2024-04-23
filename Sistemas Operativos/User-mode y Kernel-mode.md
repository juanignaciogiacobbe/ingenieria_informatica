# <span style="color:#c00000">User-Mode y Kernel-Mode</span>
 
 - <span style="color:#ffff00">Instrucciones privilegiadas</span>: disponibles solamente en kernel-mode.

## <span style="color:#c00000">User a Kernel Mode</span>

- <span style="color:#ffff00">Interrupts</span>: Señales asincrones que se envian al procesador para avisarle que cierto evento ocurrio y que requiere su atencion. El procesador esta constantemente alerta de estas señales.
- <span style="color:#ffff00">Processor Exceptions</span>: Es un evento de hardware causado por un user program, que causa la transferencia de control al kernel.
- [[System Calls]]

## <span style="color:#c00000">Kernel a User mode</span>

- Nuevo proceso: Para comenzar un nuevo proceso, el kernel copia el programa en memoria, setea el PC a la primera instruccion del proceso, setea el SP a la base del stack de usuario, y cambia a user mode.
- Retomar luego de un interrupt, un processor exception o una syscall.
- Cambiando a un proceso diferente.
- User-level upcall.