
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


![Diagrama Servidor](https://github.com/user-attachments/assets/f89f4815-8d36-4a4a-b420-bf2ce849b63d)


### Actividad 5-Apply

#### Diseña una aplicación interactiva que use el touch del móvil para controlar una visuales de tema musical de tu elección. Las visuales correrán en una aplicación de escritorio (desktop). Recuerda que ambas aplicaciones las construirás usando p5.js y utilizando el servidor Node.js como puente.


- Implementa tu diseño. Puedes usar IA generativa para ayudarte a escribir el código, pero primero debes hacer el diseño de lo que quieres.

Para implementar el diseño que tenía pensado solo necesite cambiar el sketch.js del desktop, los demás códigos los deje igual.

Para poner la canción agregue la biblioteca de p5 de audio en el html del desktop, guarde la cancion en la carpeta assets y para iniciar la cancion cree un boton.

<img width="290" height="79" alt="image" src="https://github.com/user-attachments/assets/2c823858-6a80-42e0-9c98-f12656289e1a" />

```html
 <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/addons/p5.sound.min.js"></script>
<button id="playBtn" style="position:fixed; top:10px; left:10px; z-index:999;">
  ▶ Reproducir Música
```

[Link para descargar la cancion](https://drive.google.com/file/d/1sAEqVWgI6VJ1b-O0y1chGnKfXTebONna/view?usp=sharing)



#### sketch.js del desktop

```js

// desktop.js - Visuales del desierto


let socket;
let touchX = 0.5;     // normalizado 0..1 internamente
let touchY = 0.5;
let targetX = 0.5;
let targetY = 0.5;
let velocity = 0;

let song = null;
let playing = false;
let amplitude = null;
let fft = null;

let roadOffset = 0;
let stars = [];
let cacti = [];
let mountains = [];
let tumbleweeds = [];
let dustParticles = [];
let heatWave = [];

// Tamaño del canvas origen del móvil si manda coordenadas absolutas
const SOURCE_CANVAS_W = 300;
const SOURCE_CANVAS_H = 400;

function preload() {
 
  song = loadSound('assets/silver_line.wav');
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  angleMode(DEGREES);
  background(25);

  // iniciar elementos del entorno
  for (let i = 0; i < 80; i++) stars.push({ x: random(width), y: random(height * 0.55), s: random(1,3), t: random(TWO_PI) });

 // Cactus: ubicados en las banquinas (zonas amarillas) del desierto
const perSide = 7;
const leftBandX = width * 0.12;   // borde interno del suelo izquierdo (banquina)
const rightBandX = width * 0.88;  // borde interno del suelo derecho
const bandWidth = width * 0.08;   // ancho aprox de cada banquina

for (let i = 0; i < perSide; i++) {
  // LADO IZQUIERDO
  cacti.push({
    x: random(leftBandX - bandWidth, leftBandX - 10),
    y: height * random(0.78, 0.88),   // más abajo, sobre el suelo
    size: random(30, 55),
    arms: floor(random(1, 3)),
    side: -1
  });

  // LADO DERECHO
  cacti.push({
    x: random(rightBandX + 10, rightBandX + bandWidth),
    y: height * random(0.78, 0.88),
    size: random(30, 55),
    arms: floor(random(1, 3)),
    side: 1
  });
}





  // montañas
  for (let i = 0; i < 4; i++) {
    let layer = [];
    for (let j = 0; j < 4; j++) {
      layer.push({ x: j * width / 3 + random(-80, 80), height: random(90, 180), w: random(160, 320) });
    }
    mountains.push(layer);
  }

  for (let i = 0; i < 6; i++) tumbleweeds.push(new Tumbleweed());
  for (let i = 0; i < 40; i++) heatWave.push({ x: random(width), offset: random(TWO_PI), speed: random(0.02, 0.06) });

  // socket - escucha 'message' (compatible con tu cliente inicial)
  if (typeof io === 'undefined') {
    console.error('Socket.IO client missing. Asegúrate de incluir /socket.io/socket.io.js');
  } else {
    socket = io();

    socket.on('connect', () => {
      console.log('Connected to server');
      const s = document.getElementById('status');
      if (s) s.textContent = '✓ Conectado';
    });

    socket.on('message', (data) => {
      if (!data) return;
      // aceptar {type:'touch', x:, y:} o {x:, y:}
      if (data.type === 'touch' || (typeof data.x !== 'undefined' && typeof data.y !== 'undefined')) {
        if (data.x <= 1 && data.y <= 1) {
          targetX = constrain(data.x, 0, 1);
          targetY = constrain(data.y, 0, 1);
        } else {
          targetX = constrain(data.x / SOURCE_CANVAS_W, 0, 1);
          targetY = constrain(data.y / SOURCE_CANVAS_H, 0, 1);
        }
      }
      if (typeof data.velocity === 'number') {
        velocity = constrain(data.velocity, 0, 5);
      } else {
        // estimación opcional: velocidad por cambio (simple)
        // velocity = dist(targetX, targetY, touchX, touchY) * 10;
      }

      const xEl = document.getElementById('touchX');
      const yEl = document.getElementById('touchY');
      if (xEl) xEl.textContent = targetX.toFixed(2);
      if (yEl) yEl.textContent = targetY.toFixed(2);
    });

    socket.on('disconnect', () => {
      console.log('Disconnected from server');
      const s = document.getElementById('status');
      if (s) s.textContent = '● Desconectado';
    });

    socket.on('connect_error', (err) => console.error('Socket.IO error', err));
  }

  // audio analyzer si hay audio
  if (song && typeof p5.Amplitude === 'function') {
    amplitude = new p5.Amplitude();
    fft = new p5.FFT();
  }

  // inicializar variables
  touchX = targetX;
  touchY = targetY;

  // boton play defensivo
  const playBtn = document.getElementById('playBtn');
  if (playBtn) playBtn.addEventListener('click', toggleMusic);
}

function draw() {
  // suavizado
  touchX = lerp(touchX, targetX, 0.12);
  touchY = lerp(touchY, targetY, 0.12);

  let level = 0, bass = 0, treble = 0;
  if (amplitude && playing) {
    level = amplitude.getLevel();
    bass = fft.getEnergy('bass') / 255;
    treble = fft.getEnergy('treble') / 255;
  }

  const timeOfDay = touchY; // 0..1

  // dibujar escena
  drawSky(timeOfDay, level);
  drawStars(timeOfDay);
  drawSunAndMoon(timeOfDay, level);
  drawMountains(timeOfDay, bass);
  drawGround(timeOfDay);
  drawRoad(level, bass, velocity, touchX);
  drawCacti(timeOfDay);
  drawHeatHaze();
  drawDust();
  drawTumbleweeds(level, treble);

  // movimiento carretera
  roadOffset += (velocity * 6) + (touchX - 0.5) * 4;
}

/* ---------- helpers visuales ---------- */

function drawSky(t, level) {
  let top = lerpColor(color(15, 18, 40), color(200, 220, 255), t);
  let bottom = lerpColor(color(30, 18, 45), color(255, 240, 200), t);
  for (let y = 0; y < height * 0.7; y++) {
    let f = map(y, 0, height * 0.7, 0, 1);
    stroke(lerpColor(top, bottom, f));
    line(0, y, width, y);
  }
}

function drawStars(t) {
  if (t < 0.5) {
    noStroke();
    for (let s of stars) {
      let a = map(t, 0, 0.5, 255, 0) * (0.6 + 0.4 * sin(frameCount * 0.02 + s.t));
      fill(255, a);
      ellipse(s.x, s.y, s.s);
    }
  }
}

function drawSunAndMoon(t, level) {
  if (t > 0.45) {
    // Sol
    let sy = map(t, 0.45, 1, height * 0.8, height * 0.2);
    let base = color(255, 210, 120);
    noStroke();
    for (let i = 0; i < 6; i++) {
      let a = map(i, 0, 5, 80, 0) + level * 40;
      fill(255, 200, 100, a);
      ellipse(width * 0.82, sy, 160 + i * 40 + level * 80);
    }
    fill(base);
    ellipse(width * 0.82, sy, 100 + level * 40);
  } else {
    // Luna con pulso
    let my = map(t, 0, 0.45, height * 0.2, height * 0.8);
    let pulse = 1 + level * 0.6; // vibración ligera
    noStroke();
    fill(240, 245, 255, 220);
    ellipse(width * 0.82, my, 90 * pulse, 90 * pulse);
    fill(200, 210, 220, 160);
    ellipse(width * 0.82 + 12, my - 6, 18 * pulse, 12 * pulse);
    ellipse(width * 0.82 - 20, my + 10, 12 * pulse, 10 * pulse);
    ellipse(width * 0.82 + 25, my + 18, 10 * pulse, 8 * pulse);
  }
}

function drawMountains(t, bass) {
  noStroke();

  // Nivel de audio (solo si hay música)
  let level = (amplitude && playing) ? amplitude.getLevel() : 0;

  // Altura base modificada por el touchY
  // touchY bajo = montañas más altas (noche)
  // touchY alto = montañas más bajas (día)
  let heightMod = map(touchY, 0, 1, 1.4, 0.7);

  for (let i = 0; i < mountains.length; i++) {
    let depthFactor = 1 - i * 0.25;

    // Color según el tiempo del día
    let col = lerpColor(
      color(90, 70, 60),
      color(230, 190, 130),
      constrain(t - i * 0.05, 0, 1)
    );
    fill(col);

    // Vibración suave por la música (solo si suena)
    let vib = 0;
    if (playing && amplitude) {
      vib = sin(frameCount * 2 + i * 40) * level * 50 * depthFactor;
    }

    push();
    translate(0, vib);

    beginShape();
    vertex(0, height * 0.7);

    // Forma ondulada natural con ruido y altura modulada por touchY
    for (let x = 0; x <= width; x += 8) {
      let n = noise(x * 0.01 + i * 10, frameCount * 0.008 * (playing ? 1 : 0));
      let peak = map(n, 0, 1, 80, 200) * depthFactor * heightMod;
      vertex(x, height * 0.7 - peak);
    }

    vertex(width, height);
    vertex(0, height);
    endShape(CLOSE);
    pop();
  }
}







function drawGround(t) {
  noStroke();
  fill(lerpColor(color(80,60,40), color(220,180,110), t));
  rect(0, height * 0.7, width, height * 0.3);
}

function drawCacti(t) {
  noStroke();
  let level = amplitude ? amplitude.getLevel() : 0;
  for (let c of cacti) {
    let parallax = (touchX - 0.5) * c.side * 20;
    let vib = sin(frameCount * 10 + c.x * 0.1) * level * 15; // vibración con música
    fill(lerpColor(color(40, 75, 40), color(100, 150, 80), t));
    push();
    translate(c.x + parallax, c.y + vib);
    rect(-6, -c.size, 12, c.size, 4);

    for (let i = 0; i < c.arms; i++) {
      let armY = -c.size * (0.3 + i * 0.25);
      let dir = i % 2 === 0 ? 1 : -1;
      rect(dir * 6, armY - 6, 10 * dir, 10, 3);
    }
    pop();
  }
}


// Carretera mejorada: la línea central está más centrada y consistente
function drawRoad(level, bass, vel, normX) {
  let roadTopY = height * 0.72;
  let roadBottomY = height;

  // base road trapezoide con sutil curvatura controlada por normX
  const leftTopX = width * 0.28;
  const rightTopX = width * 0.72;
  const curve = map(normX, 0, 1, -40, 40);

  noStroke();
  fill(28);
  beginShape();
  vertex(leftTopX, roadTopY + curve * 0.15);
  vertex(rightTopX, roadTopY - curve * 0.15);
  vertex(width * 0.86, roadBottomY);
  vertex(width * 0.14, roadBottomY);
  endShape(CLOSE);

  // Banquinas (shoulders)
  fill(60, 50, 40);
  beginShape();
  vertex(leftTopX - 30, roadTopY + curve * 0.2);
  vertex(rightTopX + 30, roadTopY - curve * 0.2);
  vertex(width * 0.9, roadBottomY);
  vertex(width * 0.1, roadBottomY);
  endShape(CLOSE);

  // Línea central (silver line) - centrada y con segmentos uniformes
  stroke(220, 220, 230, 220 + level * 35);
  strokeWeight(4 + level * 6);
  let segs = 36;
  // punto central superior y central inferior, con pequeño offset por curve
  let centerTopX = (leftTopX + rightTopX) / 2 + curve * 0.1;
  let centerBottomX = width / 2 + curve * 0.6;
  for (let i = 0; i < segs; i++) {
    let t1 = i / segs;
    let t2 = (i + 1) / segs;
    let x1 = lerp(centerTopX, centerBottomX, t1) + sin((roadOffset + i * 12) * 0.05) * 4;
    let y1 = lerp(roadTopY + curve * 0.12, roadBottomY, t1);
    let x2 = lerp(centerTopX, centerBottomX, t2) + sin((roadOffset + (i+1) * 12) * 0.05) * 4;
    let y2 = lerp(roadTopY + curve * 0.12, roadBottomY, t2);

    // alternar visibilidad para crear efecto de segmentos
    let phase = (roadOffset + i * 18) % 90;
    if (phase < 45) line(x1, y1, x2, y2);
  }

  // pequeñas marcas laterales (para profundidad)
  stroke(80, 80, 80, 160);
  strokeWeight(1);
  for (let i = 0; i < 8; i++) {
    let t = i / 8;
    let lx = lerp(leftTopX - 10, width * 0.14, t);
    let rx = lerp(rightTopX + 10, width * 0.86, t);
    let ly = lerp(roadTopY, roadBottomY, t);
    line(lx, ly, lx + 6, ly + 10);
    line(rx, ly, rx - 6, ly + 10);
  }
}

function drawHeatHaze() {
  noFill();
  stroke(255, 255, 255, 14);
  for (let w of heatWave) {
    w.offset += w.speed;
    beginShape();
    for (let i = 0; i < 20; i++) {
      curveVertex(w.x + i * 6 + sin(w.offset + i * 0.3) * 3, height * 0.73 + sin(w.offset + i * 0.1) * 6);
    }
    endShape();
  }
}

function drawDust() {
  for (let i = dustParticles.length - 1; i >= 0; i--) {
    dustParticles[i].update();
    dustParticles[i].display();
    if (dustParticles[i].isDead()) dustParticles.splice(i, 1);
  }
}

function drawTumbleweeds(level, treble) {
  for (let t of tumbleweeds) {
    t.update(touchX, level, treble);
    t.display();
  }
}

/* ---- clases ---- */
class Tumbleweed {
  constructor() { this.reset(); }
  reset() { this.x = random(width); this.y = height * 0.72; this.size = random(24,56); this.speed = random(0.6,1.6); this.rot = 0; }
  update(wind, lvl, tr) {
    this.x += this.speed + (wind - 0.5) * 3 + tr * 2;
    this.rot += 0.5 + lvl * 2;
    if (this.x > width + this.size) this.x = -this.size;
  }
  display() {
    push(); translate(this.x, this.y); rotate(this.rot); noFill(); stroke(120,80,40);
    for (let i = 0; i < 8; i++) line(0,0,cos(i * 45) * this.size / 2, sin(i * 45) * this.size / 2);
    pop();
  }
}

class DustParticle {
  constructor() { this.x = random(width); this.y = random(height * 0.7, height); this.vx = random(-1, 1); this.vy = random(-2, -0.5); this.life = 200; }
  update() { this.x += this.vx + (touchX - 0.5) * 1.2; this.y += this.vy; this.vy += 0.03; this.life -= 3; }
  display() { noStroke(); fill(220, 180, 120, this.life); ellipse(this.x, this.y, random(2,6)); }
  isDead() { return this.life <= 0; }
}

/* --- audio toggle (defensivo) --- */
function toggleMusic() {
  if (!song) { alert('No se cargó audio (assets/silver_line.mp3)'); return; }
  if (!playing) { song.loop(); playing = true; document.getElementById('playBtn') && (document.getElementById('playBtn').textContent = '⏸ Pausar Música'); }
  else { song.pause(); playing = false; document.getElementById('playBtn') && (document.getElementById('playBtn').textContent = '▶ Reproducir Música'); }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  // reposicionar elementos si hace falta (simple)
  for (let s of stars) { s.x = random(width); s.y = random(height * 0.55); }
}

```


