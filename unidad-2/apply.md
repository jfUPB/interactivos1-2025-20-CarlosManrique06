# Unidad 2


## 🛠 Fase: Apply

### Actividad 4

![Diagrama_Bomba](https://github.com/user-attachments/assets/df5e74b0-46ac-4113-aa14-c905b2a0afff)


### Actividad 5

```py
# Imports go at the top
from microbit import *
import utime
import music
import speech

STATE_INIT = 0
STATE_ARMED = 1
STATE_BLOW = 2


current_state = STATE_INIT
start_time = 20000

remaining = 0

mas = Image("00900:"
            "00900:"
            "99999:"
            "00900:"
            "00900")

menos = Image("00000:"
              "00000:"
              "99999:"
              "00000:"
              "00000")





# Code in a 'while True:' loop repeats forever
while True:

     if current_state == STATE_INIT:
         
         if button_a.was_pressed():
              
             if start_time < 60000: 
              start_time+= 1000
              display.show(mas)
              music.play(['c:1'])
              display.clear()
              print(start_time)
             
         if button_b.was_pressed():
             
             if start_time > 10000:
              display.show(menos)
              start_time-= 1000
              display.show(menos)
              music.play(['e:1'])
              display.clear()
              print(start_time)
                 
         if accelerometer.was_gesture('shake'):

                
             display.scroll(start_time/1000)
             music.play(music.BADDY)
             current_state = STATE_ARMED
             remaining = utime.ticks_ms()
           
             
     if current_state == STATE_ARMED:
                
         display.show(Image.CONFUSED)
         
         music.play(['e5','',])
         
         display.clear()

         music.play(['e5', ''])
         
         if utime.ticks_diff(utime.ticks_ms(), remaining) > start_time: 

             speech.say('EXPLOSION')
             display.show(Image.SKULL)
             music.play(music.BA_DING)
             music.play(music.ODE)
             current_state = STATE_BLOW
             
     if current_state == STATE_BLOW:

         if pin_logo.is_touched():
            current_state = STATE_INIT
            start_time = 20000
            music.play(music.BA_DING)
            speech.say('START')
            display.clear()
           
        
        
```

2. La definición de los vectores de prueba básicos que permiten verificar el correcto funcionamiento del programa.

   Vector 1: Comienza en el state init y disminuyo 10 segundos a la bomba, hago un shake para ver si cambia de state init a state armed y comienza el tiempo en ms. Funciono de la manera descrita, vector aprobado.

   Vector 2: Desde el estado armed la cuenta regresiva se sigue dando mientras emite sonido y muestra una cara en la pantalla, cuando el tiemmpo sea mayor al de iniciacion que serian 10 segundos muestra una calavera y pasa al state blow. Funciono de la manera descrita, vector aprobado.

   Vector 3: Desde el state blow, presiono el touch del microbit y cambia al estado init emitiendo sonido. Funciono de la manera descrita, vector aprobado



