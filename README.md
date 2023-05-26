WebotsWorkshop

This repository contains the instructions and the code for the Webots workshop done in 31/05/2023 and 01/06/2023 in the school of (?) within the context of AZORESBOT2023.

It is meant to serve as a supporting learning document.

In the case that someone that already has significant experience with Webots comes here, this repository will be mostly useless, as this is only meant as an introduction to the Webots interface and some of the specific functions that Webots uses.


          WHY USE WEBOTS
          
The answer is quite simple really. Convenience and money. As of the writing of this document the cheapest variation of the physical e-puck robot used in this tutorial is around 850 euros. 
This is an amount of money that not just anyone can afford to spend in a robot. But Webots is free. Anyone that can run Webots can use Webots.

And in the context of school/university learning, this simulator also enables students to not have to depend on hardware provided by the institution in order to continue their learning. They do not need to reserve a timeslot for them to use a robot, they do not need to take turns bringing it home, they can start the work within the classroom and continue it at home while working on the exact same world file through the Webots simulator.

          INSTALLATION

WEBOTS https://cyberbotics.com/instruction 

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

In the top left side of the interface go to File>New World File

https://github.com/AF-Github1/WebotsWorkshop/assets/133685290/3f537982-cecf-418d-8d71-23879f719dd5

Afterwards give it a name and tick the box for 'Add a rectangle arena'. This is not enabled by default. It's possible to later add the arena but it's quicker and more covenient this way

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

This particular pages includes the default parts for the e-puck, their names, and where they are located on the robot. For example, it will show where the camera is positioned and what string you should use in your code to call the camera. The same for any other part of the robot like its LEDS, its sensors and a slew of other technical details. 

At any time when you are fiddling around in Webots, if you have any doubts on how a specific part of the robot works, consult the documentation.

          MAKING A CONTROLLER
         
Now that we have our world file and our robot ready it is time to program. You now want to create a new controller. By going to the file tab....... (Make video to put here again)


After creating a new controller you must now go to the children node in the e-puck subtree and select the new controller you created (put image here).....

          CODING YOUR FIRST ROBOT
          
Explain timestep before anything else here.....


          CAMERA SPECIFICS

This code enables the calls the camera and enables it based on the TIME_STEP previously configured

camera = robot.getDevice('camera')

camera.enable(TIME_STEP) 

At every TIME_STEP instance the camera will get an image. 
In terms of colour recognition which is what we are using the camera for in this tutorial, think of the image as a matrix of RGB coloured pixels.... (Explain how it prioritizes colour here, explain rgb pixel count)

          LOOP SPECIFICS

Explain need for timestep, explain how to be careful with requests and calls as it crashes the program

          DIRECTORY NAMING SPECIFICS

46explain how files will have to be named

          SUPERVISOR

explain how to call supervisor, making dedicated node, what tou can and cant call, importable extern photo, explain DEF




**Authors/Workshop Lecturers**

António José Lopes de Freitas

Carlos Cabral

João Lopes de Freitas













