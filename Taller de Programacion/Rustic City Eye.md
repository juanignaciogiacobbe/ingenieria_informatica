# Rustic City Eye(to-do)


## Entrega intermedia

- Servicio de mensajeria 
- implementacion de MQTT
- App de monitoreo
- Sistema central de camaras
- Interfaz grafica incompleta

![[Pasted image 20240425075818.png]]

![[Pasted image 20240425075842.png]]

# Servicio de Mensajeria
- pub/sub, arquitectura cliente server(done)
- MQTT

# MQTT

- El broker deberia filtrar y distribuir los mensajes.
- CLIENTE: TODOS SON PUBLISHERS Y SUSCRIBERS
- Un cliente es un user que se conecta al broker.

## Conexion 
- Cliente: connect
- broker: connack
- ![[Pasted image 20240425075246.png]]
![[Pasted image 20240425075255.png]]


![[Pasted image 20240425075314.png]]


![[Pasted image 20240425075336.png]]

![[Pasted image 20240425075341.png]]


## PUBLISH y SUSCRIBE
- Primero habria que armar el arbol de topicos



clean start flag -> determina si quiere cargar una sesion vieja o no
will flag -> indica si se quiere enviar un will message -> si vale 1 debo tener willl props, topic y payload.
will qos -> indica la qos con la que se va a publicar el qos
will retain -> indica si se quiere retener el mensaje cuando es publicado
usernama flag -> indica si se quiere poner un username
password -> indica si se quiere poner una password

keep alive -> intervalo de tiempo medido en segundos


properties
session expiy
receive maximum
maximum packet size
topic alias maximum
request response info
request problem info
user property
auth method
auth data


payload
clientid
will properties -> si y solo si el will flag es 1:
	will delay interval
	payload format indicator
	message expiry interval
	content type
	response topic
	correlation data
	user prop

will topic -> si y solo si el will flag es 1
will payload -> si y solo si el will flag es 1
username si y solo si el username flag es 1
password -> si y solo si el password flag es 1
