# <span style="color:#c00000">NoSQL</span> 
- En un contexto en el cual las redes son cada vez mas rápidas y el almacenamiento reducía sus [[Costos]], pero con una velocidad de procesamiento estancada -> Se crean nuevos [[DataBase Management System(DBMS)]] que rompían con el paradigma del [[Modelo Logico Relacional]] y por ende con [[SQL]] -> Surge el concepto de NoSQL como todo aquello que no este basado en SQL.
	![[Pasted image 20240521143455.png]]

## <span style="color:#c00000">Clasificación</span> 
- En cada una de ellas cambia la definición de agregado, es decir, de como conjuntos de objetos relacionados se agrupan en colecciones para ser tratados como unidad y ser almacenados en un mismo lugar:
	- Clave-valor.
	- Orientadas a documentos.
	- Wide Column.
	- Basadas en grafos.

## <span style="color:#c00000">Bases de Datos Distribuidas</span> 
- Las DB NoSQL buscan aumentar la velocidad de procesamiento y la capacidad de almacenar información, explotando las ventajas que brindan las redes de computadoras y en particular internet -> Implementan la funcionalidad de un DBMS distribuido.
- Un DBMS distribuido es aquel que corre como sistema distribuido en distintas computadoras(nodos) que se encuentran sobre una red(local o a través de internet, o como un servicio de cloud computing), aprovechando las ventajas de la computación distribuida y brindando a las APPS la abstracción de ser un único sistema coherente.