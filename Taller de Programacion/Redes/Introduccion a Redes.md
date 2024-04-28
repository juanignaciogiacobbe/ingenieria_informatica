# <span style="color:#c00000">Introduccion a Redes</span> 

## <span style="color:#c00000">Sockets</span> 

- Pemiten la comunicacion entre dos procesos diferentes(en la misma maquina o en dos maquinas diferentes).
- Se usan en apps que implementan el <span style="color:#ffff00">modelo cliente-servidor</span>:
	- <span style="color:#ffff00">Cliente</span>: es activo porque inicia la interaccion con el servidor.
	- <span style="color:#ffff00">Servidor</span>: es pasivo porque espera recibir las peticiones de los clientes.
 
## <span style="color:#c00000">Modelo de capas</span> 

![[Pasted image 20240423100926.png]]

## <span style="color:#c00000">Tipos de Conexion</span> 
- <span style="color:#ffff00">Sin conexion</span>: los datos se envian al receptor y no hay control de flujo ni de errores.
- <span style="color:#ffff00">Sin conexion con ACK</span>: por cada dato recibido, el receptor envia un acuse de recibo(ACK).
- <span style="color:#ffff00">Con conexion</span>, se tienen 3 fases: establecimiento de la conexion, intercambio de datos y cierre de la conexion. Hay control de flujo y control de errores.

## <span style="color:#c00000">Modelo OSI</span> 

![[osi_model.png]]

![[osi_vs_tcp9Uug7B.png]]
