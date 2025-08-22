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
    this.Key = null; 
  }

  update() {   
    background(50);  
    fill(255);
    textSize(32);
    textAlign(CENTER, CENTER);


    if (this.state == 'CONFIG') {
      textSize(40);
      text("Tiempo" + "\n\n" + this.count, width/2, 110);
      textSize(25);
      text("Aumentar tiempo: A\nDisminuir tiempo: B\nArmar: T", width/2, height/2 + 80);

      if (this.Key) {
        if (this.Key == 'A') this.count = min(this.count + 1, 60);
        else if (this.Key == 'B') this.count = max(10, this.count - 1);
        else if (this.Key == 'T') {
          this.startTime = millis();
          this.state = 'ARMED';
        }
        this.Key = null; 
      }
    } 
    
   
    else if (this.state == 'ARMED') {
      if (millis() - this.startTime > 1000) {
        this.startTime = millis();
        this.count--;
      }
      textSize(80);
      text(this.count, width/2, height/2);
      textSize(16);
      text("Ingresa clave con teclas A/B", width/2, height/2 + 80);

      if (this.count <= 0) {
        this.state = 'EXPLODED';
      }

      if (this.Key) {
        if (this.Key == 'A' || this.Key == 'B') {
          this.key[this.keyindex] = this.Key;
          this.keyindex++;
        }

        if (this.keyindex == this.key.length) {
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
            this.key = new Array(this.PASSWORD.length).fill('');
            this.state = 'CONFIG';
          } else {
            this.keyindex = 0;
            this.key = new Array(this.PASSWORD.length).fill('');
          }
        }
        this.Key = null; 
      }
    } 
    

    else if (this.state == 'EXPLODED') {
      fill(255, 0, 0);
      text("EXPLOSION", width/2, height/2);
      textSize(16);
      fill(255);
      text("Reiniciar con T", width/2, height/2 + 80);

      if (this.Key == 'T') {
        this.count = 20;
        this.startTime = millis();
        this.state = 'CONFIG';
        this.Key = null; 
      }
    }
  }

  keyPressed(k) {
    this.Key = k.toUpperCase(); 
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

```

### Actividad 7

- Código controlador del microbit.
```py
from microbit import *

while True:
    if button_a.was_pressed():
        uart.write("A")  
    if button_b.was_pressed():
        uart.write("B")  
    if accelerometer.was_gesture("shake"):
        uart.write("S")  
    if pin_logo.is_touched():
        uart.write("T")  

```

Codigo Para eventos:

```js

let bombTask, keyTask, event;

class Evento {
  constructor() {
    this.value = null;
  }
  set(val) {
    this.value = val;
  }
  clear() {
    this.value = null;
  }
  read() {
    return this.value;
  }
}

class KeyTask {
  constructor() {}
  update() {
  
  }
  Key(k) {
    event.set(k.toUpperCase());
  }
}

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
    background(50);  
    fill(255);
    textSize(32);
    textAlign(CENTER, CENTER);

    if (this.state == 'CONFIG') {
      textSize(40);
      text("Tiempo" + "\n\n" + this.count, width/2, 110);
      textSize(25);
      text("Aumentar tiempo: A\nDisminuir tiempo: B\nArmar: T", width/2, height/2 + 80);

      if (event.read() == 'A') {
        event.clear();
        this.count = min(this.count+1,60);
      }
      else if (event.read() == 'B') {
        event.clear();
        this.count = max(10,this.count-1);
      }
      else if (event.read() == 'T') {
        event.clear();
        this.startTime = millis();
        this.state = 'ARMED';
      }
    }

    else if (this.state == 'ARMED') {
      if (millis() - this.startTime > 1000) {
        this.startTime = millis();
        this.count--;
      }
      textSize(80);
      text(this.count, width/2, height/2);
      textSize(16);
      text("Ingresa clave con teclas A/B", width/2, height/2 + 80);

      if (this.count <= 0) {
        this.state = 'EXPLODED';
      }

      if (event.read() == 'A') {
        event.clear();
        this.key[this.keyindex] = 'A';
        this.keyindex++;
      }
      else if (event.read() == 'B') {
        event.clear();
        this.key[this.keyindex] = 'B';
        this.keyindex++;
      }

      if (this.keyindex == this.key.length) {
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
          this.key = new Array(this.PASSWORD.length).fill('');
          this.state = 'CONFIG';
        } else {
          this.keyindex = 0;
          this.key = new Array(this.PASSWORD.length).fill('');
        }
      }
    }

    else if (this.state == 'EXPLODED') {
      fill(255, 0, 0);
      text("EXPLOSION", width/2, height/2);
      textSize(16);
      fill(255);
      text("Reiniciar con T", width/2, height/2 + 80);

      if (event.read() == 'T') {
        event.clear();
        this.count = 20;
        this.startTime = millis();
        this.state = 'CONFIG';
      }
    }
  }
}

function setup() {
  createCanvas(400, 400);
  event = new Evento();
  keyTask = new KeyTask();
  bombTask = new BombTask();
}

function draw() {
  bombTask.update();
}

function keyPressed() {
  keyTask.Key(key);
}


```

