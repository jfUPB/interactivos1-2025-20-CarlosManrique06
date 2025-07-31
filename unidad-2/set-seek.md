# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 1

Describe detalladamente cómo funciona este ejemplo.

R/  Se define una clase llamada Pixel, que representa un píxel ubicado en una posición específica de la pantalla. Cada objeto de esta clase puede encenderse o apagarse cada cierto intervalo de tiempo, haciendo que parpadee. Al crear un objeto Pixel, se le asigna una posición en la pantalla, un estado inicial de brillo el cual es initState y un intervalo de tiempo en milisegundos que nosotros queramos.

En este ejemplo se crean dos píxeles. el primero es pixel1, que cambia cada 1000 milisegundos, y pixel2, que cambia cada 500 milisegundos. En un bucle, el programa llama constantemente al método update() de cada píxel para verificar si ha pasado el tiempo necesario y si es asi cambia su estado y realiza la accion, donde cada píxel parpadee de manera independiente con su propios atributos asignados.

¿Cuáles son los estados en el programa?

R/ El primer estado es Init. En este estado, el programa configura el tiempo de inicio y enciende el píxel con el valor inicial especificado. Después, cambia automáticamente al segundo estado, WaitTimeout.
El segundo estado WaitTimeout, donde el programa está constantemente verificando si ha pasado el intervalo de tiempo establecido. 

¿Cuáles son los eventos/inputs en el programa?
R/ El principal evento es el tiempo, donde el programa calcula cuánto tiempo ha pasado desde que se guardó startTime.

¿Cuáles son las acciones en el programa?
R/ Alterna el estado del píxel entre encendido que es el valor 9 y apagado que es el valor 0, y reinicia el contador de tiempo con el bucle pare seguir ejecutando el bucle del programa.

### Actividad 2
1.Escribe el código que soluciona este problema en tu bitácora.

```py
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(2,0,9,3000)
pixel2 = Pixel(2,2,0,2000)
pixel3 = Pixel(2,4,0,3000)

estado = "ROJO"

while True:
     if estado == "ROJO":
        pixel1.update()
        if pixel1.pixelState == 0:  # Se apagó, pasa al siguiente estado
            estado = "AMARILLO"
            pixel2.state = "WaitTimeout"
            
            

     elif estado == "AMARILLO":
        pixel2.update()
        if pixel2.pixelState == 0:
            estado = "VERDE"
            pixel3.state = "WaitTimeout"

     elif estado == "VERDE":
        pixel3.update()
        if pixel3.pixelState == 0:
            estado = "ROJO"
            pixel3.state = "WaitTimeout"
```
2.Identifica los estados, eventos y acciones en tu código.

Estados: En el codigo los estados corresponden a los colores del semáforo: ROJO, AMARILLO y VERDE.  Solo uno de los tres LED está encendido dependiendo del estado en el que se encuentre ya que hay una variable llamada estado que dependiendo del led encendido va cambiando el estado  y prendiendo otro led.

Eventos: Los eventos que hacen cambiar de un estado a otro son las condiciones que detectan si un LED se ha apagado. Esto indica que ha pasado el tiempo correspondiente para ese estado y cambiar al siguiente estado del semáforo.

Acciones: La accion es encender un led dependiendo del estado. Si el estado es igual a ROJO enciende led 1, si es AMARILLO enciende led 2 y si es VERDE enciende led 3.
