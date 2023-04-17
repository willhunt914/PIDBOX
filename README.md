# PIDbox

### Goal/planning

For this project we chose to do a design simelar to Mr Dierolfs because it was well documented and their were many tutorials on how to do it. 
Out goal was to create a design that would ballence a ball directly in the middle using and ultrasonic sensor and servos.





![pidplannign](https://user-images.githubusercontent.com/71402974/232500023-27507196-46f4-4ddd-9c11-e0a9c3934b7b.png)



### Code

```python
#PID controller system with CircuitPython
# https://srituhobby.com

import time
import board
import pulseio
import adafruit_hcsr04
import analogio
import math

servo = pulseio.PWMOut(board.D5, duty_cycle=0, frequency=50) # set up PWM output for servo on pin D5
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D2, echo_pin=board.D3) # set up HC-SR04 ultrasonic sensor on pins D2 and D3
kp = 0 # initialize PID constants
ki = 0
kd = 0
priError = 0 # initialize previous error and total error
toError = 0

def PID():
    global priError, toError # use global variables for previous error and total error
    dis = sonar.distance # measure distance with ultrasonic sensor

    setP = 15 # set target distance
    error = setP - dis # calculate error

    Pvalue = error * kp # calculate proportional component
    Ivalue = toError * ki # calculate integral component
    Dvalue = (error - priError) * kd # calculate derivative component

    PIDvalue = Pvalue + Ivalue + Dvalue # calculate total PID output
    priError = error # update previous error
    toError += error # update total error
    print(PIDvalue) # print PID output for debugging

    Fvalue = int(PIDvalue) # convert PID output to integer

    Fvalue = math.map_range(Fvalue, -135, 135, 0, 65535) # map PID output to servo PWM duty cycle

    if Fvalue < 0: # limit servo PWM duty cycle to within valid range
        Fvalue = 0
    if Fvalue > 65535:
        Fvalue = 65535

    servo.duty_cycle = Fvalue # set servo PWM duty cycle to control servo position

while True:
    PID() # run PID loop
    time.sleep(0.1) # wait before next iteration
```
### Cad



### parts




### Reflection

