# <span style="color:#c00000">Virtualizacion</span>
> Tomo un recurso físico(como la memoria o el procesador), y lo transformo en una forma virtual mas general, poderosa y fácil de usar.
> <span style="color:#ffff00">Le provee a una aplicación lla ilusión de que tiene una cantidad de recursos que, físicamente, no son reales o mejor dicho, no están disponibles</span>. 
> El SO puede presentar a cada aplicación la abstracción de que tiene un procesador enteramente dedicado a ella, aunque a un nivel físico puede haber en realidad un sólo procesador compartido entre todas las aplicaciones que están corriendo.
> La mayoría de recursos físicos pueden ser virtualizados.

## <span style="color:#c00000">Virtualizacion de Memoria</span>
-  <span style="color:#ffff00">El SO le hace creer al proceso que este tiene toda la memoria disponible para ser reservada</span> y usada como si este estuviera siendo ejecutado solo en la computadora.
- Los procesos se dividen en 4 segmentos: instrucciones del programa, variables globales, heap y stack. Todos estos segmentos pertenecientes a un proceso se denomina [[Address Space]] del proceso.

	![[Pasted image 20240418203152.png]]
### <span style="color:#c00000">Objetivos</span> 
- <span style="color:#ffff00">Transparencia</span>: El SO debería implementar la memoria virtual de modo que sea invisible para los programas en ejecución(se comportan como si tuvieran su propia memoria física dedicada).
- <span style="color:#ffff00">Eficiencia</span>: El SO debería asegurarse de manejar una virtualizacion lo mas eficientemente posible en términos de tiempo y espacio.
- <span style="color:#ffff00">Protección</span>: Se debería asegurar de proteger a los procesos de los demás. No se debería afectar la memoria de procesos ajenos.

## <span style="color:#c00000">Virtualizacion del Procesador</span> 
- Consiste en dar una ilusión de la existencia de un único procesador para cualquier programa que requiera su uso.
- Nos provee simplicidad en la programación(cada proceso cree que tiene toda la CPU, que todos los dispositivos le pertenecen, y que estos dispositivos tienen el mismo nivel de interfaces), y aislamiento frente a fallas(los procesos no afectan directamente a los demás, y no colapsan la maquina).

	![[Pasted image 20240506134936.png]]