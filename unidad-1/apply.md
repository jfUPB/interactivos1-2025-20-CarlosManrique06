# Unidad 1

## 🛠 Fase: Apply

### Actividad 05

Vamos a crear juntos un programa en p5.js que interactúe con un micro:bit. La idea es que el programa en p5.js muestre un cuadrado en la pantalla que cambie de color al presionar un botón del micro:bit y regrese a su color original al soltar el botón.

~~~js
let port;
let connectBtn;
let connectionInitialized = false;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  
   background(220);
  
   if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }
  
     if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A") {
        fill("red");
      } else if (dataRx == "N") {
        fill("green");
      }
        }
    rectMode(CENTER);
        rect(width / 2, height / 2, 50, 50);
  
  


        if (!port.opened()) {
            connectBtn.html("Connect to micro:bit");
        } else {
            connectBtn.html("Disconnect");
        }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
      connectionInitialized = false;
    } else {
        port.close();
    }
}
~~~




Al ejecutar el programa muestra un botón para establecer o cerrar la conexión con el microbit, y un cuadro en el centro de la pantalla que estara de color verde y cambiara a rojo mientras se presione el boton A en el microbit, sino regresara a color verde. El input es el boton al ser presionado y el cable con los datos enviados desde la microbit a la computadora,enviando A o N. El proceso consiste en leer esos datos seriales, dependiendo del valor recibido, cambiara el color de relleno del cuadro rojo para A y verde para N. El output es la pantalla del computador y el programa que recibe los datos para realizar el proceso correspondiente.



### Actividad 06

Enlace P5

[Ver sketch en p5.js](https://editor.p5js.org/CarlosManrique06/sketches/rJjoo3Ox0)

Código del microbit

~~~py
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.was_pressed():
        uart.write('A')
        
    if button_b.was_pressed():
        uart.write('B')
        
    sleep(100)
~~~

Código de P5
~~~js
let port;
let connectBtn;
let connectionInitialized = false;
let x = 200;

function setup() {
  createCanvas(400, 400);
  background(220);
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx == "A") {
      x -= 20;
    } else if (dataRx == "B") {
      x += 20;
    }
  }
  fill("red");
  circle(x, 200, 40);

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

~~~
