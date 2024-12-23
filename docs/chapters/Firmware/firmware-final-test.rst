One final test for the Simple Thimble firmware
+++++++++++++++++++++++++++++++++++++++++++++
In this section we will make sure that all firmwares we uploaded to the microcontrollers 
work together.

To do this we have to connect just the dongle to one of our USB ports and battery-power the 
thimble microcontroller with the servomotors attached.

Once everything is wired, we can use the ``Tools -> Serial Monitor`` to write data directly to the dongle via USB.
This will result in the dongle sending this serial data wirlessly to the other board controlling the thimbles via 
ESP-NOW protocol.

In the next animated image you can see this final test performed: the user types the characters "AA" and "zz" to the 
serial port with the result of the thimbles moving to reach this positional command

|
.. image:: firmware-final-test.gif
   :alt: pref
   :width: 700 px
   :align: center

|