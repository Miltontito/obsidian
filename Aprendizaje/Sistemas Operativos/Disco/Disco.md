Sector -> elemento fisico del disco.
Bloque -> elemento logico del disco.

![[Pasted image 20251015191133.png]]

**Tiempo de posicionamiento** (Seek Time) -> Tiempo que le toma al dispositivo llegar a la pista que se pide.

**Retardo rotacional** -> Tiempo que le toma al sector deseado comenzar a pasar por el mecanismo de Lectura/escritura

**Tiempo de transferencia** -> Tiempo que tardo en leer los sectores.

**Tiempo de Acceso Total** -> Tiempo de posicionamiento + Retardo Rotacional + Tiempo de Transferencia.  

**Tiempo de acceso** -> Tiempo de posicionamiento + retardo rotacional.

# Politicas de administración
---
Fifo: Se procesan los requerimientos en el orden de arribo, justa para los procesos, se aproxima a la seleccion al azar cuando el número de procesos es elevado

Prioridad: El objetivo no es optimizar el uso del disco, los trabajos batch cortos pueden tener mayor prioridad, provee buen tiempo de respuesta.

LIFO: Existe posibilidad de inanicion, es buena para procesmiento de transacciones.

SSTF: selecciona el requerimiento de i/o que requiere el menor movimiento del mecanismo de acceso desde la posición actual.

SCAN: el mecanismo se mueve en una dirección satisfaciendo todos los requerimientos que encuentra en el camino hasta que alcanza la ultima pista en esa dirección, luego la dirección es revertida.

Parece la opcion perfecta, pero en su trabajo se pueden colar requerimientos haciendo que los que estaban siguientes se retrasen,

C-SCAN: restringe el scan a una unica direccion, cuando se alcanza la ultima pista en la direccion de scaneo el mecanismo es deuelto a la primera pista y el proceso comeinza nuevamente.

LOOK: igual que scan pero no llega a los extremos del disco si no lo necesita.

F-SCAN: dos colas, una cola esta vacia y recibe los nuevos requerimientos.

N-STEP SCAN: segmenta los requerimientos en colas de longitud N, procesa los requerimientos en una cola utilizando SCAN, los nuevos requerimientos que surgen mientras se esta procesando una cola se agregan a otra cola.

# Raid
---
