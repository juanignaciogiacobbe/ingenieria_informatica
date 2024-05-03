# <span style="color:#c00000">Shell</span> 
- Interprete de comandos -> Dado un array de chars, lo interpreta y construye un comando ejecutable.
- Tiene capacidad de redireccionamiento de flujo estándar y soporta concatenación de comandos.

## <span style="color:#c00000">Ejecución de la shell</span>
1. Un proceso principal se forkea, y se realiza un exec del comando enviado.

![[Pasted image 20240502082015.png]]





![[Pasted image 20240502082125.png]]


## <span style="color:#c00000">Invocación de comandos</span> 
- Los comandos que mas se utilizan están guardados en el directorio /bin. 
- Existe una variable de entorno llamada $PATH, en la cual se declaran las rutas mas usualmente accedidas por el SO.
- Es deseable, la funcionalidad de poder pasarle _argumentos_ al momento de querer ejecutar dichos comandos. Los argumentos pasados al programa de esta forma, se guardan en la famosa variable `**char* argv[]**`, junto con cuántos fueron en `**int argc**`, declaradas en la función `main` de cualquier programa en _C_.
- `getline()` delimita por el salto de linea(se toma como un ENTER).

	![[Pasted image 20240502084837.png]]

## <span style="color:#c00000">Redirecciones</span> 

### <span style="color:#c00000">Redirecciones de flujo estándar</span>
- Permite almacenar la salida de un programa en un archivo de texto para luego poder analizarla, como así también ejecutar un programa enviándole un archivo como entrada estándar. Hay 3 formas de redireccion del flujo estándar:
	- <span style="color:#ffff00">Entrada y salida estándares a archivos</span>(`<in.txt >out.txt`): Son los operadores clásicos del manejo de la redireccion del stdin y el stdout en archivos de entrada y salida respectivamente.  
	- <span style="color:#ffff00">Error estándar a archivo</span>(`2>err.txt`): Es una de las dos formas de redireccionar el flujo estándar de error análogo al caso anterior del flujo de salida estándar en un archivo de texto.
	- <span style="color:#ffff00">Combinar salida y errores</span>(`2>&1`): Se redirecciona el flujo estándar por errores hacia donde apunta la salida.
	![[Pasted image 20240502084947.png]]

- Utilizamos `dup2`, la cual nos permite redireccionar el flujo estándar.
	![[Pasted image 20240502085123.png]]
### <span style="color:#c00000">Pipes</span>
- Permite redireccionar la salida de un programa hacia otros programas. Se hace mediante el pipe `|`.
- Se pueden concatenar dos o mas programas para que la salida estándar de uno de redirija a la entrada estándar del siguiente.
- Shell soporta pipes entre dos comandos(pipes simples), y la ejecución de n comandos concatenados(pipes multiples).

	![[Pasted image 20240502085201.png]]

	![[Pasted image 20240502085227.png]]

## <span style="color:#c00000">Variables de Entorno</span> 
- Para ver la lista completa de variables de entorno definidas: env.
- La shell tiene la capacidad de expandir variables de entorno.
- Las env se indican con el `$` antes del nombre -> la shell se encarga de reemplazar en la linea leída todos los tokens que comiencen por `$` por los valores correspondientes del entorno. <span style="color:#ffff00">Esto ocurre antes de que el proceso sea ejecutado</span>.
- Las variables vacías/no seteadas no deben traducirse a argumentos en la etapa exec.

	![[Pasted image 20240502085321.png]]
### <span style="color:#c00000">Variables de entorno temporarias</span> 
- Se soporta la incorporación de nuevas variables a la ejecución de un programa. Se incorporan de forma dinámica.
	![[Pasted image 20240502085344.png]]

### <span style="color:#c00000">Pseudo-variables</span> 
- Son propias de la shell, y cambian su valor dinamicamente a lo largo de su ejecución.


## <span style="color:#c00000">Comandos Built-in</span> 
- Nos permiten realizar acciones que no siempre podríamos hacer si ejecutáramos ese mismo comando en un proceso separado. Éstos son propios de cada _shell_ aunque existe un estándar generalizado entre los diferentes intérpretes, como por ejemplo `cd` y `exit`.

## <span style="color:#c00000">Procesos en segundo plano</span> 
- Son muy útiles a la hora de ejecutar comandos que no queremos esperar a que terminen, para que la shell nos devuelva el prompt adecuadamente.
- La shell deberá esperar oportunamente a los procesos en background. Esto puede hacerse sincrónicamente antes de mostrar cada _prompt_, con el objetivo de que en una ejecución normal _no se dejen procesos huérfanos_.
- Se quiere que el manejo y liberación de recursos del proceso ocurra en el mismo momento que termina. Para lograr esto, se utiliza el manejo de señales(en este caso, queremos atrapar a `SIGCHLD`) la cual se genera cada vez que un proceso hijo termina.
- El SO nos da la posibilidad de poder ejecutar lógica _custom_ para cada señal que se precise manejar de manera particular. Con la _syscall_ `sigaction(2)` vamos a poder configurar lo que se denomina **handler** (a.k.a una _función_) para dicha señal y liberar los recursos del proceso en _segundo plano_ que haya finalizado.
- La solución más fácil es asegurarse de que todos los procesos en _segundo plano_ tengan un mismo _process group_. Y que la llamada a `waitpid(2)` en el _handler_ no use -1 como argumento (es decir, esperar por _cualquier proceso_), sino un valor numérico que restrinja la llamada a los procesos en segundo plano.