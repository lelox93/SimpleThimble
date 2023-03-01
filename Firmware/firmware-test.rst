Firmware test code
++++++++++++++++++

To familiarize with the arduino IDE and write our first **firmware code**, we will write and upload a test code into our D1 mini microcontroller.
This code is an example of testing if your device is working as expected. 
It will help you verify that your device is functioning correctly and that all its components are working properly. 
This code will just move the servomotors as soon as the board is powered:

.. code-block:: arduino

    #include <Arduino.h>
    #include <ESP8266WiFi.h>
    #include <espnow.h>
    #include <Servo.h>

    Servo servo_idx;   // create servo object to control a servo
    Servo servo_thmb;  // create servo object to control a servo

    void setup() {
        Serial.begin(115200);
        delay(1000);
        servo_idx.attach(14);  // attaches the servo on pin D5 to the servo object
        servo_thmb.attach(12);  // attaches the servo on pin D6 to the servo object

        WiFi.disconnect();
        ESP.eraseConfig();

        servo_idx.write(0);
        servo_thmb.write(0);
        delay(500);
        servo_idx.write(50);
        servo_thmb.write(50);
        delay(500);
        servo_idx.write(0);
        servo_thmb.write(0);

        // Wifi STA Mode
        WiFi.mode(WIFI_STA);

        // Get Mac Add
        Serial.println();
        Serial.print("Mac Address: ");
        Serial.print(WiFi.macAddress());
    }

    void loop() {
        // loop does nothing.
    }
