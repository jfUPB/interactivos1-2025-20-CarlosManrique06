
# Evidencias de la unidad 7


### Actividad 1

- ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?

R/ Obtuve https://3ncnsvph-3000.use2.devtunnels.ms/. Porque localhost  solo existe dentro de cada dispositivo,  si escribiera http://localhost:3000 en el celular, este buscaría el servidor dentro del propio celular, no en un servidor y eso solo funciona si ambos dispositivos están conectados a la misma red Wifi. En cambio, la URL de Dev Tunnels es pública y accesible , porque el servicio crea un túnel seguro desde esa dirección hacia el puerto 3000 del computador. De esta forma, cualquier dispositivo puede conectarse al servidor local.

- Describe brevemente qué hace npm install y npm start.

R/ npm install, lo que hace es instalar todos los paquetes y dependencias para que el programa funcione correctamente y npm start inicializa el servidor y escucha en el mismo dispositivo en localhost:3000 para abrir el servidor.

<img width="567" height="256" alt="image" src="https://github.com/user-attachments/assets/8cea86fd-571b-48bb-8195-4d3c0c105d27" />


¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

R/ Observe un 2 mensajes de new client connected, pero los mensajes tanto para el cliente escritorio y cliente móvil eran iguales, otro mensaje que salia era que se recibio un nuevo mensaje de tipo touch que recibe coordenadas en x y coordendas en y del cliente móvil a donde el usuario está tocando para que el círculo cambia de posicion.

<img width="625" height="122" alt="image" src="https://github.com/user-attachments/assets/9b68b176-4274-46e8-a50a-659415668c13" />


Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?

<img width="311" height="408" alt="image" src="https://github.com/user-attachments/assets/9f470d0b-6597-4979-9235-09eb55b620ac" />


R/ La interacción funciono de forma correcta, cada vez que tocaba la pantalla y movía el dedo el círculo se iba moviendo. Sin embargo, si se notaba el retraso de como el círculo se movía cuando hacia el touch en otro lado, se demoraba un poco el círculo en cambiar de posición, probablemente se deba principalmente a que la conexión entre el celular y el servidor no es directa, sino que pasa a través del túnel, provocando que los datos enviados pasen por el intermediario y se demoran un poco más en llegar.


### Actividad 2

- Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?

R/ Dev Tunnels es necesario porque el servidor Node.js corre en localhost:3000, lo que significa que solo es accesible desde el mismo dispositivo. Si intento abrir esa dirección desde otro dispositivo como un celular, el sistema buscará el servidor dentro del propio teléfono, no en el computador.

Para permitir que un dispositivo externo acceda, se necesita una dirección pública. Dev Tunnels se vuelve un intermediario  entre una URL pública  y el puerto local donde corre la aplicación. Así, cuando el celular accede a esa URL, el tráfico viaja por el túnel hacia el servidor local y las respuestas vuelven por el mismo camino.

- Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.

R/ La función touchMoved() en p5.js se ejecuta automáticamente cada vez que el usuario mantiene un dedo en la pantalla y lo mueve. En cada llamada, las variables mouseX y mouseY contienen la posición actual de cuando se toca la pantalla. Dentro de esta función, el programa envía las coordenadas del movimiento al servidor. Sin embargo, enviar un mensaje en cada mínima instancia sería ineficiente, porque los sensores táctiles detectan incluso temblores como comentaste en la explicacion conceptual, por eso se sería mejor usar una variable threshold, donde el código compara la distancia entre la posición actual y la última enviada, y solo transmite si el cambio es significativo.


- Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?

R/ Dev Tunnels permite que la aplicación sea accesible desde cualquier lugar, ya que crea un enlace público que reenvía las conexiones directamente al servidor local. Además, no requiere configuraciones adicionales como abrir puertos , lo que lo hace muy práctico para pruebas remotas como se había comentado en clase. Su única desventaja es que puede ser un poco más lento debido al reenvío de datos a través del túnel.

Por otro lado, usar la IP local es más rápido porque la comunicación ocurre dentro de la misma red y dispositivo, sin intermediarios. Sin embargo, solo funciona si ambos dispositivos están conectados a la misma red y no. Además, no ofrece un acceso público y puede ser menos seguro si se exponen los puertos del equipo.

- Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal)

<img width="1522" height="755" alt="image" src="https://github.com/user-attachments/assets/7e1afca2-9592-483b-9b38-ece3dc9e3bde" />


En la imagen se evidencia el cliente del celular, computador y la terminal con los diferentes datos.


### Actividad 3

- ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?

  R/ La función express.static('public') le indica a Express que automáticamentee cuando un cliente accede a la raíz del servidor http://localhost:3000, Express busca y entrega el archivo index.html y demás recursos directamente sin que tengamos que definir rutas manualmente como en la U6, ya que en la U6  con el .get pediamos manualmente esa ruta y se respondía manualmente a cada solicitud HTTP.

- Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?

R/ En el móvil, el evento touchMoved() se activa cuando el usuario mueve el dedo sobre la pantalla. Cada vez que pasa este evento, el cliente envía un mensaje al servidor usando socket.emit('message', datos), donde incluye las coordenadas actuales del toque (mouseX, mouseY). En el servidor, la línea socket.on('message', (message) escucha los mensajes que llegan. Cuando recibe uno, lo muestra en la consola y se prepara para reenviarlo a los demás clientes conectados, luego los clientes como computador tienen un socket.on('message') que escucha los mensajes reenviados por el servidor. Cuando los reciben, actualizan su interfaz, por ejemplo dibujando la nueva posición del círculo en el canvas.


En este caso se usa socket.emit porque envía el mensaje solo al cliente que lo generó y evita duplicar el movimiento en el celular cuando ya se conoce la posicion. Así, solo los otros dispositivos reciben la actualización; Por otro lado, io.emit lo envía a todos los clientes, incluido el emisor y socket.broadcast.emit lo envía a todos menos al emisor.



- Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?

R/ Si el móvil enviara los mismos datos del touch, el servidor los recibe y usa socket.broadcast.emit para reenviarlo como intermediario, haciendo que todos los demás clientes conectados recibirían el mensaje, quitando el propio emisor original.

- ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?

R/ Los mensajes console.log en el servidor sirven como registro de actividad en tiempo real. Permiten saber: Cuándo un nuevo cliente se conecta, los datos que están siendo recibidos, cuando un cliente se desconecta y cuando el servidor escucha al port 3000. Esta información sirve para comprobar el funcionamiento del programa, ya sea para depurar errores, verificar la comunicación entre clientes y servidor, y confirmar que los eventos de conexión, envío y desconexión están ocurriendo correctamente.


### Actividad 4

- Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.


