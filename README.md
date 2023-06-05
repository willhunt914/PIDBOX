# PIDbox
### Matthias Zimmerman & Will Hunt
### Goal/planning

For this project we chose to do a design similar to Mr Dierolfs because it was well documented and their were many tutorials on how to do it. We also did it because Mr Dierolf is an idol and we want to be like him (Mr Dierolf wanted that)
Our goal was to create a design that would balance a ball directly in the middle using and ultrasonic sensor and servos. 



![pidplannign](https://user-images.githubusercontent.com/71402974/232500023-27507196-46f4-4ddd-9c11-e0a9c3934b7b.png)

This was our first idea and sketch where a servo located on the base you have a string or something to control the chamber.


For this project we didn't have a planning document but we decided to make a finish date for all the different parts of the project.

Onshape finished by 5/12 so that we have time to make changes.

Build done by 5/17 so that we can have a quick start on PID and make sure that everything works as it should.

Code First prototype should be done by 5/18 so that we can have a lot of time to test the code.

Our work should be done 5/31 and thats when we should do documentation. We did documentation throughout the project so that we could have more time to work.

One problem we anticipated was not having enough time to document. We decided to do the documentation throughout the project instead of at the end so we would have enough time.

### Criteria+Constriants

The criteria for this project was fairly simple, create something that utilizes PID to do anything.

The criteria included, Work together in groups of 2.
Use only an Arduino and other standard components in the Sigma Lab.
Use 4 or 6 AA batteries and a battery pack for power.
Include a power switch and an LED power indicator.
Ensure everything is securely mounted (the Arduino can use standoffs or rubber feet).

[Bill of Materials](https://docs.google.com/document/d/1J53i04ptv5_mM0lnMhT_mGYdmYwtcKZW3SEIHETr12E/edit)


### Code

```python
#Ping Pong Balance code
#Code By Will, Matthias and help from Mr Garcia
#This code uses PID to ballance a ball in the center of a platform.
import time
import board
import adafruit_hcsr04
from adafruit_motor import servo
import pwmio
from simple_pid import PID
#imports libraries 



pwm = pwmio.PWMOut(board.A1, duty_cycle=2 ** 15, frequency=50)
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D6, echo_pin=board.D7, timeout=0.1)# sets correct pins 
setpoint=13
my_servo = servo.Servo(pwm)

# adjust kP, kI, kD to tune the PID controller
pid = PID(8, 3, 0, setpoint=setpoint, output_limits=(10, 175))

input = sonar.distance 
my_servo.angle=10
print('Angle: ', 10,)
time.sleep(1.5)
my_servo.angle=175
print('Angle: ', 175,)
time.sleep(1.5)
my_servo.angle=65
print('Angle: ', 60,)
time.sleep(1.50)
#used to randomize position of ball and find right angles

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
    #     my_servo.angle = 90  
  
    if distance > 29:
        my_servo.angle = 175 # used to get ball away from ultrasonic sensor 
        time.sleep(0.1)
    elif distance > 12.5  and distance < 15.5: # used to stop ball if at correct point 
        my_servo.angle = 60 #set angle
        time.sleep(0.1)
    else:
        output = pid(distance)

        my_servo.angle = output
    print('Distance: ', distance,'PID Output: ', output ) # prints distance 
    p,i,d = pid.components
    print(p, i, d) # used to print PID values 
    time.sleep(0.1)

        

```

### Code Reflection

Possibly the hardest part of this project was the code. To create this code, I peiced together code from my past asignments. At first, I created a code that would move back if it was greater than the setpoint, forward if it was less that the setpoint or stay still if it was directly at the setpoint. I later imported the PID Code and pid libraries. It was important to find the minimum and maximum point for the PID code. 




I also learned that the setpoint is a very crucial part of the PID project and trying different ones is also important so you get the best possible code. For our poject, the servo was a very important piece and figuring out where the servo is at 0 degrees 90 degrees and 180 degrees is important. That's why in the start of the code I chose the degrees of the servo and found out the lowest middle and highest points to better calibrate the servo.


For someone coding this project here is something that killed 2 birds with 1 stone.


### Code Problem 1
One problem I encountered with the code and operation was finding out where the servo values were in the right spot for what we needed.

![COde1](https://github.com/willhunt914/PIDBOX/assets/112961434/36db4cc9-593b-4eb5-a136-aeb38f848659)

My solution was to move the servo to the 3 angles which we figured would be the up, the down, and the middle. This also randomized where the ball which was inadvertent but a huge help.




Here is another problem that we solved and should be of great use to the next person to try this.


### Code Problem 2
Another problem we had was getting values that wouldn't be possible within the confines of the box.

![Code 2](https://github.com/willhunt914/PIDBOX/assets/112961434/3d7bf9f8-5a34-4b7a-96e3-24b919177dbd)
 
 
The solution was finding that if the value we got from the ultrasonic sensor was greater than 29 we would kind of reset it and move it away from the bad readings and the PID would go back to work.


### Wiring Diagram 

<img src="https://github.com/willhunt914/PIDBOX/assets/71402974/027e861d-31be-49ce-8adf-1da0d4c700c3" alt="Evidence#1" width="500" height="500">

## Cad

[Onshape Link](https://cvilleschools.onshape.com/documents/7c87217263b0a725d3512c0e/w/d04d77d161baa69265bfc1db/e/c6bb2c1666ca8a2d2c29ad5d)

### Images

![Screenshot 2023-05-18 154910](https://github.com/willhunt914/PIDBOX/assets/112961434/97cc8196-3556-4fc6-85b0-99e43942295c)

This view shows where the light and switch will go, and also shows where the battery pack is held.

![Screenshot 2023-05-18 154842](https://github.com/willhunt914/PIDBOX/assets/112961434/d15d83bb-8c6f-4863-bb55-db3a7626f89a)

This picture shows the isometric viewpoint which shows how the servo is positioned and where it hooks onto the ball chamber.

![Screenshot 2023-05-18 154829](https://github.com/willhunt914/PIDBOX/assets/112961434/3d010b23-4162-4270-831f-e4633b3f571c)

Friction fit and the t-slots allowed or us to quickly put the box together and take it apart.




### Reflection (includes problems and solutions)
The CAD, while it might seem easier than the code for this project is actually a crucial piece which insures that all the code can run smoothly and the project functions as it should. Our time management was lot better for this project and we weren't rushed. We knew if we stayed focused we could finish the project on time. The communication between me and Will was important so we both knew what we wanted from each other. One thing to think about during this project is the dimensions of the chamber for the ping pong ball. The length was 289.60mm, height was 54.00mm, and the width was 57.200 which was almost a perfect fit for the ping pong ball and I led to very few bad readings from the ultrasonic sensor. An issue I ran into was not thinking logically about the differences between onshape and the real world. I accidently looked over something which came back to bite me but, by the end of the project I definitely learned to think about things thoroughly and not just in 1 dimension.


I learned that having at strong plan at the start makes the whole process easier. Taking the time to plan makes the whole project move smoother even though it may seem unnessesary.

Here are some tips for anyone that attempts this project to avoid mistakes that we made.


### Problem #1

![PIDBOX#3](https://github.com/willhunt914/PIDBOX/assets/112961434/cd20c6a7-7a55-4461-ada8-b235ba777d57)



Our first problem with cad was that screw holes in the bottom would slow the ball down and would not let it balance.
### Solution #1

Our solution was...

![Screenshot 2023-05-22 093548](https://github.com/willhunt914/PIDBOX/assets/112961434/e1c62af7-ee5a-4057-9c3b-59204c726199)

Moving the screws from the bottom to the side of the chamber so that the screws don't get in the way. This was an example ofme thinking only in onshape and not thinking about the ball and where it was gonna be.


### Problem 2

<img src="https://github.com/willhunt914/PIDBOX/assets/112961434/d3b54ae3-1375-4a07-a4a5-2d41a0973268" alt="Old Wire" width="500" height="600">

Our original wire bent and twisted which made it very hard to get constant readings.

### Solution 2
<img src="https://github.com/willhunt914/PIDBOX/assets/112961434/c6d6ecbf-95f3-44d2-9823-a3ff049083af" alt="new wire" width="500" height="600">

 
 
Our new idea was to use a very strong wire which didn't bend at all. This worked and our values were much less random and the movements were more controlled.

### Misstep #1
One misstep was putting the battery pack on the side which led to the whole thing being unbalanced.

### Solution #1 
I had to put holes on the bottom for screws in order to keep it balanced. 

### Misstep #2
Another mistake was putting the servo so close to the ground which made the servo horn hit the base. 

### Solution #2
I put nuts in between the servo and the servo holder so that it would add space and allow for the srvo horn to move freely.

### Evidence

<img src="https://github.com/willhunt914/PIDBOX/assets/112961434/1d47b976-68e1-439a-9bda-f3334fe806eb" alt="Evidence#1" width="450" height="650">


https://github.com/willhunt914/PIDBOX/assets/112961434/8d510ab7-2464-4e5e-adf6-877d366d688f


This is a video of the first time we got the pid part of our project to work.
