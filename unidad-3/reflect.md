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

R/ El evento estaria el estado ARMED y cada vez que ocurra la accion de reducir el tiempo a la mitad la flecha volveria a ARMED mientras que la bomba no llegue a 0.

Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

R/ Es poner en funcionamiento la maquina de estados y probar los eventos y acciones para cambiar de estado y corroborar que funcione adecuadamente. Es muy útil ya que permite encontrar fallos o partes a mejor facilmente en el programa ademas de que facilita observar como funciona el programa o como deberia de estar funcionando.

Parte 2: reflexión sobre tu proceso (Metacognición)

¿Qué parte del diseño de la bomba te resultó más desafiante: crear el diagrama de estados o traducir ese diagrama a código? ¿Por qué?

R/ traducir el código fue más complejo, ya que en este caso teniamos que traducir el modelo de arquitectura de python a javascript, pero lo complicado era cambiar la sintaxis, ya que tenia que biscar mucha info para realizarlo y aveces me generaba errores y seguir corrigiendo la sintaxis.

Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?

R/ Muchos errores fueron de sintaxis, ya que me generaba errores y tocaba solucionarlos poco a poco. Por otro lado, me generaba problemas añadir la parte de identificar las teclas y realizaba los vectores de prueba para hallar los errores y muchas veces eran errores pequeños como de escritura.

El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?

R/ Si,inicie añadiendo cosas simples como las variables, los estados principales, luego los cambios de estado e iba poniendo las acciones en cada uno y añadiendo funcionalidades que necesitara para complementar y en diferentes instancias ponia a funcionar el código a ver si funciona bien.

Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?

R/ Se puede aplicar en muchos casos de entretenimiento digital y en diferentes proyectos donde veas que hay cambios importantes de estados o que necesites una buena concurrencia en tu programa sin necesidad de poner un alto en el programa.

### Actividad 9

Responde a las siguientes preguntas con total sinceridad. ¡Cada comentario es valioso!

Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?

R/ Las diferentes versiones de la bomba, ya que muestra diferentes funcionalidades sin necesidad que colocar solo una version como explicacion, ya que con diferente versiones se puede entender un poco mas diferentes formas de realizar el programa sin que se siente muy abrumador en el tema de abordar los conceptos.

Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso? ¿Qué cambiarías o eliminarías?

R/ Al inicio me parecio confuso entender las diferentes funcionalidades de los eventos y hacer el password, pero poco a poco fui entendiendo

Empezar a hacer: ¿Qué te habría ayudado a entender mejor?

R/ Tal vez separar un poco más la funcionalidades y luego unificarlas para entender algunas cosas mejor.


Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa a diseñar y programar uno complejo? ¿Por qué?

R/ 4,2. En este caso fue complejo porque siempre habia varias funcionalidades para realizar en la bomba y diferentes versiones que realizar y teniamos que cambiar la sintaxis que siempre tomaba su tiempo mirar que nos puede funcionar y que errores pueden salir en el programa.



