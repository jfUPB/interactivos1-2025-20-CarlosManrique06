
# Evidencias de la unidad 6

### Actividad 1

<img width="576" height="362" alt="ClonarRepositoria" src="https://github.com/user-attachments/assets/31df172c-5a7b-43e6-a32e-27e43191bad4" />

Tuve que usar el github bash para clonar el repositorio en el computador. Primero use el comando: git clone https://github.com/juanferfranco/entangledTest-sfi1-2025-20.git . Para clonarlo en el pc luego utilice 
el comando cd  entangledTest-sfi1-2025-20 Para acceder al directorio, después use el code . para abrilo en visual code y el punto para abrir el directorio.

Para iniciar las pag se usa el npm install y luego npm start para correr las pag en la web.

¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?

```bash
B09S113est@N00023578 MINGW64 ~/entangledTest-sfi1-2025-20 (main)
$ npm install

added 120 packages, and audited 121 packages in 4s

17 packages are looking for funding
  run `npm fund` for details
```
El terminal empezo a instalar las librerias necesarias para poder ejecutar el servidor.

¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?

<img width="757" height="377" alt="PagVacia" src="https://github.com/user-attachments/assets/1723d659-3840-4d05-b3e8-f669853c1a6b" />

R/ El mensaje esta preguntando por la direccion

Describe lo que ves inicialmente en page1 y page2 en tu navegador.

R/ <img width="386" height="276" alt="paginas" src="https://github.com/user-attachments/assets/cdca4ca1-b7b8-4a72-9c4d-16c2e3e0ac2f" />

Aparece que sincronizando datos, esperando a que se conecte a la segunda pag web.


¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?

R/ Aparece que un usuario se conecto y el id del usuario, donde se reciben los datos de ese usuario conectado.

```bash
A user connected - ID: -KLfr7wyM8QkYQ2TAAAB
Received win1update from ID: -KLfr7wyM8QkYQ2TAAAB Data: { x: 0, y: 0, width: 1920, height: 911 }

```

Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?

R/ <img width="1663" height="827" alt="Pagfuncional" src="https://github.com/user-attachments/assets/02bd5e0f-edb9-479e-8ff3-7a7d4a9bbe0c" />

### Actividad 2

#### Pregunta 1
- Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.
  
Si se corta la rampa: me quedo desconectado de la red, así que no podría llegar a acceder a ninguno de los servicios de los servidoes. Es como si el carro quedara sin entrada a la autopista, puedo tener vehículo  pero no hay forma de que avance por los servidores.

- ¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?

 Por ejemplo en el Restaurante: Cliente: el comensal, el Servidor es el mesero, la petición es lala orden de comida y la respuesta es el plato servido en la mesa. EN una biblioteca el cliente es el estudiante, el servidor el bibliotecario, la peticion un libro especifico y la respuesta prestamo del libro. En un supermercado el cliente es el comprador, el servidor es el cajero, la peticion es pagar por los productos y la respuesta es la comprar registrada y el recibo

- Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

En la siguiente ruta: https://www.youtube.com/feed/subscriptions. El protocolo es https://, el nombre de dominio es www.youtube.com y la ruta es /feed/subscriptions. Si no se coloca una ruta especfica te llevaria la parte principal del dominio en mi caso a https://www.youtube.com que es la parte por defecto del dominio.

#### Preguntas 2

- Compara HTTP con los protocolos seriales que usaste.

¿Qué similitudes encuentras?

Similitudes:

Ambos sirven para comunicar dos dispositivos como cliente y servidor en HTTP o  microbit  y computador en serial, En los dos casos la información viaja como secuencia de bytes. Requieren un formato acordado: si el receptor no entiende el orden o el tipo de datos, no puede interpretarlos y se basan en el mismo principio: uno envía, el otro recibe y responde.


¿Qué diferencias clave ves?

Serial ASCII/binario: muy simple, envías caracteres o valores, sin mayor organización, diseñado para comunicacion entre dispositivos.

HTTP: tiene una estructura definida línea de petición, cabeceras, cuerpo del mensajes,etc. Diseñado para la web.


¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?


Serial: basta con enviar un byte o un string, el otro lo interpreta directamente.

HTTP: necesita describir qué recurso pides, qué formato usas, qué lenguaje hablas, cuánto mide el mensaje, etc. Manda es un paquete de instrucciones para el navegador.

#### Preguntas 3

Piensa en una página web simple, como un formulario de login.

- ¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?

R/ HTML Es todo los campos donde escribes el texto, como usuario y contraseña, los botones que hay para cuando escribes los datos

- ¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?

R/ Es todo el apartado visual, el diseño de los botones, la tipografia del texto, el fondo de la pagina y demás.

- ¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?

R/ Es todo lo que son funciones, cuando tu realices cierta accion, es todo lo que sucede después como los menjaes de error, cuando aparecen los botones y el diseño y cundo ingresas el usuario y contraseña correcto.

#### Pregunta 4

Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.

- ¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?

Mejora el rendimiento del programa, es más práctico, ya que muchas veces en la web tu no necesitas estar cada ciertos frames revisando funciones y ejecutando código, sino que normalmente las funciones ocurren cuando sucede un evento como, di click y cargo la pagina, undi este boton y me llevo a tal parte, presione el scroll y empezo a subir y bajar la pagina, entonces es mucho mejor en este caso, ya que no necesitas estar revisando y ejecutando constantemente el código a preguntar si ocurrió una acción

¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?

No seria eficiente, ya que estar redibujando la página sino a cambiado gasta recursos de memoria innecesarios si solo se nececita redibujar la página cuando ciertos eventos ocurran.


- ¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?

Porque permite que todo el ciclo de una aplicación web, tanto lo que ocurre en el navegador y lo que ocurre en el servidor, se escriba en el mismo lenguaje. Así, un desarrollador no tiene que aprender dos lenguajes distintos en el cliente y  el servidor, pudiendo reutilizar código de entre ambos servidores, sabiendo que manejas muy bien un solo lenguaje lo cuál también ahorra tiempo en el desarrollo de la web.


- Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?

La comunicación HTTP tradicional funciona bajo el esquema pregunta y respuesta, donde el cliente siempre inicia la petición y el servidor solo responde. En cambio, con WebSockets/Socket.IO se abre un canal de comunicación en tiempo real, lo que permite que tanto el cliente como el servidor envíen información de manera continua sin necesidad de estar pidiendo todo el tiempo. Esto es ideal para aplicaciones como chats en línea, videojuegos multijugador y notificaciones instantáneas.

### Actividad 3

#### Experimento 1

<img width="985" height="686" alt="image" src="https://github.com/user-attachments/assets/9fd4b5ba-1a0b-49af-870a-436ceab28cb2" />

¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? 

R/ Esto demuestra que el servidor solo responde a las URLs que tú defines con app.get(). Si cambias la ruta, solo esa nueva URL funcionará cuando reinicies el servidor.


#### Experimento 2

- Conectado al servidor (ID)

Page1: A user connected - ID: hqUVJnyF_DdftLn0AAAB

Page2: A user connected - ID: zexBLvCkSIiNAOMZAAAD

- Desconectado del servidor (ID)

Page1: User disconnected - ID: hqUVJnyF_DdftLn0AAAB

Page2: User disconnected - ID: zexBLvCkSIiNAOMZAAAD

-  El ID de cada pagina coincide tanto cuando se conecta al servidor y cuando se desconecta.

En conclusión, cada vez que un cliente  se conecta al servidor, el servidor le asigna un ID único. Cuando se cierra la pestaña, el servidor detecta la desconexión y muestra el mismo ID. Así, el servidor puede identificar y gestionar cada cliente de forma individual. 

#### Experimento 3


<img width="578" height="177" alt="image" src="https://github.com/user-attachments/assets/94e87b84-fe0e-415a-af52-751b7b15669d" />


Cuando muevo page1 aparece win1update y cuando muevo page2 aparece win2update, en ambos casos se registra x, y , altura y ancho.
