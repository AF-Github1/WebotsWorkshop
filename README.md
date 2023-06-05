WEBOTS WORKSHOP

This repository contains the instructions and the code for the Webots workshops done in 31/05/2023 and 01/06/2023 within the context of AZORESBOT2023.

https://azoresbot2023.uac.pt/

It is meant to serve as a supporting learning document.

In the case that someone that already has significant experience with Webots comes here, this repository will be mostly useless, as this is only meant as an introduction to the Webots interface and some of the specific functions that Webots uses.


WARNING

CURRENTLY IMAGES/VIDEOS LINKS ARE BROKEN


--------------------------------------------------------

INSTALLATION

Webots

[https://cyberbotics.com](https://www.cyberbotics.com/) 

Since this tutorial will be in python, it will also be necessary to install python.

Python Windows

https://www.python.org/downloads/windows/

**Path instructions**

After having both Python and Webots installed you may have to manually tell Webots the path to your python executable.

Go to Tools>Preferences


https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/84ff14e0-f41c-4416-989a-db59a8965051

Type python in the Python Command section

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/7c97bfcd-8949-42fc-b79e-e736c5ace261)

Now you must go to environment variable and define the path for Python

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/a1d292ea-d18e-4c93-8c81-660ca85b6ecf)

The path must be the location for the Python executable and it will change depending on where you installed Python. After the path has been correctly configured you will now be able to write Python code for your Webots controller

--------------------------------------------------------

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

--------------------------------------------------------

MAKING A NEW WORLD

In the top left side of the interface go to File>New>New World File

https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/4f87ddca-5ee8-4a4d-8d1d-f7a106e3aa8b

If it warns you it can't create a new world due to not being able to change the files in its current location, create a new project directory instead, which will be the option above. Creating a new project directory will also create a new world file 

Afterwards give it a name and tick the box for 'Add a rectangle arena'. This is not enabled by default. It's possible to later add the arena but it's quicker this way


--------------------------------------------------------

ADDING A ROBOT
          
At this stage you should have already created a world and can now add a robot and any other object you so desire. To add any object select the + icon below the top left options.

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/86b27873-1fe1-4905-b55c-208de1066e0c)

Then you can use the find text box to look up what you want. In this case we need an e-puck

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/ac8c67fe-af11-453b-be7e-c397ebbaeb89)

Then it's just a matter of clicking 'Add' and the robot should spawn in your arena.

--------------------------------------------------------

E-PUCK SPECIFICS

For the sake of this demonstration the GCtronic's e-puck will be used. One thing that will mentioned a few times over this document is the Webots documentation that can specify certain aspects of Webots and its robots at a much greater detail than one could ever do here. As such any explanation on how a robot works will be supported with a link to the relevant documentation 

[https://cyberbotics.com/doc/guide/epuck
](https://cyberbotics.com/doc/guide/epuck)

These particular pages includes the default parts for the e-puck, their names, and where they are located on the robot. For example, it will show where the camera is positioned and what string you should use in your code to call the camera. The same for any other part of the robot like its LEDS, its sensors and a slew of other technical details. 

At any time when you are fiddling around in Webots, if you have any doubts on how a specific part of the robot works, consult the documentation.

--------------------------------------------------------

MAKING A CONTROLLER
         
Now that we have our world file and our robot ready it is time to program. You now want to create a new controller. Go to File>New>New Robot Controller

https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/615c33c4-8dd0-4904-8df9-6a153d87c950

Select the coding language you will code it on, for the purposes of this tutorial this will be python, select a IDE, which should be Webots and finally give it a name, which can be whatever you like.

Now that we have our controller we need to go to the controller children node of the e-puck in the scene tree. There will be a controller selected by default. Change it to the new controller you just created.

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/cae170db-e742-48e9-a002-ff8b07fa9806)

Now to the right of your screen you should now see your controller text file that should look like this

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/19437f15-0621-42e1-93a3-53165b4f92bf)

To note:

Some older videos and posts adressing how Webots work are based on older versions. More recent versions put the controller wizard within the file tab, so if you are not finding the controller wizard tab, it's because you are in a more recent version of Webots and must instead create a new controller through the file tab.

Webots expects files to follow certain conventions for controllers if you are adding the files manually and not through the new controller option in the Webots interface.
Please look at the last section in this page of the documentation for the naming/directory convention.
https://cyberbotics.com/doc/guide/the-standard-file-hierarchy-of-a-project

--------------------------------------------------------

CONTROLLER BASICS

There are some fundamental pieces of information one must know before starting to program a robot. 

First of all the simulation is based on a timestep, this being the time in miliseconds that takes for each instance of any action to occur in the simulation. You can check and change the value of the timestep in the basicTimeStep children node or define a timestep value through a variable inside a controller.

By default the basicTimeStep is 32

If you have different timesteps for different parts/logic loops of the robot, remember that the timestep should be a multiple of the first timestep that you created initially. If you create a new value it should be always be in multiples. So if your first timestep you declared is 16, your other values should be 32,64,128 and so on. This is so that every part of the simulation is in sync. If the simulation stops being in sync some issues might crop up like certain objects becoming non functional/not function as they should.

Another important point is how you call each part of the robot. They may need to be imported and they follow certain conventions in order to be activated. This will be explained in greater detail in the coding section below.

--------------------------------------------------------

CODING YOUR FIRST ROBOT
 
I will show some sample code along with the explanation of what it does. I will also show how to install certain modules. 

**The full code without any comments will be put in a section below this one if you wish to copy it.
**

#This line calls the modules of the robot used to code in this controller. 

from controller import Robot, DistanceSensor, Motor, Camera, LED

#I define the timestep variable here and define max speed, a variable to make it a bit more covenient to change the robots velocity. This doesn't need to be a particular value, this just happens to be the top speed for the physical e-puck

TIME_STEP = 32
MAX_SPEED = 6.28


#This creates the first robot instance

robot = Robot()

#This is a list for the sensor names. These are the sensors around the robot that detect the proximity of objects. After making this list I activate each one of them with a for function and using the timestep variable previously configured, so they will get proximity information at every timestep

ps = []

psNames = [
    'ps0', 'ps1', 'ps2', 'ps3',
    'ps4', 'ps5', 'ps6', 'ps7'
]

for i in range(8):
    ps.append(robot.getDevice(psNames[i]))
    ps[i].enable(TIME_STEP)
    
    
#This is a list for the LED names. Similarly to the previous lines, this calls upon all the LEDS in order to activate them.

led = []

ledNames = [
    'led0', 'led1', 'led2', 'led3',
    'led4', 'led5', 'led6', 'led7'
]

for j in range(8):

    led.append(robot.getDevice(ledNames[j]))
    
  
#This activates the right and left motors for the robot

leftMotor = robot.getDevice('left wheel motor')

rightMotor = robot.getDevice('right wheel motor')

#The set position function defines the target destination for the motors. In this case we want them to keep moving, so we just set it to infinite

leftMotor.setPosition(float('inf'))

rightMotor.setPosition(float('inf'))

#In here this just defines the initial velocity for the motor. So whenever it starts running the code in this controller it starts from 0 velocity.

leftMotor.setVelocity(0.0)

rightMotor.setVelocity(0.0)

#This activates the camera. We call the camera and enable image gathering based on timestep
       
camera = robot.getDevice('camera')

camera.enable(TIME_STEP) 

    
#This activates the GPS. 

gps = robot.getGPS('gps')

gps.enable(TIME_STEP)

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/35aba30f-e09f-4fb0-8a28-4f6be1963e85)

--------------------------------------------------------

By default the e-puck robot does not come with the gps module. As such it is necessary to add the gps through the scene tree. Select the turret slot in the scene tree

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/9e3d8aa4-f6ba-4fba-add3-3848f3af4caa)

Using the same button as we used before to add a new object, look up GPS in the search box and add it to the robot.

--------------------------------------------------------

#This starts the logic loop for our robot

while robot.step(TIME_STEP) != -1:

    # This creates a list to register the values obtained from the proximity sensors
    
    psValues = []
    for i in range(8):
        psValues.append(ps[i].getValue())
       
  #This gets the values obtained by the GPS and prints them to the console after formatting them.
 
    gps_value = gps.getValues()
    print(gps_value)   
    msg = "GPS test- "
    for each_val in gps_value:
        msg += " {0:0.2f}".format(each_val)
    print(msg)
    
  #This is the logic for the obstacle detection. Whenever the appropriate sensors detect they are within a given distance of an obstacle, depending on which sensors detect it we either define right_obstacle or left_obstacle as true.
  
    right_obstacle = psValues[0] > 80.0 or psValues[1] > 80.0 or psValues[2] > 80.0
    left_obstacle = psValues[5] > 80.0 or psValues[6] > 80.0 or psValues[7] > 80.0


  #Whenever the value of the right/left obstacle is true we change the speed for each of the motors. As such, the robot will rotate either to the left or to the right until the sensors stop detecting obstacles
  #To note that this simple code does not prevent a obstacle detection loop, so if the robot manages to get a situation where it detects obstacles in both sides it will get stuck until manually removed from the position.
  
  https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/4fa13e96-1e7d-4dce-b171-fd9f04d3fafe

    leftSpeed  = MAX_SPEED
    rightSpeed = MAX_SPEED
    if left_obstacle:
        # Turns right
        leftSpeed  = 0.5 * MAX_SPEED
        rightSpeed = -0.5 * MAX_SPEED
    elif right_obstacle:
        # Turns left
        leftSpeed  = -0.5 * MAX_SPEED
        rightSpeed = 0.5 * MAX_SPEED
        
    leftMotor.setVelocity(leftSpeed)
    rightMotor.setVelocity(rightSpeed)
   
   #This part of the loop is relevant to the camera image logic. I will need to explain a couple of concepts before going in greater detail
 
   --------------------------------------------------------
   
   The camera in webots sees image as a matrix of pixels, and it assigns to each one of these pixels a RGBA value. It is possible to manually define the RGBA value of an object without actually changing it's colour, so the default RGB value for certain objects might not correspond to reality. For example, the walls of the arena are perceived as blue by the camera.
   
   It is not possible to get information out of the bounds of the camera image. As such the FOR loop for the image array must be within the height and width of the matrix of the gathered image.
   
   --------------------------------------------------------
   
  #As mentioned before, this for loops handle the logic for gathering and checking the RGBA values for the pixels in the image obtained through the camera
  
    for x in range(0,camera.getWidth()):
        for y in range(0,camera.getHeight()):
            image = camera.getImageArray()

            robot.step(TIME_STEP)
  #This part stores the RGBA values of the pixels within a variable. In image[x][y][0], the x and y correspond to the coordinates of the pixels and the [0] corresponds to R in RGBA (Red). As such, 1 corresponds to green, 2 to blue and not used in this code, 3 corresponds to Alpha.
  #It compares the RGB values in the image and prints out the appropriate colour for whichever type is more numerous.
  #Whenever it is detecting a color it blinks its LEDS, with led[j].set(1) activating the LED and led[j].set(0) turning them off again
  
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
    
    
    
--------------------------------------------------------  
    
FULL UNCOMMENTED CODE
    
from controller import Robot, DistanceSensor, Motor, Camera, LED

TIME_STEP = 32
MAX_SPEED = 6.28

robot = Robot()
ps = []
psNames = [
    'ps0', 'ps1', 'ps2', 'ps3',
    'ps4', 'ps5', 'ps6', 'ps7'
]

for i in range(8):
    ps.append(robot.getDevice(psNames[i]))
    ps[i].enable(TIME_STEP)
    
    
led = []
ledNames = [
    'led0', 'led1', 'led2', 'led3',
    'led4', 'led5', 'led6', 'led7'
]

for j in range(8):
    led.append(robot.getDevice(ledNames[j]))
    
  
leftMotor = robot.getDevice('left wheel motor')
rightMotor = robot.getDevice('right wheel motor')

leftMotor.setPosition(float('inf'))
rightMotor.setPosition(float('inf'))
leftMotor.setVelocity(0.0)
rightMotor.setVelocity(0.0)
       
camera = robot.getDevice('camera')
camera.enable(TIME_STEP) 
  
gps = robot.getGPS('gps')
gps.enable(TIME_STEP)

while robot.step(TIME_STEP) != -1:

    psValues = []
    for i in range(8):
        psValues.append(ps[i].getValue())
       
 
    gps_value = gps.getValues()
    print(gps_value)   
    msg = "GPS test- "
    for each_val in gps_value:
        msg += " {0:0.2f}".format(each_val)
    print(msg)
    
    right_obstacle = psValues[0] > 80.0 or psValues[1] > 80.0 or psValues[2] > 80.0
    left_obstacle = psValues[5] > 80.0 or psValues[6] > 80.0 or psValues[7] > 80.0

  
    leftSpeed  = MAX_SPEED
    rightSpeed = MAX_SPEED
    if left_obstacle:
        leftSpeed  = 0.5 * MAX_SPEED
        rightSpeed = -0.5 * MAX_SPEED
    elif right_obstacle:
        leftSpeed  = -0.5 * MAX_SPEED
        rightSpeed = 0.5 * MAX_SPEED
        
    leftMotor.setVelocity(leftSpeed)
    rightMotor.setVelocity(rightSpeed)
  
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
 
 --------------------------------------------------------
    
SUPERVISOR

https://cyberbotics.com/doc/reference/supervisor

This is a special type of node that serves as a sort of master for the simulation. It can spawn or despawn robots and objects, changes parameters, stop or restart the simulation and so on. What it can't do is get internal values from components of other robots, like camera images.

Any robot can be a supervisor, although it is better to use a dedicated robot node for it

Add a dedicated robot node to the world

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/5fe9e3cf-324f-4357-8cb3-051a928820e0)

This robot node does not correspond to an actual robot running in the simulation, it's just a node that can run the code for a controller. In this case since we will be converting a node into a supervisor node, there's no need to have another object in our arena.

We then create a new controller. There is nothing different in the process of creating this controller, you can create it exactly like when we created our first. The contents though, will be very different.

Finally we change the the value of supervisor in our new robot node to TRUE

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/2bd5c61e-4eff-47da-952f-9772cd12dcd8)

Only the node that we use for the supervisor should be declared as the supervisor and nothing else. 

Below it will be shown an example of what you can do using the supervisor and some basics on how to code it

--------------------------------------------------------

SUPERVISOR EXAMPLE
          
#Imports the supervisor API

from controller import Supervisor

#Declaring timestep value

TIME_STEP = 32

#In here we declare the node as a supervisor node instead of a robot node

robot = Supervisor()

   --------------------------------------------------------

The robot.getFromDef('DEF') function is how you call a node.
Every object and robot can have their DEF value modified, which can be different from the name. By default this field is empty so as you create objects to call through the supervisor you should fill this field with the strings you will use.

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/122e2c7d-fd23-46aa-95c9-d98c3225c963)
   --------------------------------------------------------

#As explained before, this is how we call the node

epuck = robot.getFromDef('epuck')

#This gets the value for the translation field of the epuck robot (the position)

translation_field = epuck.getField('translation')

#This calls the root node, the world file, and associates it with a variable

root_node = robot.getRoot()

#This gets the children node values for the root node

children_field = root_node.getField('children')

   --------------------------------------------------------

Importing objects through the supervisor

Any new node you create through the supervisor must first be imported through the IMPORTABLE EXTERPROTO interface

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/6da3ab86-37c0-4f45-af4b-cceca87c58d5)

![image](https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/d26167ff-abf6-440e-9a6b-02a613f210c9)

Each object can only be called once, but can each be called multiple times.

--------------------------------------------------------

#In our case we will import a ball and a couple of different robots.

children_field.importMFNodeFromString(-1, 'DEF BALL Ball { translation 0 1 1 }')

#This imports a ball node that we added through IMPORTABLE EXTERNPROTO

ball_node = robot.getFromDef('BALL')

#Gets the color value for the ball

color_field = ball_node.getField('color')



#We create a loop with a counter so we can better control what happens in the simulation

i = 0
while robot.step(TIME_STEP) != -1:

  if (i == 0):
  
    #This defines a new position for the translation field, changing the position
    
    new_value = [2.5, 0, 0]
    
    translation_field.setSFVec3f(new_value)
    
    #This removes the e-puck we manually added to the world
    
  if i == 10:
  
      epuck.remove()
      
   #This imports a new e-puck from the IMPORTABLE EXTERPROTO table. What we want to import is called through the name it shows on the table. The name of e-puck in the table is 'E-puck' so that is the string we will use
   
  if i == 20:
  
    children_field.importMFNodeFromString(-1, 'E-puck { }')
    
  #This saves the translation value of the ball node
  
  position = ball_node.getPosition()
  
  #And then we print out each of the xyz position values to the console
  
  print('Ball position: %f %f %f\n' %(position[0], position[1], position[2]))
  
  #When the ball goes below a certain z value, we change its colour

  if position[2] < 0.2:
  
    red_color = [1, 0, 0]
    
    color_field.setSFColor(red_color)

  i += 1


**Authors/Workshop Lecturers**

António José Lopes de Freitas

Carlos Cabral

João Lopes de Freitas













