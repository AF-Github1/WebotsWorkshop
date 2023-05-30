WebotsWorkshop

This repository contains the instructions and the code for the Webots workshops done in 31/05/2023 and 01/06/2023 within the context of AZORESBOT2023.

It is meant to serve as a supporting learning document.

In the case that someone that already has significant experience with Webots comes here, this repository will be mostly useless, as this is only meant as an introduction to the Webots interface and some of the specific functions that Webots uses.


          WHY USE WEBOTS
          
Practicality and reduction of expenses. As of the writing of this document the cheapest variation of the physical e-puck robot used in this tutorial is around 850 euros. 
This is an amount of money that not just anyone can afford to spend in a robot. But Webots is free. Anyone that can run Webots can use Webots.

And in the context of school/university learning, this simulator also enables students to not have to depend on hardware provided by the institution in order to continue their learning. They do not need to reserve a timeslot for them to use a robot, they do not need to take turns bringing it home, they can start the work within the classroom and continue it at home while working on the exact same world file through the Webots simulator.

          INSTALLATION

WEBOTS [https://cyberbotics.com](https://www.cyberbotics.com/) 

Since this tutorial will be in python, it will also be necessary to install python.

Python Windows
https://www.python.org/downloads/windows/

Path instructions here...
check ubuntu and redhat specifics including path..

        GLOSSARY

**NODE**

Any object that be can added or manipulated in Webots. The world can be considered a node, a robot can be considered a node, the coordinate system is a node and so on.

**ROOT NODE**

Highest node in a given hierarchy. Usually the created world file is considered the root node

**CHILDREN NODE**

All nodes within the hierarchy of a root node. Any object that is added to a world will be considered a children node. These children nodes can in turn have their own children nodes and so on.

**SCENE TREE**

It's the visual representation for the entire node hierarchy and its the interface where the user can modify, create or delete nodes.

**WORLD**

It is the work environment in which you add and modify nodes. The world file will contain all of these changes.

**CONTROLLER**

It is a text file that contains the code you write. It is not contained within the world file, it is a separate file. 

        MAKING A NEW WORLD

In the top left side of the interface go to File>New>New World File

https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/3f537982-cecf-418d-8d71-23879f719dd5

Afterwards give it a name and tick the box for 'Add a rectangle arena'. This is not enabled by default. It's possible to later add the arena but it's quicker this way

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/e81a4e44-07ff-4d9f-b08a-5624d7d811bd)

To note:

Some older videos and posts adressing how Webots work are based on older versions. More recent versions put the controller wizard within the file tab, so if you are not finding the controller wizard tab, it's because you are in a more recent version of Webots and must instead create a new controller through the file tab.

Webots expects files to follow certain conventions for controllers if you are adding the files manually and not through the new controller option in the Webots interface.
Please look at the last section in this page of the documentation for the naming/directory convention.
https://cyberbotics.com/doc/guide/the-standard-file-hierarchy-of-a-project

          ADDING A ROBOT
          
At this stage you should have already created a world and can now add a robot and any other object you so desire. To add any object select the + icon below the top left options.

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/280c61f3-ddf8-4272-873d-f5591dd19635)

Then you can use the find text box to look up what you want. In this case we need an e-puck

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/ac8c67fe-af11-453b-be7e-c397ebbaeb89)

Then it's just a matter of clicking 'Add' and the robot should spawn in your arena.

          E-PUCK SPECIFICS

For the sake of this demonstration the GCtronic's e-puck will be used. One thing that will mentioned a few times over this document is the Webots documentation that can specify certain aspects of Webots and its robots at a much greater detail than one could ever do here. As such any explanation on how a robot works will be supported with a link to the relevant documentation 

[https://cyberbotics.com/doc/guide/epuck
](https://cyberbotics.com/doc/guide/epuck)

These particular pages includes the default parts for the e-puck, their names, and where they are located on the robot. For example, it will show where the camera is positioned and what string you should use in your code to call the camera. The same for any other part of the robot like its LEDS, its sensors and a slew of other technical details. 

At any time when you are fiddling around in Webots, if you have any doubts on how a specific part of the robot works, consult the documentation.

          MAKING A CONTROLLER
         
Now that we have our world file and our robot ready it is time to program. You now want to create a new controller. By going to File>New>New Robot Controller

https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/615c33c4-8dd0-4904-8df9-6a153d87c950

Select the coding language you will code it on, for the purposes of this tutorial this will be python, select a IDE, which should be Webots and finally give it a name, which can be whatever you like.

Now that we have our controller we need to go to the controller children node of the e-puck in the scene tree. There will be a controller selected by default. Change it to the new controller you just created.

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/cae170db-e742-48e9-a002-ff8b07fa9806)

Now to the right of your screen you should now see your controller text file that should look like this

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/19437f15-0621-42e1-93a3-53165b4f92bf)

          CONTROLLER BASICS

There are some fundamental pieces of information one must know before starting to program a robot. 

First of all the simulation is based on a timestep, this being the time in miliseconds that takes for each instance of any action to occur in the simulation. 

If you have different timesteps for different parts/logic loops of the robot, remember that the timestep should be a multiple of the first timestep that you created initially. So if your initial timestep is 16, then if you create a new value it should be new values of 32,48,64 and so on. This is so that every part of the simulation is in sync. If the simulation stops being in sync some issues might crop up like certain objects becoming non functional/not function as they should.

Another important point is how you call each part of the robot. They may need to be imported and they follow certain conventions in order to be activated. This will be explained in greater detail in the coding section below.

          CODING YOUR FIRST ROBOT
 
I will show some sample code along with the explanation of what it does. I will also show how to install certain modules 
 
# This line calls the modules of the robot used to code in this controller. 
from controller import Robot, DistanceSensor, Motor, Camera, LED

# I define the timestep variable here and define max speed, a variable to make it a bit more covenient to change the robots velocity. This doesn't need to be a particular value, this just happens to be the top speed for the physical e-puck
TIME_STEP = 32
MAX_SPEED = 6.28


# I create the robot instance with this line
robot = Robot()
# This is a list for the sensor names. These are the sensors around the robot that detect the proximity of objects. After making this list I activate each one of them with a for function and using the timestep variable previously configured, so they will get proximity information at every timestep
ps = []
psNames = [
    'ps0', 'ps1', 'ps2', 'ps3',
    'ps4', 'ps5', 'ps6', 'ps7'
]

for i in range(8):
    ps.append(robot.getDevice(psNames[i]))
    ps[i].enable(TIME_STEP)
    
    
# This is a list for the LED names. Similarly to the previous lines, this calls upon all the LEDS in order to activate them.
led = []
ledNames = [
    'led0', 'led1', 'led2', 'led3',
    'led4', 'led5', 'led6', 'led7'
]

for j in range(8):
    led.append(robot.getDevice(ledNames[j]))
    
  
# This activates the right and left motors for the robot
leftMotor = robot.getDevice('left wheel motor')
rightMotor = robot.getDevice('right wheel motor')

# The set position function defines the target destination for the motors. In this case we want them to keep moving, so we just set it to infinite
leftMotor.setPosition(float('inf'))
rightMotor.setPosition(float('inf'))
# In here this just defines the initial velocity for the motor. So whenever it starts running the code in this controller it starts from 0 velocity.
leftMotor.setVelocity(0.0)
rightMotor.setVelocity(0.0)

# This activates the camera. We call the camera and enable image gathering based on timestep
       
camera = robot.getDevice('camera')
camera.enable(TIME_STEP) 

    
# This activates the GPS. (INSERT ADDING GPS IN TURRET SLOT HERE).........

gps = robot.getGPS('gps')
gps.enable(TIME_STEP)



# This starts the logic loop for our robot
while robot.step(TIME_STEP) != -1:

    # This creates a list to register the values obtained from the proximity sensors
    psValues = []
    for i in range(8):
        psValues.append(ps[i].getValue())
       
  # This gets the values obtained by the GPS and prints them to the console after formatting them.
 
    gps_value = gps.getValues()
    print(gps_value)   
    msg = "GPS test- "
    for each_val in gps_value:
        msg += " {0:0.2f}".format(each_val)
    print(msg)
    
  # This is the logic for the obstacle detection. Whenever the appropriate sensors detect they are within a given distance of an obstacle, depending on which sensors detect it we either define        right_obstacle or left_obstacle as true.
    right_obstacle = psValues[0] > 80.0 or psValues[1] > 80.0 or psValues[2] > 80.0
    left_obstacle = psValues[5] > 80.0 or psValues[6] > 80.0 or psValues[7] > 80.0


  # Whenever the value of the right/left obstacle is true we change the speed for each of the motors. As such, the robot will rotate either to the left or to the right until the sensors stop detecting obstacles
  # To note that this simple code does not prevent a obstacle detection loop, so if the robot manages to get a situation where it detects obstacles in both sides it will get stuck until manually removed from the position.
  
  https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/4fa13e96-1e7d-4dce-b171-fd9f04d3fafe

    leftSpeed  = MAX_SPEED
    rightSpeed = MAX_SPEED
    if left_obstacle:
        # Virar para a direira
        leftSpeed  = 0.5 * MAX_SPEED
        rightSpeed = -0.5 * MAX_SPEED
    elif right_obstacle:
        # Virar para a esquerda
        leftSpeed  = -0.5 * MAX_SPEED
        rightSpeed = 0.5 * MAX_SPEED
        
    leftMotor.setVelocity(leftSpeed)
    rightMotor.setVelocity(rightSpeed)
    
    (THIS PART NOT EDITED YET.-..............
  # This part of the loop gets the value of the image obtained from the camera in pixels. For each pixel that corresponds to a given RGB value, 
    for x in range(0,camera.getWidth()):
        for y in range(0,camera.getHeight()):
            image = camera.getImageArray()

            robot.step(TIME_STEP)
            red = image[x][y][0]
            green = image[x][y][1]
            blue = image[x][y][2]
            
            if red > green and red > blue:
                for j in range(8):
                    led[j].set(1)
                    robot.step(TIME_STEP)
                    led[j].set(0)
                    print('red')
            if green > red and green > blue:
               for j in range(8):
                   led[j].set(1)
                   robot.step(TIME_STEP)
                   led[j].set(0)    
                   print('green')   
            if blue > red and blue > green:
               for j in range(8):
                   led[j].set(1)
                   robot.step(TIME_STEP)
                   led[j].set(0) 
                   print('blue')
            break
        break
    
 

          CAMERA SPECIFICS

This code enables the calls the camera and enables it based on the TIME_STEP previously configured

camera = robot.getDevice('camera')

camera.enable(TIME_STEP) 

At every TIME_STEP instance the camera will get an image. 
In terms of colour recognition which is what we are using the camera for in this tutorial, think of the image as a matrix of RGB coloured pixels.... (Explain how it prioritizes colour here, explain rgb pixel count)


          SUPERVISOR

explain how to call supervisor, making dedicated node, what tou can and cant call, importable extern photo, explain DEF




**Authors/Workshop Lecturers**

António José Lopes de Freitas

Carlos Cabral

João Lopes de Freitas













