# <span style="color:#c00000">El Kernel</span>

> Corre directamente en el procesador con derechos irrestringidos.
> Cumple el rol de mediador entre los procesos y el hardware.

- Es capaz de performar cualquier operacion disponible en el hardware.

## <span style="color:#c00000">Informacion guardada en el PCB</span> 
- <span style="color:#ffff00">Identificacion del proceso</span>(PID, PID_padre, PGID).
- <span style="color:#ffff00">Datos de estado del proceso</span>: Registros de proposito general de la CPU, SP, Instruction pointer.
- <span style="color:#ffff00">Datos de control del proceso</span>: Estado del proceso y otra informacion de [[Scheduling]], ID de los hijos, datos de IPC(signals y messages), y contadores de tiempo de uso de la CPU.