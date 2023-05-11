# PIDbox

### Goal/planning

For this project we chose to do a design simelar to Mr Dierolfs because it was well documented and their were many tutorials on how to do it. 
Out goal was to create a design that would ballence a ball directly in the middle using and ultrasonic sensor and servos.





![pidplannign](https://user-images.githubusercontent.com/71402974/232500023-27507196-46f4-4ddd-9c11-e0a9c3934b7b.png)



### Code

```python
import time
import board
import adafruit_hcsr04
from adafruit_motor import servo
import pwmio
from simple_pid import PID


# pid = PID(1, 0.1, 0.05, setpoint=1)

# Assume we have a system we want to control in controlled_system
# v = controlled_system.update(0)


pwm = pwmio.PWMOut(board.A1, duty_cycle=2 ** 15, frequency=50)
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D6, echo_pin=board.D7, timeout=0.1)
setpoint=20
my_servo = servo.Servo(pwm)

# adjust kP, kI, kD to tune the PID controller
pid = PID(.7, .1, 0, setpoint=setpoint, output_limits=(-40, 40))

# grab initial value
input = sonar.distance

while True:
    distance = 0
    # first measure distance
    try:
        distance = sonar.distance
        print((distance,))
        time.sleep(0.1)
    except RuntimeError:
        print("Retrying!")
        time.sleep(0.1)

    # # use if statements to compare distance to setpoint and move servo
    # if distance > setpoint:
    #     print("greater than setpoint")
    #     my_servo.angle = 120
    # elif distance < setpoint:
    #     print("less than setpoint")      
    #     my_servo.angle = 40
    # else:
    #     print("at setpoint") 
    #     my_servo.angle = 90  
    # 
    ## Compute new output from the PID according to the systems current value
    output = pid(sonar.distance)
    print('PID Output: ', output)
    print('Servo Angle: ', output+90)

    my_servo.angle = output + 90
        


```
### Cad



### parts




### Reflection

