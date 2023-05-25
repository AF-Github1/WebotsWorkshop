          # WebotsWorkshop

This repository contains the instructions and the code for the Webots workshop done in 31/05/2023 and 01/06/2023 in the school of (?).

It is meant to serve as a supporting document.

In the case that someone that already has significant experience with Webots comes here, this repository will be mostly useless, as this is only meant as an introduction to the Webots interface and some of the specific functions that Webots uses.

          INSTALLATION

WEBOTS https://cyberbotics.com/instruction 

Since this tutorial will be in python, it will also be necessary to install python.

Python Windows
https://www.python.org/downloads/windows/

Path instructions here...
check ubuntu and redhat specifics including path..

        MAKING A NEW WORLD



explain arena
explain NUE coordinates

To note: Some older videos and posts adressing how Webots work are based on older versions. More recent versions put the controller wizard within the file tab, so if you are not finding the controller wizard tab, it's because you are in a more recent version of Webots and must instead create a new controller through the file tab.

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

          E-PUCK SPECIFICS

https://cyberbotics.com/doc/guide/epuck

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

















