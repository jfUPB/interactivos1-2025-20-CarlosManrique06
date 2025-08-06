# Unidad 2


## 🛠 Fase: Apply

### Actividad 4


### Actividad 5

```py
# Imports go at the top
from microbit import *
import utime
import music

STATE_INIT = 0
STATE_ARMED = 1
STATE_BLOW = 2

ARMED_INTERVAL = 1000


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
              sleep(500)
              display.clear()
              print(start_time)
             
         if button_b.was_pressed():
             
             if start_time > 10000:
              display.show(menos)
              sleep(500)
              display.clear()
              start_time-= 1000
              print(start_time)
                 
         if accelerometer.was_gesture('shake'):

             music.play(music.BADDY)
             current_state = STATE_ARMED
             remaining = utime.ticks_ms()
           
             
     if current_state == STATE_ARMED:
                
         display.show(Image.CONFUSED)     
         sleep(500)
         display.clear()
         sleep(500)
         
         if utime.ticks_diff(utime.ticks_ms(), remaining) > start_time: 

             display.show(Image.SKULL)
             music.play(music.BA_DING)
             music.play(music.ODE)
             current_state = STATE_BLOW
             
     if current_state == STATE_BLOW:

         if pin_logo.is_touched():
            current_state = STATE_INIT
            start_time = 20000
            music.play(music.BA_DING)
            display.clear()
           
        
```

