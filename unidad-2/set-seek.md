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
