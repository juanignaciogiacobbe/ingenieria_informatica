# <span style="color:#c00000">Sistemas Operativos</span> 

## <span style="color:#c00000">Que es un Sistema Operativo
</span>

> Es la capa de software mas baja, encargada de manejar los recursos de una computadora para sus usuarios y aplicaciones. 
> 
> Debe ser confiable: la <span style="color:#ffff00">proteccion</span> impide que los bugs que aparecen en algún programa corrompa a los demás programas o al mismo SO.
> <span style="color:#ffff00">Seguridad</span>: SO debe limitar a aquellos programas y usuarios que no generan confianza.
> <span style="color:#ffff00">Privacidad</span>: En un sistema multi-user, cada usuario debe ser limitado a ver ciertos datos.


![[Pasted image 20240418195516.png]]

- En sistemas de propósito general, los usuarios interactuan con aplicaciones, las cuales se ejecutan en un ambiente provisto por el SO, y el SO hace de mediador con la capa de hardware.

![[Pasted image 20240418195730.png]]

## <span style="color:#c00000">Roles de un SO</span>

## <span style="color:#c00000">Referee</span>
- Deben ser capaces de manejar los recursos compartidos entre aplicaciones en una misma maquina.
- [[Aislamiento]] de cada aplicación de las demás, de forma tal que un bug en una aplicación no corrompa a las demás aplicaciones que corren en la misma maquina.
- Debe protegerse a si mismo y a las aplicaciones de virus maliciosos.
- Decide cuando y que recursos brindarles a las aplicaciones.
- Resource allocation: Debe mantener todas las actividades corriendo en simultaneo, allocando recursos apropiadamente.

## <span style="color:#c00000">Ilusionista</span>
- Se logra con la [[Virtualizacion]]
- Los SO deben brindar una abstracción(enmascaramiento) del hardware físico para simplificar el diseño de las aplicaciones.
- Nos dan la ilusión de "tener memoria infinita", o de tener todos los procesadores de la maquina enteramente para nosotros.
- Con esta abstracción, los SO permiten invisibilizar las reasignaciones de recursos para las distintas aplicaciones corriendo.
## <span style="color:#c00000">Pegamento</span>
- Los SO proveen un set de servicios comunes para que se puedan compartir recursos de una forma sencilla.
- Proveen una interfaz de rutinas comunes para el usuario, para tener el mismo "look and feel". 


- [[Dual-mode Operation]]
- [[Proceso]]
- [[Kernel]]
- [[Scheduler]]
- [[Concurrencia]]

## <span style="color:#c00000">Trabajos Practicos</span> 
- [[Shell]]