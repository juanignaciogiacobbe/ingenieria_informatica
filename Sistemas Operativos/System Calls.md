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


## <span style="color:#c00000">Fork()</span> 
- Utilizada para crear un proceso nuevo.
- PID(process ID): en UNIX es el identificador del proceso, y nos permite llamar a un proceso para hacer algo con el.
- El proceso creado es casi una copia exacta del proceso padre.
- El proceso hijo comienza a ejecutarse desde que se llama a `fork()`.
- El hijo tiene su propia copia del address space, sus propios registros, su propio PC. Retorna para `fork()` un valor distinto que el padre(retorna 0).
- El output de los programas no es deterministico. Al tener dos procesos activos corriendo en el sistema, y asumiendo que contamos con un único CPU, nos trae la necesidad de tener un [[Scheduler]], el cual va a determinar que proceso corre en un momento determinado.

## <span style="color:#c00000">Wait()</span> 
- Nos permite que por ejemplo un proceso padre espere a que el proceso hijo termine.
- Permite que nuestro output sea deterministico, ya que podemos controlar de cierta forma el flujo de ejecución de los procesos.

	![[Pasted image 20240503175259.png]]
	![[Pasted image 20240503175314.png]]

## <span style="color:#c00000">Exec()</span> 
- Es util cuando queremos correr un programa que es diferente al programa invocador.`fork()` es util cuando queremos correr copias de un mismo programa, sin embargo, para correr un programa distinto, vamos a utilizar `exec()`.
- Dado el nombre de un ejecutable y algunos argumentos, carga el código y data estática de ese ejecutable y sobreescribe su actual code segment con el(se reinicia el heap y el stack). El SO corre ese programa.
- No crea un proceso nuevo, sino que transforma el programa que se esta corriendo en un programa distinto.
	![[Pasted image 20240503175549.png]]