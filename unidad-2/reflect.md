# Unidad 2


## 🤔 Fase: Reflect

### Actividad 6

 Parte 1: recuperación de conocimiento (Retrieval Practice)

1. Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?

R/ Es una maquina capaz de realizar diferentes tareas a traves del manejo de estados. los cuatro componentes fundamentalos son el estado, evento y accion.

2. Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

  R/ Porque es capaz de realizar tareas a la vez mientras un estado espera a que el temporizador alcance el tiempo que tiene para realizar otra tarea y a diferencia del sleep, no apaga el programa por un tiempo y puede gestionar diferente actividades.

3. Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

   R/ En el estado armed añadiria un nuevo evento que hiciera la accion de modificar el tiempo a la mitad, pero la condicion seria que solo se pudiera reducir el tiempo si esa reduccion no es menor que 10.

4. Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

   R/ Es

Parte 2: reflexión sobre tu proceso (Metacognición)

1. ¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?
   

2. Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?


3. El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?


4. Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?
