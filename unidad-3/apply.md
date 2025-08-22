# Unidad 3


## 🛠 Fase: Apply

### Actividad 6
- El código fuente de la bomba en p5.js.

```js
let bomb;

class BombTask {
  constructor() {
    this.PASSWORD = ['A','B','A'];
    this.key = new Array(this.PASSWORD.length).fill('');
    this.keyindex = 0;
    this.count = 20;
    this.startTime = millis();
    this.state = 'CONFIG';
  }

  update() {   
    background(0);  
    fill(255);
    textSize(32);
    textAlign(CENTER, CENTER);

    if (this.state === 'CONFIG') {
      text("Tiempo: " + this.count, width/2, height/2);

  
      textSize(16);
      text("Aumentar tiempo: tecla A\nDisminuir tiempo: tecla B\nArmar: tecla espacio", width/2, height/2 + 80);

    } else if (this.state === 'ARMED') {
     
      if (millis() - this.startTime > 1000) {
        this.startTime = millis();
        this.count--;
      }

      text("Tiempo: " + this.count, width/2, height/2);

      if (this.count <= 0) {
        this.state = 'EXPLODED';
      }

      textSize(16);
      text("Ingresa clave con teclas A/B", width/2, height/2 + 80);

    } else if (this.state === 'EXPLODED') {
      fill(255, 0, 0);
      text("EXPLOSION ", width/2, height/2);

      textSize(16);
      fill(255);
      text("Haz clic para reiniciar", width/2, height/2 + 80);
    }
  }

  keyPressed(k) {
    if (this.state === 'CONFIG') {
      if (k === 'a' || k === 'A') {
        this.count = min(this.count + 1, 60);
      } else if (k === 'b' || k === 'B') {
        this.count = max(10, this.count - 1);
      } else if (k === ' ') { 
        this.startTime = millis();
        this.state = 'ARMED';
      }
    } 
    else if (this.state === 'ARMED') {
      if (k === 'a' || k === 'A') {
        this.key[this.keyindex] = 'A';
        this.keyindex++;
      } else if (k === 'b' || k === 'B') {
        this.key[this.keyindex] = 'B';
        this.keyindex++;
      }

      if (this.keyindex === this.key.length) {
        let passIsOK = true;
        for (let i = 0; i < this.key.length; i++) {
          if (this.key[i] !== this.PASSWORD[i]) {
             
            passIsOK = false;
           
            break;
          }
        }
        if (passIsOK) {
          this.count = 20;
          this.keyindex = 0;
          this.state = 'CONFIG';
        } else {
          this.keyindex = 0; 
        }
      }
    }
  }

  mousePressed() {
    if (this.state === 'EXPLODED') {
      this.count = 20;
      this.startTime = millis();
      this.state = 'CONFIG';
    }
  }
}

function setup() {
  createCanvas(400, 400);
  bomb = new BombTask();
}

function draw() {
  bomb.update();
}

function keyPressed() {
  bomb.keyPressed(key);
}

function mousePressed() {
  bomb.mousePressed();
}


```
