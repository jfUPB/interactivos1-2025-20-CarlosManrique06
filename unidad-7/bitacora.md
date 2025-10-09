
# Evidencias de la unidad 7


### Actividad 1

¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?

R/

Describe brevemente qué hace npm install y npm start.

R/ npm install, lo que hace es instalar todos los paquetes y dependencias para que el programa funcione correctamente y npm start inicializa el servidor y escucha en el mismo dispositivo en localhost:3000 para abrir el servidor.

¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

R/

Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?

R/


### Actividad 2

- Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?

R/ Dev Tunnels es necesario porque el servidor Node.js corre en localhost:3000, lo que significa que solo es accesible desde el mismo dispositivo. Si intento abrir esa dirección desde otro dispositivo como un celular, el sistema buscará el servidor dentro del propio teléfono, no en el computador.

Para permitir que un dispositivo externo acceda, se necesita una dirección pública. Dev Tunnels se vuelve un intermediario  entre una URL pública  y el puerto local donde corre la aplicación. Así, cuando el celular accede a esa URL, el tráfico viaja por el túnel hacia el servidor local y las respuestas vuelven por el mismo camino.

- Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.

R/ La función touchMoved() en p5.js se ejecuta automáticamente cada vez que el usuario mantiene un dedo en la pantalla y lo mueve. En cada llamada, las variables mouseX y mouseY contienen la posición actual de cuando se toca la pantalla. Dentro de esta función, el programa envía las coordenadas del movimiento al servidor. Sin embargo, enviar un mensaje en cada mínima instancia sería ineficiente, porque los sensores táctiles detectan incluso temblores como comentaste en la explicacion conceptual, por eso se sería mejor usar una variable threshold, donde el código compara la distancia entre la posición actual y la última enviada, y solo transmite si el cambio es significativo.


- Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?

R/  Dev Tunnels permite que la aplicación sea accesible desde cualquier lugar, ya que crea un enlace público que reenvía las conexiones directamente al servidor local. Además, no requiere configuraciones adicionales como abrir puertos , lo que lo hace muy práctico para pruebas remotas como se había comentado en clase. Su única desventaja es que puede ser un poco más lento debido al reenvío de datos a través del túnel.

Por otro lado, usar la IP local es más rápido porque la comunicación ocurre dentro de la misma red y dispositivo, sin intermediarios. Sin embargo, solo funciona si ambos dispositivos están conectados a la misma red y no. Además, no ofrece un acceso público y puede ser menos seguro si se exponen los puertos del equipo.

- Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal)

R/
