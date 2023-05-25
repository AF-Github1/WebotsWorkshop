

WebotsWorkshop

This repository contains the instructions and the code for the Webots workshop done in 31/05/2023 and 01/06/2023 in the school of (?) within the context of AZORESBOT2023.

It is meant to serve as a supporting document.

In the case that someone that already has significant experience with Webots comes here, this repository will be mostly useless, as this is only meant as an introduction to the Webots interface and some of the specific functions that Webots uses.


          WHY USE WEBOTS
          
The answer is quite simple really. Convenience and money. As of the writing of this document the cheapest variation of the physical e-puck robot used in this tutorial is around 850 euros. 
This is an ammount of money that not just anyone can afford to dump into a robot. But Webots is free. Anyone that can run Webots can use Webots.
And in the context of school/university learning, this simulator also presents



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

Node highest in a given hierarchy. Usually the created world file is considered the root node

**CHILDREN NODE**

All nodes within the hierarchy of a root node. Any object that is added to a world will be considered a children node. These children nodes can in turn have their own children nodes and so on.

**SCENE TREE**

It's the visual representation for the entire node hierarchy and its the interface where the user can modify, create or delete nodes.

node, proto node, adding removing, external photo...

**WORLD**

It is the work environment in which you add and modify nodes. The world file will contain all of these changes.

**CONTROLLER**

It is a text file that contains the code you write. It is not contained within the world file, it is a separate file. ****(Confirm this, clarify naming conventions)****

        MAKING A NEW WORLD

1- File
2- Make a new world
.....

explain arena
explain NUE coordinates

To note: Some older videos and posts adressing how Webots work are based on older versions. More recent versions put the controller wizard within the file tab, so if you are not finding the controller wizard tab, it's because you are in a more recent version of Webots and must instead create a new controller through the file tab.



          E-PUCK SPECIFICS

For the sake of this demonstration the GCtronic's e-puck will be used. One thing that will mentioned a few times over this document is the Webots documentation that can specify certain aspects of Webots and it's robots at a much greater detail than one could ever do here. As such any explanation on how a robot works will be supported with a link to the relevant documentation 

[https://cyberbotics.com/doc/guide/epuck
](https://cyberbotics.com/doc/guide/epuck)

This particular pages includes the default parts for the e-puck, their names, and where they are located on the robot. For example, it will show where the camera is positioned and what string you should use in your code to call the camera. The same for any other part of the robot like its LEDS, its sensors and a slew of other technical details. 

At any time, if you have any doubts on how a specific part of the robot works, consult the documentation.

This part of the documentation links to the specification of the e-puck. It includes where the part

showing engineering doc might be a bit much, but explain what it is, as it explains where parts are located

          CAMERA SPECIFICS

Explain camera image functioning, how color recog works

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












