# Unidad 2


## 🛠 Fase: Apply

### Actividad 4


### Actividad 5

```py
# Imports go at the top
from microbit import *
import utime

STATE_INIT = 0
STATE_ARMED = 1
STATE_BLOW = 2

ARMED_INTERVAL = 1000


current_state = STATE_INIT
start_time = 20000
interval = 0


# Code in a 'while True:' loop repeats forever
while True:
     if current_state == STATE_INIT:
         
         if button_a.was_pressed():

             if start_time < 60000: 
              start_time+= 1000
              print(start_time)
             
         if button_b.was_pressed():
             
             if start_time > 10000: 
              start_time-= 1000
              print(start_time)
                 
         if accelerometer.was_gesture('shake'):
             current_state = STATE_ARMED
             
     if current_state == STATE_ARMED:
         start_time = utime.ticks_ms()
         print(start_time)

         if start_time <= 0:
             current_state = STATE_BLOW
             
           
             
     if current_state == STATE_ARMED:
         print(current_state)
             
             
         
        

```
