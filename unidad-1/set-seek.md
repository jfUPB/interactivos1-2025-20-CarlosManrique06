# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

¿Qué es un sistema físico interactivo?

R/ Es un sistema capaz de darle al usuario una interacción más inmersiva en tiempo real, En estos sistemas se usan los estímulos del alrededor para hacer que la interacción que tiene el usuario logre esa inmersion mediante el uso de estos estímulos en tiempo real. Funciona a través de inputs como sensores o botones que captan información, un proceso que analiza esos datos  y outputs como pantallas que muestran al usuario el resultado. 

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

R/ podria diseñar  videojuegos o proyectos más inmersivos mediante los estimulos sensoriales para reforzar lo que quisiera presentar en algun futuro proyecto, también diseñar diferentes sistemas interactivos que detecten los movimientos para ver como afecta la experiencia en un juego.

### Actividad 02

Qué es el diseño/arte generativo?

R/ El diseño generativo es un sistema donde utilizas un programa para realizar una obra casi o completa, buscando promocionar algo a comparacion del arte generativo que lo que busca es contar y narrar la historia que quiere mostrar el autor del arte generativo donde cada resultado del producto va ser unico cada vez que el sistema de un resultado dando un factor de aleatoridad gracias a los algoritmos realizados en el sistema.

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

R/ En mis proyectos podría utilizarlo para generar nuevos ambientes que se vayan cambiando en tiempo real de acuerdo a los estímulos que está recibiendo el usuario y utilizarlos por el progama de acuerdo a la reaccion del usuario o que el mismo usuario los pueda moldear a su gusto.

### Actividad 03

En este sistemas físico interactivo identifica los inputs, outputs y el proceso:

- Desde el microbit los inputs son los botones A, B y hacerle shake.

- Desde el microbit el output son la pantalla del computador por la pag P5.

- Desde el computador  el input es el boton send love.

- Desde el computador el output es la pantalla del microbit

 - Proceso: Cuando se presiona el boton A, la pantalla del computador donde está conctado el microbit da el resultado que se escriba a y se pone fondo rojo, cuando se presiona B que escriba b y se pone fondo amarillo y cuando se sacude que escriba C y se pone fondo verde. Por otro lado, en la web del microbit, si se presiona el botond send love, en la pantalla del microbit se mostrara primero un corazcon y luego una cara feliz.

### Actividad 04

### Generando patrones visuales

Link del programa: (<https://editor.p5js.org/CarlosManrique06/sketches/3IdXQ2uoW>)

```js
function setup() {
  createCanvas(600, 600);
  background(20);
  noStroke();
  
}

function draw() {
 
  let t = frameCount * 0.07;

  
  let offsetX = 200 * sin(t * 0.3); 
  let offsetY = 150 * cos(t * 0.2);  

  // Coordenadas del punto
  let x = 100 * cos(t) / (1 + sin(t) * sin(t)) + 300 + offsetX;
  let y = 100 * sin(t) * cos(t) / (1 + sin(t) * sin(t)) + 300 + offsetY;

  let r = random(255);
  let g = random(255);
  let b = random(255);


  fill(r, g, b, 150);
  ellipse(x, y, 6, 6);
}
```
![Programa](https://github.com/user-attachments/assets/ab962ef0-4251-4fe3-864e-cfefe674e46b)


