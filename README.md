# PIDbox

### Goal/planning

For this project we chose to do a design similar to Mr Dierolfs because it was well documented and their were many tutorials on how to do it. 
Out goal was to create a design that would balance a ball directly in the middle using and ultrasonic sensor and servos. 





![pidplannign](https://user-images.githubusercontent.com/71402974/232500023-27507196-46f4-4ddd-9c11-e0a9c3934b7b.png)

This was our first idea and sketch where a servo located on the base you have a string or something to control the chamber.


For this project we didn't have a planning document but we decided to make a finish date for all the different parts of the project.

Onshape finished by 5/12 so that we have time to make changes.

Build done by 5/17 so that we can have a quick start on PID and make sure that everything works as it should.

Code First prototype should be done by 5/18 so that we can have a lot of time to test the code.

Our work should be done 5/31 and thats when we should do documentation. we did documentation throughout so that we could have more time on the project.

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

### Evidence
[Onshape Link](https://cvilleschools.onshape.com/documents/7c87217263b0a725d3512c0e/w/d04d77d161baa69265bfc1db/e/c6bb2c1666ca8a2d2c29ad5d)

[Bill of Materials](https://docs.google.com/document/d/1J53i04ptv5_mM0lnMhT_mGYdmYwtcKZW3SEIHETr12E/edit)



https://github.com/willhunt914/PIDBOX/assets/112961434/8d510ab7-2464-4e5e-adf6-877d366d688f


This is a video of the first time we got our PID to work.

### Images

![Screenshot 2023-05-18 154910](https://github.com/willhunt914/PIDBOX/assets/112961434/97cc8196-3556-4fc6-85b0-99e43942295c)

This view shows where the light and switch will go, and also shows where the battery pack is held.

![Screenshot 2023-05-18 154842](https://github.com/willhunt914/PIDBOX/assets/112961434/d15d83bb-8c6f-4863-bb55-db3a7626f89a)

This picture shows the isometric viewpoint which shows how the servo is positioned and where it hooks onto the ball chamber.

![Screenshot 2023-05-18 154829](https://github.com/willhunt914/PIDBOX/assets/112961434/3d010b23-4162-4270-831f-e4633b3f571c)

Friction fit+ t-slots allowed or us to quickly put the box together and take it apart.
### Problem #1

![PIDBOX#3](https://github.com/willhunt914/PIDBOX/assets/112961434/cd20c6a7-7a55-4461-ada8-b235ba777d57)

Our first CAD problem came when the original axel design didn't work beacuse the way to attatch the axel to the chamber was through screw holes which interuppted the movement of the ball which stopped us from getting good readings.
### Solution

Our solution was...

![Screenshot 2023-05-22 093548](https://github.com/willhunt914/PIDBOX/assets/112961434/e1c62af7-ee5a-4057-9c3b-59204c726199)

Moving where the axel was connected on the chamber from the bottom to the sides so it had more stability and didn't interupt ball movements.


### Reflection

