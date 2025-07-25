# Unidad 1

## 🤔 Fase: Reflect

### Actividad 7

En tu bitácora. Sin mirar tus apuntes, los tutoriales o los sketches previos, responde a las siguientes preguntas con tus propias palabras. El objetivo es el proceso de recordar, no la perfección.

Parte 1: recuperación de conocimiento (Retrieval Practice)

Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.

R/ Una de las características que definen un sistema físico interactivo es la inmersion que puede ofrecer el sistema, la variabilidad que puede tener el sistema como la aleatoridad haciendo que cada vez que el programa realiza el proceso el resultado puede ser totalmente diferente cada vez que se realice y por último que está la posibilidad de manejar el sistema en tiempo real para poder usar lo que percibimos en niestro entorno en lo que queremos mostrar.

Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?

R/ -Input: Cuando se presiona el boton A o B es un input que mandara la infomacion por el cable conectado entre el microbit y el Pc ese cable es otro input que termina de mandar la informacion al computador y el programa.
   -Proceso: Cuando se presiona el boton A o B en el microbit el circulo mostrado en pantalla a traves del código se movera a la izquierda o la derecha en el canvas cierta cantidad cada vez que se presione uno de los dos botones.
   -Output: Es la pantalla donde se evidencia el resultado del programa.

¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?

R/ la línea uart.write manda esa informacion escrita de A a P5 y la recibira una funcion que se encargara de realizar un proceso si se envia esa informacion A.

¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?

R/ El arte generativo esta hecho bajo una serie de pasos programados en la computadora que por ejemplo en base a un promt tiene un facor de aleatoridad.

Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.

R/En el microbit tendria que programar  el momento que detecte la acción shake y enviar esa informacion a P5 y en P5 tendría que crear un circulo, recibir esa informacion shake para realizar el cambio de color y tendría que usar la funcion de random en los colores para que cambie cada vez con el shake.

Parte 2: reflexión sobre tu proceso (Metacognición)

¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?

R/ Para mi la parte técnica, ya que se trabaja con dos sistemas que usan lenguajes de código diferentes, entonces toca hacer el código en el microbit y luego el código en p5 y toca conectarlos para que reciban y mande información.

Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?

R/ Que el microbit es encargado de enviar la info a p5 para realizar lo que se quiere hacer en el programa y que ambas tienen que estar enviando y recibiendo información para que el proceso se realice sin complicaciones

Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?

R/ La respuesta sigue siendo similar a la anterior, ya que seguimos en fase de aprendizaje y para tener más claridad acerca de como lo usaria para futuros proyectos seria cuando poco a poco vaya entendiendo más y realizando más prototipo sobre sistemas fisicos interactivos.

El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?

R/ Como es un territorio nuevo, paso paso lo siento mejor, porque así puedo ir entendiendo como va funcionando cada parte sabiendo que no hay errores al hacer el ejemplo. Por otro lado, creo que también es importante realizarlo por cuenta propia para afianzar conocimientos y ponerme a pensar de como lo hago, así que es bueno tener ambas.


### Actividad 8

Tu compañero resolvió el problema de manera diferente a ti, qué hizo diferente, qué aprendiste de su solución. En tu bitácora documenta lo anterior y escribe, como si le estuvieras explicando, lo que tú hiciste y por qué es diferente a lo que hizo tu compañero.

R/ Lo que tenemos el compañero y yo es muy parecido, para mover el circulo puse que con A se moviera en el eje x  con un valor de -20 y cuando se presiona B se moviera en el eje x con u valor de +20, el color del criculo es diferente y que mi compañero trato de añadir la opcion de shake en el microbit para reañizar una accion, pero no lo termino.

### Actividad 9

Responde a las siguientes preguntas. Tu honestidad es el recurso más valioso para la mejora del curso.

1.Continuar: ¿Qué actividad, video o ejemplo de esta unidad te resultó más inspirador o te ayudó más a entender el potencial de los sistemas físicos interactivos?

R/ Un video que me resulto inspirado fue el del VJ realizando los cambios del sistema fisico interactivo en tiempo real, el vero como utlizaba sus oidos para mostrar en base a lo que sentia lo que quiere representar. y el potencial de lo que puede hacer un sistema de este tipo en tiempo real de acuerdo a lo que percibimos a nuestro alrededor.

2.Dejar de hacer: ¿Hubo alguna parte que te pareció demasiado abstracta, muy rápida o confusa? ¿Hay algo que crees que podríamos cambiar para que sea más claro?

R/ El funcionamiento del microbit y el p5, pero refieriendome a como el p5 recibe esa informacion y las funciones que de codigo usadas en para poder hacerlo, aveces era un poco confuso para mi entender ese funcionamiento

3.Empezar a hacer: ¿Qué te genera más curiosidad ahora? ¿Te gustaría explorar más sensores del micro:bit (luz, temperatura), crear visualizaciones más complejas en p5.js o ver más ejemplos de proyectos artísticos?

R/ La verdad que seria muy interesante mirar que otras caracteristicas del entorno puede percibir el microbit con los sensores para asi mismo pensar en como utilizar esas sensaciones en un producto mas compejo y ver otros proyectos también me gustaria observar para saber que más se a logrado con los sitemas interactivos

4.Balance inspiración vs. técnica: ¿Cómo sentiste el equilibrio entre ver los videos inspiradores de la Actividad 01 y la parte técnica de conectar las herramientas en las actividades 03-06?
R/ Fue un poco complejo de ver lo que se ha logrado con lo que se inicia a realizarse, pero eso es parte del proceso para llegar a lograr cosas mostradas en los videos.

Comentario adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad introductoria?



