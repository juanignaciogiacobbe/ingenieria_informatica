# <span style="color:#c00000">Diseño Relacional</span> 

## <span style="color:#c00000">Problemas que se presentan en esquemas defectuosos</span>
- Incapacidad para almacenar ciertos hechos.
- Redundancias -> inconsistencias.
- Ambigüedades.
- Perdida de información y [[Dependencias Funcionales]].
- Existencia de valores nulos.
- Aparición, en la DB, de estados que no son validos en el mundo real.

## <span style="color:#c00000">Criterios de un buen Diseño Relacional</span> 
- <span style="color:#ffff00">"Hechos distintos se deben almacenar en objetos distintos"</span>. 
- Preservación de información.
- Minima redundancia.
- Al partir de un correcto diseño conceptual y se hace un correcto pasaje al modelo lógico, se obtiene un esquema sin redundancia y se preserva toda la información del mundo real que se quería modelar.
- Se formalizan estos requisitos a través de las [[Formas Normales]].

[[Algoritmos de Normalizacion]]
[[Algoritmos de calculo de claves]]