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