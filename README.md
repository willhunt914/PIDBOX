# PIDbox

### Goal/planning

For this project we chose to do a design similar to Mr Dierolfs because it was well documented and their were many tutorials on how to do it. 
Our goal was to create a design that would balance a ball directly in the middle using and ultrasonic sensor and servos. 





![pidplannign](https://user-images.githubusercontent.com/71402974/232500023-27507196-46f4-4ddd-9c11-e0a9c3934b7b.png)

This was our first idea and sketch where a servo located on the base you have a string or something to control the chamber.


For this project we didn't have a planning document but we decided to make a finish date for all the different parts of the project.

Onshape finished by 5/12 so that we have time to make changes.

Build done by 5/17 so that we can have a quick start on PID and make sure that everything works as it should.

Code First prototype should be done by 5/18 so that we can have a lot of time to test the code.

Our work should be done 5/31 and thats when we should do documentation. We did documentation throughout the project so that we could have more time to work.

One problem we anticipated was not having enough time to document. We decided to do the documentation throughout the project instead of at the end so we would have enough time.

### Code

```python
# import necessary libraries
import time
import board
import adafruit_hcsr04
from adafruit_motor import servo
import pwmio
from simple_pid import PID


# pid = PID(1, 0.1, 0.05, setpoint=1)

# Assume we have a system we want to control in controlled_system
# v = controlled_system.update(0)


# initialize PWM and sonar
pwm = pwmio.PWMOut(board.A1, duty_cycle=2 ** 15, frequency=50)
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D6, echo_pin=board.D7, timeout=0.1)
setpoint=13
my_servo = servo.Servo(pwm)

# adjust kP, kI, kD to tune the PID controller
pid = PID(8, 3, 0, setpoint=setpoint, output_limits=(10, 175))

# grab initial value
# input = sonar.distance 
my_servo.angle=10
# print('Angle: ', 10,)
time.sleep(.5)
my_servo.angle=175
# print('Angle: ', 160,)
time.sleep(.5)
my_servo.angle=65
# print('Angle: ', 80,)
time.sleep(.5)

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

    ## Compute new output from the PID according to the systems current value
    
    # if the distance is less than 28 cm, then do the code below
    # then indent all of this 
    if distance > 29:
        my_servo.angle = 175
        time.sleep(0.1)
    else:
        output = pid(distance)

        my_servo.angle = output
    # print('Distance: ', distance,'PID Output: ', output)
    p,i,d = pid.components
    # print(p, i, d)
    my_servo.angle = (180-output)
    time.sleep(0.1)
        

```

### Code Reflection

Possibly the hardest part of this project was the code. The code To create this code I peiced together code from my past asignments. At first, I created a code that would move back if it was greater than the setpoint, forward if it was less that the setpoint or stay still if it was directly at the setpoint. I later imported the PID Code and pid libraries. It was important to find the minimum and maximum point for the PID code. 




I also learned that the setpoint is a very crucial part of the PID project and trying different ones is also important so you get the best possible code. For our poject, the servo was a very important piece and figuring out where the servo is at 0 degrees 90 degrees and 180 degrees is crucial. That's why in the start of the code I chose the degrees of the servo and found out the lowest middle and highest points to better calibrate the servo.


For someone coding this project here is something that killed 2 birds with 1 stone.


### Code Problem 1
One problem I encountered with the code and operation was finding out where the servo values were in the right spot for what we needed.

![COde1](https://github.com/willhunt914/PIDBOX/assets/112961434/36db4cc9-593b-4eb5-a136-aeb38f848659)

My solution was to move the servo to the 3 angles which we figured would be the up, the down, and the middle. This also randomized where the ball which was inadvertent but a huge help.




Here is another problem that we solved and should be of great use to the next person to try this.


### Code Problem 2
Another problem we had was getting values that wouldn't be possible within the confines of the box.

![COde 2](https://github.com/willhunt914/PIDBOX/assets/112961434/3d7bf9f8-5a34-4b7a-96e3-24b919177dbd)
 
 
The solution was finding that if the value we got from the ultrasonic sensor was greater than 29 we would kind of reset it and move it away from the bad readings and the PID would go back to work.


### Wiring Diagram 

![Screenshot 2023-06-01 111227](https://github.com/willhunt914/PIDBOX/assets/71402974/a2691ea1-cc53-4d89-b0bc-76781608a0e4)

### Evidence
[Onshape Link](https://cvilleschools.onshape.com/documents/7c87217263b0a725d3512c0e/w/d04d77d161baa69265bfc1db/e/c6bb2c1666ca8a2d2c29ad5d)

[Bill of Materials](https://docs.google.com/document/d/1J53i04ptv5_mM0lnMhT_mGYdmYwtcKZW3SEIHETr12E/edit)



https://github.com/willhunt914/PIDBOX/assets/112961434/8d510ab7-2464-4e5e-adf6-877d366d688f


This is a video of the first time we got the pid part of our project to work.

## Cad

### Images

![Screenshot 2023-05-18 154910](https://github.com/willhunt914/PIDBOX/assets/112961434/97cc8196-3556-4fc6-85b0-99e43942295c)

This view shows where the light and switch will go, and also shows where the battery pack is held.

![Screenshot 2023-05-18 154842](https://github.com/willhunt914/PIDBOX/assets/112961434/d15d83bb-8c6f-4863-bb55-db3a7626f89a)

This picture shows the isometric viewpoint which shows how the servo is positioned and where it hooks onto the ball chamber.

![Screenshot 2023-05-18 154829](https://github.com/willhunt914/PIDBOX/assets/112961434/3d010b23-4162-4270-831f-e4633b3f571c)

Friction fit and the t-slots allowed or us to quickly put the box together and take it apart.





### Reflection (includes problems and solutions)
The CAD, while it might seem easier than the code for this project is actually a crucial piece which insures that all the code can run smoothly and the project functions as it should. Our time management was lot better for this project and we weren't rushed. We knew if we stayed focused we could finish the project on time.

Things I learned: I learned that having a very solid plan at the start is important and gives us time to be able to adapt still. There was one instance of me not thinking ahead and so when a piece came it didn't work like I thought because I didn't think of it in a logical sense at the time. So I learned that taking the time to think logically would be VERY beneficial to our project.

Here are some tips for anyone that attempts this project to avoid mistakes that we made.


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

 
 
Our new idea was to use a very strong wire which didn't bend at all. This worked and our values were much less random and the movements were more controlled.

### Misstep #1
One mistep was putting the battery pack on the side which led to the whole thing being unbalanced.

### Solution #1 
I had to put holes on the bottom for screws in order to keep it balanced. 

### Misstep #2
Another mistake was putting the servo so close to the ground which made the servo horn hit the base. 

### Solution #2
I put nuts in between the servo and the servo holder so that it would add space and allow for the srvo horn to move freely.
