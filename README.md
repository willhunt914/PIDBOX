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

Our work should be done 5/31 and thats when we should do documentation. We did documentation throughout so that we could have more time on the project.

### Code

```python
import time
import board
import adafruit_hcsr04
from adafruit_motor import servo
import pwmio
from simple_pid import PID
# import necessary libraries


pwm = pwmio.PWMOut(board.A1, duty_cycle=2 ** 15, frequency=50)
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D6, echo_pin=board.D7, timeout=0.1)
setpoint=13 #sets middle point
my_servo = servo.Servo(pwm)
#sets pins for servo and ultrasonic sensor 



pid = PID(8, 3, 0, setpoint=setpoint, output_limits=(10, 175)) # adjust kP, kI, kD to tune the PID controller


while True:
    distance = 0
    # first measure distance
    try:
        distance = sonar.distance
        time.sleep(0.1)
    except RuntimeError:
        print("Retrying!")
        time.sleep(0.1)

    # use this code to check servo without PID
    # # use if statements to compare distance to setpoint and move servo
    # if distance > setpoint:
    #     print("greater than setpoint")
    #     my_servo.angle = 120
    # elif distance < setpoint:
    #     print("less than setpoint")      
    #     my_servo.angle = 40
    # else:
    #     print("at setpoint") 

    
    
    if distance > 29:
        my_servo.angle = 175
        time.sleep(0.1) # this is used to get the servo away from the ultrasonic sensor when it is too close 
    else:
        output = pid(distance)

        my_servo.angle = output
    p,i,d = pid.components
    my_servo.angle = (180-output)
    time.sleep(0.1)

```

### Code Reflection

Possibly the hardest part of this project was the code. To create this code I peiced together code from my past asignments. At first, I created a code that would move back if it was greater than the setpoint, forward if it was less that the setpoint or stay still if it was directly at the setpoint. I later imported the PID Code and pid libraries. It was important to find the minimum and maximum point for the PID code.

### Evidence
[Onshape Link](https://cvilleschools.onshape.com/documents/7c87217263b0a725d3512c0e/w/d04d77d161baa69265bfc1db/e/c6bb2c1666ca8a2d2c29ad5d)

[Bill of Materials](https://docs.google.com/document/d/1J53i04ptv5_mM0lnMhT_mGYdmYwtcKZW3SEIHETr12E/edit)



https://github.com/willhunt914/PIDBOX/assets/112961434/8d510ab7-2464-4e5e-adf6-877d366d688f


This is a video of the first time we got our PID to work.

## Cad

### Images

![Screenshot 2023-05-18 154910](https://github.com/willhunt914/PIDBOX/assets/112961434/97cc8196-3556-4fc6-85b0-99e43942295c)

This view shows where the light and switch will go, and also shows where the battery pack is held.

![Screenshot 2023-05-18 154842](https://github.com/willhunt914/PIDBOX/assets/112961434/d15d83bb-8c6f-4863-bb55-db3a7626f89a)

This picture shows the isometric viewpoint which shows how the servo is positioned and where it hooks onto the ball chamber.

![Screenshot 2023-05-18 154829](https://github.com/willhunt914/PIDBOX/assets/112961434/3d010b23-4162-4270-831f-e4633b3f571c)

Friction fit+ t-slots allowed or us to quickly put the box together and take it apart.





### Reflection (includes problems and solutions)
The CAD, while it might seem easier than the code for this project is actually a crucial piece which insures that all the code can run smoothly and the project functions as it should. Our time management was  lot better this project and we weren't rushed and we knew if we stayed focused we could finish the project on time. I learned that having a very solid plan at the start is important and to be able to adapt still. There was one instance of me not thinking ahead and so when a piece came it didn't work like I thought because I didn't think of it in a logical sense at the time.


### Problem #1

![PIDBOX#3](https://github.com/willhunt914/PIDBOX/assets/112961434/cd20c6a7-7a55-4461-ada8-b235ba777d57)

Our first CAD problem came when the original axel design didn't work beacuse the way to attatch the axel to the chamber was through screw holes which interuppted the movement of the ball which stopped us from getting good readings.
### Solution #1

Our solution was...

![Screenshot 2023-05-22 093548](https://github.com/willhunt914/PIDBOX/assets/112961434/e1c62af7-ee5a-4057-9c3b-59204c726199)

Moving where the axel was connected on the chamber from the bottom to the sides so it had more stability and didn't interupt ball movements.


### Problem 2

<img src="https://github.com/willhunt914/PIDBOX/assets/112961434/d3b54ae3-1375-4a07-a4a5-2d41a0973268" alt="Old Wire" width="500" height="600">

Our original wire bent and twisted which made the PID very hard to balance and led to bad readings.

### Solution 2
<img src="https://github.com/willhunt914/PIDBOX/assets/112961434/c6d6ecbf-95f3-44d2-9823-a3ff049083af" alt="new wire" width="500" height="600">

 
 
 Our new idea was to use a very strong wire which didn't bend at all.

### Mistep #1
One mistep was putting the battery pack on the side which led to the whole thing being unbalanced.

### Solution #1 
I had to put holes on the bottom for screws in order to balance it for the PID values.

### Mistep #2
Another mistake was putting the servo so close to the ground which made the servo horn hit the base. 

### Solution #2
I put nuts in between the servo and the servo holder so that it would add space and allow for the srvo horn to work.



