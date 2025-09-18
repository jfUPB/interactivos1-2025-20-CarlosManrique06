
# Evidencias de la unidad 5

### Act1 


#### 1. ¿Cómo se están comunicando el micro:bit y el sketch de p5.js?

El microbit usa el serial para enviar datos al computador por el puerto USB y el p5 recibe esos datos por el webserial, el microbit envía de forma cada 100ms una cadena de texto con los valores de:

- Acelerómetro en X (xValue)

- Acelerómetro en Y (yValue)

- Boton A (aState)

- Botón B (bState)

#### 2. ¿Qué datos envía el micro:bit?

El microbit construye la cadena en: data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
uart.write(data)

Ver datos en el serial como HEX

<img width="1070" height="751" alt="Cap2" src="https://github.com/user-attachments/assets/5e73ec02-d85b-4950-be12-67522e2ddc8f" />


Datos en texto
����ASCII:
-1344,-1388,False,False


Datos en Hex
fa c0 fa 94 00 00 41 53 43 49 49 3a 0a 2d 31 33 34 34 2c 2d 31 33 38 38 2c 46 61 6c 73 65 2c 46 61 6c 73 65 0a

#### 3. ¿Cómo es la estructura del protocolo ASCII usado?

El protocolo que se usa aquí es texto plano en ASCII, separado por comas y terminado en salto de línea que es 0a como la linea mostrada arriba.

-  Parte del código de p5.js donde lee y transforma datos se encuentra en el draw y es el siguiente:

```js
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n"); 
  if (data) {
    data = data.trim();           
    let values = data.split(",");  
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    }
  }
}

```
Lee una línea completa en ASCII hasta \n. La divide por comas como por ejemplo: "-120","345","True","False". Convierte los primeros dos a enteros a coordenadas X y Y.Convierte los dos últimos a booleanos de estado de botones A y B y con  a updateButtonStates() se manejan los eventos keypress keypress up.


### Act 2

Ver datos en el serial como texto

<img width="1081" height="759" alt="image" src="https://github.com/user-attachments/assets/9260fcdc-ec03-4fb1-8932-fc39646eefb6" />

Cuando cambio la linea para enviar datos en binario:

```py

data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
uart.write(data)
```

En el serialTerminal  mostrado en la imagen de arriba se evidencias caracteres raros que son ilegibles.

Esto pasa porque los bytes que se envian ya no representan letras ASCII como 123,456,True,False\n, sino que son valores binarios puros. El programa de terminal intenta interpretarlos como letras, pero muchos bytes no corresponden a códigos ASCII respecto a texto, y por eso no se muestran interpretados sino ilegibles.


####  Experimento 2: ver los datos como Hexadecimal

![Serial en AScii](https://github.com/user-attachments/assets/5e80fe1e-c95a-4b45-898b-4297634a7979)


Esto corresponde a los bytes enviados por struct.pack(), donde el byte más significativo va primero, 2h hacer referencia a dos enteros cortos con signo y 2B dos enteros corto sin signo, donde cada bloque representa directamente los números binarios empaquetados en 6 bytes en total.

-  ¿Ventajas y desventajas de usar binario frente a ASCII?

El binario tiene la ventaja de que solo estas enviando 6 bytes en este este caso y no tienes que pasarlo de nú,eros a cadena de texto, lo cual lo hace más rápido de enviar y procesar por el microbit, la desventajas que tiene es que al ser interpretdo en números es dificil de interpretarlo directamente y requieres un programa hex que lo pueda interpretar para saber los datos que estas enviando, como estamos enviando un paquete compactado, si uno de esos bytes se pierde o no se envía correctamente el paquete completo se dañaria.


el ASCII es más fácil de leer e interpretar, con el salto de linea se reenvia todo al microbit si hay algun error, pero es mucho más lento haciendo que tenga menor eficiencia, ya que toca pasarlos en cadenas que suelen ser mucho más largas en bytes.

#### Experimento con el gesto shake

Con este código:

```py

if accelerometer.was_gesture('shake'):
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
    uart.write(data)

```

Cuando se sacude el microbit, se manda un solo paquete en binario.

- ¿Cuántos bytes se envían por mensaje?

con 2h serian 4 bytes, que son 2 enteros cortos con signo, con 2B seria 2 enteros cortos sin signo, lo cual daria 6 bytes en total.

#### ¿Cómo se verían positivos y negativos en binario?

Los números posiitvos se representan con los mismos bits como por ejemplo, el 6 en 4 bits se representa como 0110. Por otro lado, los números negativos se tienen que representar en complemento  a dos.

El complemento a dos es un sistema binario de representación numérica utilizado por las computadoras para codificar números enteros positivos y negativos. Permite operaciones aritméticas eficientes y simplifica los circuitos lógicos en sistemas digitales

Cuando el bit más significativo, el cual es el dígito más a la izquierda de un número binario, si ese es 1 el número entero se señala como negativo y cuando es 0 El número entero se señala como positivo.

Ejemplo
Con representación de 4 bits, el número 6 en binario es 0110. Para tomar el complemento a dos, invertir cada bit, que se convierte en 1001, y añade 1: 1010 (representa -6).

####  Experimento final: enviar binario + ASCII

Código:

```py
data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
uart.write(data)
uart.write("ASCII:\n")
data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
uart.write(data)
```

Binario: mejor para transmisión eficiente en sistemas en tiempo real.

ASCII: mejor para depuración, prototipado, y cuando importa la legibilidad.

### Actividad 3

#### Pregunta 1

Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

Antes en ASCIIc como cada dato tenía longitud variable como:  -120, 524, True, False\n. El lector no sabía cuántos caracteres correspondían a cada valor. Por eso era necesario usar comas para separar y un salto de línea \n para marcar el final del paquete.

Ahora en el binario el tamaño del paquete está fijo en 6 bytes. El interpretador sabe cuánto medirán los datos y puede leerlos directamente sin delimitadores. En ASCII era necesario delimitar porque los datos tenían tamaños variables. En binario no, porque el tamaño es fijo.


#### Error de lectura de datos

¿Qué ves en la consola? ¿Por qué crees que se produce este error?

Ejemplo de salida:
```js
microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false
microBitX: 500 microBitY: 513 microBitAState: false microBitBState: false
microBitX: 3073 microBitY: 1 microBitAState: false microBitBState: false
```

A veces los valores son correctos (500, 524), otras veces aparecen números que no corresponden como  (513, 3073). probablemente esto ocurre porque el receptor puede empezar a leer desde la mitad de un paquete. Como los datos binarios no tienen delimitador, va leyendo y corriendo esos dato y se interpretan bytes de dos paquetes distintos, así que probablemente sea un error de sincronizacion que no siempre coincide con los 6 bytes enviados por el microbit.


#### Framing

Framing es el acto de delimitar el comienzo y fin de un mensaje. Esto se denomina framing, porque este acto crea un marco (frame) en donde el mensaje puede ser enviado y delimitado.

Cuando estaba investigando vi que habían varias formas de realizar la delimitacion y una de ellas era Byte stuffing, la cual es una estrategia para indicar caracteres de control en las cadenas, donde se define un delimitador y un caracter de escape. El delimitador indica el principio y fin del frame para saber donde cortar el receptor.

- ¿Qué ves cuando aplicamos la estrategia de framing con header (0xAA) y checksum?

El código ahora acumula bytes  y solo procesa cuando encuentra el header 0xAA + 6 datos + checksum. Si el checksum no coincide, el paquete se descarta.

En la consola empiezan a verse datos estables y sin errores de sincronización:

```js
microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false
microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false
microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false

```
Con framing y checksum se logra sincronización confiable, se detectan paquetes corruptos y se garantiza la integridad de la comunicación entre el microbit y el envio de datos. En cambio sin el puede generar errores de sincronizacion porque el receptor no sabe donde cortar y verificar que los datos enviados son los correctos

- ¿Qué otras estrategias de framing existen además del delimitador que usamos? 

De lo que estuve investigando y complementa lo que dije arriba del  byte stuffing. Para el framing  existen varias estrategias con diferentes atributos. Estas estrategias se pueden agrupar en estrategias de stuffing, estrategias con campos de longitud, violación de código y de longitud fija.

Entre las estrategias de stuffing, las dos principales son bit stuffing y byte stuffing. Bit stuffing consiste en definir un delimitador (usualmente 01111110) y enviar los datos precedidos y antecedidos por el delimitador. 

Otra forma de indicar el fin de un frame consiste en indicar la longitud de un mensaje en un campo del encabezado. Esta longitud debe encontrarse en un lugar predecible, ya que será necesario interpretarla correctamente para determinar donde termina un frame.

- ¿Qué ventajas tendría un framing por longitud frente a uno por delimitadores en términos de fiabilidad y velocidad?.

El framing por longitud resulta más eficiente porque el receptor sabe exactamente cuántos bytes leer, aunque corre el riesgo de perder toda la trama si el campo de longitud se corrompe. En cambio, el framing por delimitadores es más simple de implementar y permite re-sincronizar al encontrar un nuevo delimitador, aunque es menos eficiente ya que requiere escanear los datos. Por esto, la primera técnica suele usarse en protocolos binarios de alto rendimiento, mientras que la segunda es común en protocolos sencillos o basados en texto, como mensajes ASCII o comunicación serial básica.


La info de lo que investigue fue sacada de: [Link Archivo](https://www.cubawiki.com.ar/images/7/72/Puntoapunto.pdf)

### Act4

Código:

```js
let serialBuffer = [];


var modules;

var tileSize = 30;
var gridResolutionX;
var gridResolutionY;
var tiles = [];

var doDrawGrid = true;
var isDebugMode = false;

function preload() {
  // load SVG modules
  modules = [];

  // METHOD 1: Looping through local files is efficient
  // for (var i = 0; i < 16; i++) {
  //   modules[i] = loadImage('data/' + nf(i, 2) + '.svg');
  // }

  // METHOD 2: Read files one-by-one
  modules[0] = loadImage('data/00.svg');
  modules[1] = loadImage('data/01.svg');
  modules[2] = loadImage('data/02.svg');
  modules[3] = loadImage('data/03.svg');
  modules[4] = loadImage('data/04.svg');
  modules[5] = loadImage('data/05.svg');
  modules[6] = loadImage('data/06.svg');
  modules[7] = loadImage('data/07.svg');
  modules[8] = loadImage('data/08.svg');
  modules[9] = loadImage('data/09.svg');
  modules[10] = loadImage('data/10.svg');
  modules[11] = loadImage('data/11.svg');
  modules[12] = loadImage('data/12.svg');
  modules[13] = loadImage('data/13.svg');
  modules[14] = loadImage('data/14.svg');
  modules[15] = loadImage('data/15.svg');

}

let port;
let connectBtn
let microBitConnected = false;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};

let appState = STATES.WAIT_MICROBIT_CONNECTION;

let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;




function setup() {
  // use full window size
  createCanvas(windowWidth, windowHeight);
  
   // Adición del serial
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}
function updateButtonStates(newAState, newBState) {
  
  if (newAState === true && prevmicroBitAState === false) {
  
    

    print("A pressed");
  }

  if (newBState === true && prevmicroBitBState === false) {
    
   
    initTiles();
    print("B pressed");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
function readSerialData() {
  // Acumula los bytes recibidos en el buffer
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

  // Procesa el buffer mientras tenga al menos 8 bytes (tamaño de un paquete)
  while (serialBuffer.length >= 8) {
    // Busca el header (0xAA)
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift(); // Descarta bytes hasta encontrar el header
      continue;
    }

    // Si hay menos de 8 bytes, espera a que llegue el paquete completo
    if (serialBuffer.length < 8) break;

    // Extrae los 8 bytes del paquete
    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8); // Elimina el paquete procesado del buffer

    // Separa datos y checksum
    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    // Calcula el checksum sumando los datos y aplicando módulo 256
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue; // Descarta el paquete si el checksum no es válido
    }

    // Si el paquete es válido, extrae los valores
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);
    
    console.log(
      `microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState}`
    );

  }
}
function draw() {
  
  background(255);
  
    if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");
  }
  
  
   switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
           case STATES.WAIT_MICROBIT_CONNECTION:
      
      // evento 1:
      if (microBitConnected === true) {
        // Preparo todo para el estado en el próximo frame
         cursor(CROSS);
         rectMode(CENTER);
         imageMode(CENTER);
         strokeWeight(0.15);
         textSize(8);
         textAlign(CENTER, CENTER);

        gridResolutionX = round(width / tileSize) + 2;
        gridResolutionY = round(height / tileSize) + 2;

        initTiles();
      
        
        
        appState = STATES.RUNNING;
      }

      break;

    case STATES.RUNNING:
       
         if (microBitConnected === false) {
        print("Waiting microbit connection");
        cursor();
        appState = STATES.WAIT_MICROBIT_CONNECTION;
      }
       
         readSerialData();
          
        
        if (microBitAState === true)
        
        {
            
           setTile();
          
         
          if (mouseIsPressed && mouseButton == RIGHT)
           
          {
               unsetTile();
          }
        }
       
  }



  if (doDrawGrid) drawGrid();
  drawModules();
}

function initTiles() {
  for (var gridX = 0; gridX < gridResolutionX; gridX++) {
    tiles[gridX] = [];
    for (var gridY = 0; gridY < gridResolutionY; gridY++) {
      tiles[gridX][gridY] = 0;
    }
  }
}

function setTile() {
  // convert mouse position to grid coordinates
  var gridX = floor(microBitX / tileSize) + 1;
  gridX = constrain(gridX, 1, gridResolutionX - 2);
  var gridY = floor(microBitY / tileSize) + 1;
  gridY = constrain(gridY, 1, gridResolutionY - 2);
  tiles[gridX][gridY] = 1;
}

function unsetTile() {
  var gridX = floor(microBitX / tileSize) + 1;
  gridX = constrain(gridX, 1, gridResolutionX - 2);
  var gridY = floor(microBitY / tileSize) + 1;
  gridY = constrain(gridY, 1, gridResolutionY - 2);
  tiles[gridX][gridY] = 0;
}

function drawGrid() {
  for (var gridX = 0; gridX < gridResolutionX; gridX++) {
    for (var gridY = 0; gridY < gridResolutionY; gridY++) {
      var posX = tileSize * gridX - tileSize / 2;
      var posY = tileSize * gridY - tileSize / 2;
      fill(255);
      if (isDebugMode) {
        if (tiles[gridX][gridY] == 1) fill(220);
      }
      rect(posX, posY, tileSize, tileSize);
    }
  }
}

function drawModules() {
  for (var gridX = 0; gridX < gridResolutionX - 1; gridX++) {
    for (var gridY = 0; gridY < gridResolutionY - 1; gridY++) {
      // use only active tiles
      if (tiles[gridX][gridY] == 1) {
        // check the four neightbours, each can be true or false
        var NORTH = str(tiles[gridX][gridY - 1]);
        var WEST = str(tiles[gridX - 1][gridY]);
        var SOUTH = str(tiles[gridX][gridY + 1]);
        var EAST = str(tiles[gridX + 1][gridY]);

        // create binary result out of it
        var binaryResult = NORTH + WEST + SOUTH + EAST;

        // convert binary string to a decimal value from 0 - 15
        var decimalResult = parseInt(binaryResult, 2);

        var posX = tileSize * gridX - tileSize / 2;
        var posY = tileSize * gridY - tileSize / 2;

        // decimalResult is also the index for the shape array
        image(modules[decimalResult], posX, posY, tileSize, tileSize);

        if (isDebugMode) {
          fill(150);
          text(decimalResult + '\n' + binaryResult, posX, posY);
        }
      }
    }
  }
}

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (key == 'g' || key == 'G') doDrawGrid = !doDrawGrid;
  if (key == 'd' || key == 'D') isDebugMode = !isDebugMode;
}
```
Primer cambio:

siguiendo el ejemplo del profe, agregué un serialBuffer que acumula los bytes recibidos. Esto fue necesario porque los datos no llegan siempre completos, sino en fragmentos.

```js
let serialBuffer = [];

function readSerialData() {
  // Acumula los bytes recibidos en el buffer
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

```
 Esto implementa un framing por longitud fija  con delimitador (0xAA) para sincronización. Luego segui añadiendo lo demás como el cheksum para que descartara los paquetes invalidos.


Experimento C: Botones A mientras se usan los accelerometros del microbit

Botón A: dibuja tiles.

Botón B: reinicia el canva.



<img width="1918" height="999" alt="Act4_Apply" src="https://github.com/user-attachments/assets/53bbf478-1e8a-4b5a-9cfe-f1391e597e62" />

En la imagen se evidencia que los datos están siendo recibidos, ya que coloque el: 

console.log( `microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState}`);

Para corroborar que los datos se estaban enviando corrrectamente 

 4. Evidencias conceptuales

Framing: Se implementó un framing con delimitador y longitud fija. Esto asegura resincronización rápida en caso de error.

Checksum: Aplicado como validación 

Control de flujo: Hay un control con el console.log para saber si se estaban enciando los datos correctamente

Hacer esta ac4 me permitió comprender que pasar de mensajes de texto a datos binarios estructurados es un salto fundamental en protocolos de comunicación para darle una mayor eficiencia al sistema al que quiero enviarle los datos y que no consuma tanta memoria tratando de traducir toda una cadena como en ASCII.
