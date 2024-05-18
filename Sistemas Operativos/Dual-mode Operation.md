# <span style="color:#c00000">Dual-Mode Operation</span>
- Es un mecanismo para evitar la ejecución directa.
- Tenemos un bit en el status register que nos indica el modo actual del procesador -> 0 para kernel mode(sin restricciones) y 3 para user mode.

![[Pasted image 20240418203842.png]]

# <span style="color:#c00000">User-Mode y Kernel-Mode</span>
 
 - En user-mode, se ejecutan instrucciones en nombre del usuario.
 - En kernel-mode, se ejecutan instrucciones en nombre del [[Kernel]] del SO de <span style="color:#ffff00">forma privilegiada</span>(protege la memoria, los puertos de I/O y la posibilidad de ejecutar ciertas instrucciones).
	 ![[Pasted image 20240506133433.png]]
	 
 - <span style="color:#ffff00">Modo dual</span>: Permite que los distintos modos posean cada uno su propio set de instrucciones.
 - Para diferenciar estos dos modos operacionales, se utiliza un bit en el registro de control del procesador, que permite diferenciar entre tipos de instrucciones(privilegiadas vs no privilegiadas). Le indica al procesador si la instrucción ejecutada puede ser o no ejecutada dependiendo del modo en que se encuentre el mismo.
 - <span style="color:#ffff00">El SO y los programas viven en memoria al mismo tiempo</span>, y el SO debe poder configurar el hardware de forma tal que cada proceso pueda leer y escribir su propia porción de memoria.
 - En las arquitecturas de x86 se tienen 4 modos de operaciones vía el hardware. Van del 0 a 3 y se denominan rings, siendo el ring 0 el nivel mas privilegiado (el del kernel - modo supervisor o modo kernel) y el 3 el menos (el de las aplicaciones - modo usuario). La diferencia entre modos esta en un bit en el registro de control del procesador.
 
	![[Pasted image 20240427181302.png]]

## <span style="color:#c00000">Instrucciones privilegiadas</span>
- Disponibles en kernel-mode pero NO en user-mode.
- El kernel del SO necesita poder ejecutar estas instrucciones para poder hacer su trabajo -> para cambiar su nivel de privilegios, ajustar el acceso a memoria, deshabilitar y habilitar interrupciones.
- El aislamiento de procesos es posible solo si hay una forma de limitar la ejecución de los programas en user mode directamente cambiando su nivel de privilegio. Si no es transfiriendo el control al kernel del SO, un proceso no puede cambiar su nivel de privilegio.
- Los procesos pueden cambiar indirectamente su nivel de privilegio ejecutando instrucciones especiales llamadas [[System Calls]], para transferir el control al kernel en una ubicacion especial definida por el SO.
- <span style="color:#ffff00">Un proceso de aplicación NO tiene permitido cambiar su nivel de privilegio</span>, ni tampoco tiene permitido cambiar el set de memoria al que puede acceder y NO puede deshabilitar las interrupciones del procesador.
- Cuando una aplicación trata de acceder a memoria a la que no debería tener acceso para cambiar su nivel de privilegio, se produce una excepción del procesador. Dicha excepción causa que el procesador le transfiera el control al <span style="color:#ffff00">Exception Handler del kernel.</span>

## <span style="color:#c00000">Proteccion de memoria</span>
- Para ejecutar un proceso, el SO y la aplicación deben residir en memoria al mismo tiempo. La aplicación debe estar para ejecutarse, mientras que el SO debe estar para arrancar el programa y controlar si aparece algún interrupt, processor exceptions o system calls mientras el programa corre.
- Podríamos tener varios procesos en memoria, y que quieran compartir la memoria de forma segura, por lo que el SO debe configurar el hardware de forma tal que cada proceso pueda leer y escribir solo su propia memoria. Para ello el hardware provee un mecanismo de protección de memoria.
- El SO debe ser capaz de configurar el hardware de forma tal que cada aplicación pueda leer y escribir su propia memoria, y no la memoria del SO o de otra aplicación.

## <span style="color:#c00000">User a Kernel Mode</span>
Los procesos de usuario puede transicionar al Kernel de forma voluntaria, a través de las [[System Calls]].
### <span style="color:#c00000">Exceptions</span>
- Es una condición inesperada causada por el comportamiento de un programa de usuario. El hardware va a parar de ejecutar el proceso actual y empezar a correr un Manejador de Excepciones especialmente diseñado en el Kernel.
- Pueden hacer que el SO detenga el proceso y devuelva un código de error al usuario, o puede hacer que el Kernel le de el poder a otro proceso de ser ejecutado.
- Algunas causas de arrojo de exceptions:
	- Acceder fuera de la memoria del proceso.
	- Intentar ejecutar una instrucción privilegiada en modo user.
	- Dividir por 0.

### <span style="color:#c00000">Interrupts</span>
- Es una señal asíncrona enviada al procesador indicándole que ocurrió un evento externo que requiere de su atención. El procesador detiene entonces el proceso que esta actualmente ejecutándose y empieza a correr el Manejador de Excepciones en el Kernel.
- Son usadas para informar al Kernel que se ha completado una request de los I/O.
- Una alternativa a ellas es el polling, que es el chequeo en loop por parte del Kernel de cada dispositivo I/O para ver si ocurrió algún evento que requiera de manejo. Cuando se esta haciendo polling, no se puede correr código a nivel de usuario.
- Otra fuente de interrupciones son las interrupciones inter-procesador -> Cuando existen multiples procesadores, uno de ellos puede causar una interrupción en cualquiera de los otros. El Kernel usa estas interrupciones para coordinar acciones a través del multiprocesador.
- En el caso de que se haya producido una interrupción, no sólo se accederá a la tabla de interrupciones para obtener un handler sino también se guardará el estado del proceso interrumpido en el `Stack de Interrupciones`, antes de llamar al handler.
- Este `stack de interrupciones` está separado del stack del kernel. Y si el kernel está corriendo en un sistema multiprocesador, cada procesador tiene su propio stack de interrupciones en el kernel para que se puedan manejar múltiples traps y excepciones a través de los múltiples procesadores.


## <span style="color:#c00000">Kernel a User mode</span>
### <span style="color:#c00000">Nuevo Proceso</span>
- El Kernel copia el programa a memoria, setea el PC para ser la primera instrucción del proceso, setea el SP para ser la base del user stack y cambia a user mode.

### <span style="color:#c00000">Reanudar luego de una exception, interrupt o syscall</span>
- Cuando el Kernel termina de manejar la request, reanuda la ejecución del proceso interrumpido, restaurando su PC y sus registros, y cambiando de nuevo a user mode.

### <span style="color:#c00000">Cambiar a otro proceso diferente</span>
- En algunos casos, el Kernel puede decidir cambiar a otro proceso diferente al que estaba ejecutando antes de la interrupción, exception o syscall. Y como el kernel eventualmente quiere reanudar el proceso viejo, necesita cambiar el estado del proceso en el `control block` del proceso.

### <span style="color:#c00000">Llamada ascendente en User Level</span>
- Muchos SO proveen a los users la habilidad de recibir de forma asíncrona notificaciones de eventos. Este mecanismo es muy similar al manejo de interrupciones del Kernel, excepto que es a nivel de usuario.


## <span style="color:#c00000">Context Switch</span> 
- Para asegurarnos que ningún programa malicioso pueda corromper al kernel cuando transicionamos de usuario a kernel, necesitamos que el procesador guarde su estado y switchee lo que está haciendo, todo mientras continúa ejecutando instrucciones que pueden llegar a alterar el estado de lo que sea que esté en proceso de guardado.
- Un cambio de contexto implica congelar el estado del CPU y reemplazarlo por otro. Además, puede llegar a ocurrir un cambio de privilegio. El cambio de contexto requiere soporte del hardware: de user a kernel (gana prioridad), y de kernel a user (pierde prioridad)