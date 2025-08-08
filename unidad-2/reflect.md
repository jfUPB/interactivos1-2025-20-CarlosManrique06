# Unidad 2


## 🤔 Fase: Reflect

### Actividad 6

- Parte 1: recuperación de conocimiento (Retrieval Practice)

1. Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?

R/ Es una maquina capaz de realizar diferentes tareas a traves del manejo de estados. los cuatro componentes fundamentalos son el estado, evento, accion y transicion.

2. Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

  R/ Porque es capaz de realizar tareas a la vez mientras un estado espera a que el temporizador alcance el tiempo que tiene para realizar otra tarea y a diferencia del sleep, no apaga el programa por un tiempo y puede gestionar diferente actividades.

3. Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

   R/ En el estado armed añadiria un nuevo evento que hiciera la accion de modificar el tiempo a la mitad, pero la condicion seria que solo se pudiera reducir el tiempo si esa reduccion no es menor que 10.

4. Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

   R/ Un vector de prueba es realizar una descripcion sobre  la transicion de un estado a otro para corroborar que funciona adecuadamente y es fundamental para ver si se encuentran errores a corregir o si esta funcionando como deberia funcionar

Parte 2: reflexión sobre tu proceso (Metacognición)

1. ¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?
   
R/ Traducir el código a Micropython, ya que aveces tocaba corregir errores en el código y al inicio terminando de enteder el utime diff, que a la hora de ponerlo en el código no me funciona bien, pero luego entendi mejor su funcionamiento y entendí sin problema como funciona y se maneja.

2. Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?

   R/ Me ayuda de la forma en saber si el código está funcionando debidamente o si me falta implementar algo me pregunto cual es el estado, el evento y la transicion.


3. El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?

   R/ Si, primero añadi los estados y las transiciones principales para el funcionamiento del programa y luego fui añadiendo detalles como música, mostrar figuras en pantalla y detalles de feedback.


4. Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?

   R/ No tengo un proyecto claro, pero podria ser implementado en una receta para un videojuego o una experiencia interactiva de este tipo, con el fin de saber en que paso de la receta estoy y así ejecutarla de mejor manera.

### Actividad 7

- Analiza de manera crítica el diseño y la implementación de tu compañero y deja un comentario de retroalimentación específico y constructivo.

R/ El compañero realizo el ejercicio muy bien, implemento los estados de manera correcta y tiene feedback al usuario para saber lo que se esta realizando en el programa, las diferencias del código entre mi compañero y yo es más de la parte visual y feedback.

### Actividad 8

- Responde a las siguientes preguntas con total sinceridad. ¡Cada comentario es valioso!

4. Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?

R/ La bomba que es el apply es la que me ayudo a afianzar de mejor lo aprendido en clase, ya que me enfrente por mi solo a todo el concepto visto en clase y eso me ayudo a entende todo mejor. El elemento más importante es la maquina de estados, ya que es una forma buena de representar lo que va a realiar el programa y para encontrar errores.

2. Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso, innecesariamente complicado o que aportó poco a tu aprendizaje? ¿Qué cambiarías o eliminarías?

R/ Me confundi un poco en la explicacion del utime, pero a la hora de realizar la practica entendí mucho mejor el concepto


3. Empezar a hacer: ¿Qué te habría ayudado a entender mejor?

R/ Alguna explicacion más ya respecto a los temas de las funciones que tiene el microbit como la de realizar que se muestre un conteo regresivo.


4. Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa (Actividad 03) al diseño desde cero de uno complejo (Actividad 04 y 05)? ¿Por 
qué?

 R/ 3.5 . Aunque la dificultad dependeria del problema a realizar ya que podria ser más sencillo o más complejo de diseñar y pasarlo a código.
