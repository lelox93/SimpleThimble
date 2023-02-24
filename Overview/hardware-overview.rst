Hardware Overview of Simple Thimble
===================================

Simple Thimble is a DIY haptic thimble that provides tactile feedback to the user. It is designed to be easy to assemble and use, and can be used for a variety of applications.

.. caution::
    The project mechanics has been designed to be self produced with low-cost FDM (fused deposition modeling) 3D printing

.. danger:: 
    To obtain properly working 3D printed mechanical parts, you may need to file some parts to make them fit together. Moreover, soldering parts is needed to make this project.
    Always wear the proper **safety equipment**. This includes ``safety glasses`` to protect your eyes from flying debris, a ``face mask`` to protect your lungs from fumes, and ``gloves`` to protect your hands from heat and sharp edges. Additionally, it is important to work in a *well-ventilated* area to reduce the risk of inhaling toxic fumes.


Components
----------

Simple Thimble consists of the following components:

-   an ESP32 microcontroller
-   an ESP8266 microcontroller (WeMoS D1 mini)
-   a battery shield for the D1 mini board
-   a Li-Po 3.7V battery
-   a standard SG90 servomotor
-   a switch

-   3D printed thimble parts

Parts role inside the thimble
-----------------------

#.  Connect the haptic motor to the Arduino Uno board using the provided wires and connectors. 
#.  Place the haptic motor inside the 3D printed thimble housing. 
#.  Connect the 9V battery to the Arduino Uno board. 
#.  Secure the thimble housing with screws. 
#.  Connect the Arduino Uno board to a computer via USB cable and upload the code. 
#.  Test the Simple Thimble by pressing the button on the Arduino Uno board. 