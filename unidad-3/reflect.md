# Unidad 3


## 🤔 Fase: Reflect


### Actividad 8

En tu bitácora, sin consultar tu código, diagramas o notas, responde a las siguientes preguntas con us propias palabras. Concéntrate en el esfuerzo de recordar, no en la perfección de la respuesta.

Parte 1: recuperación de conocimiento (Retrieval Practice)

Describe con tus palabras qué es una máquina de estados. 

R/ Una maquina de estados se divide en los diferentes comportamientos principales que va a tener un programa, donde cada uno de esos estados tiene diferentes eventos que cambiaran el estado dependiendo de lo que se busque desarrollar en el programa.


¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?

R/ Los eventos, las acciones, el inicializador y los vectores de prueba

Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender varios eventos y tareas “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit o en p5.js. 

R/ Porque asi puedes generar varios eventos al tiempo sin la necesidad de dañar la concurrencia del programa y puedes identificar mejor fallos con los vectores de prueba.

¿Qué problema soluciona en comparación con usar funciones como sleep()?

R/ Que no tiene la necesidad de poner en alto todo el programa, sino que puedes cambiar de estados mientras el programa sigue su concurrencia normal.

Imagina que tienes que añadir una nueva funcionalidad a la bomba: si se recibe un evento especial (por ejemplo, una combinación de botones o un comando serial) mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

R/

Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.



Parte 2: reflexión sobre tu proceso (Metacognición)

¿Qué parte del diseño de la bomba te resultó más desafiante: crear el diagrama de estados o traducir ese diagrama a código? ¿Por qué?
Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?
El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?
Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?
