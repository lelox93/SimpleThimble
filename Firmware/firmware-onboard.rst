The final Simple Thimble onboard firmware
+++++++++++++++++++++++++++++++++++++++++++++
.. _onboardFirmware:

This firmware enables an ESP8266 device to receive data using the ESP-NOW protocol.

The code to upload to the ESP8266 device is the following:

.. code-block:: arduino
    
    #include <Arduino.h>
    #include <ESP8266WiFi.h>
    #include <espnow.h>
    #include <Servo.h>

    // Define struct containing force sensed data
    typedef struct force_data {
    uint16_t force_sensed_index = 0;
    uint16_t force_sensed_thumb = 0;
    } force_data;

    // Initialize force_data struct
    struct force_data forceData;

    // Create servo objects
    Servo servo_index;
    Servo servo_thumb;

    // Define Master Mac address
    uint8_t macMaster[] = {0x40, 0x22, 0xD8, 0x3C, 0x1C, 0xCC};

    // Initialize other auxiliary variables
    int limit = 180;
    int offset_index = 0;
    int offset_thumb = 0;

    // Define the callback function connected to the event of receiving ESP-NOW data
    void onDataReceiver(uint8_t * mac, uint8_t *incomingData, uint8_t len) {
    memcpy(&forceData, incomingData, sizeof(forceData));
    servo_index.write(map(forceData.force_sensed_index, 0, 255, offset_index, limit));
    servo_thumb.write(map(forceData.force_sensed_thumb, 0, 255, offset_thumb, limit));
    ESP.wdtFeed();
    }

    void setup() {
    // Start serial communication
    Serial.begin(115200);

    // Attach the servos to their respective pins
    servo_index.attach(14);   // pin D5
    servo_thumb.attach(12);   // pin D6

    // Disconnect from WiFi and erase the stored config
    WiFi.disconnect();
    ESP.eraseConfig();

    // Start up sequence
    servo_index.write(0);
    servo_thumb.write(0);
    delay(500);
    servo_index.write(50);
    servo_thumb.write(50);
    delay(500);
    servo_index.write(0);
    servo_thumb.write(0);

    // Set device as a Wi-Fi Station
    WiFi.mode(WIFI_STA);

    // Init ESP-NOW
    if (esp_now_init() != 0) {
        Serial.println("Error initializing ESP-NOW");
        return;
    }

    // Set the device to act as both a sender and receiver using ESP-NOW
    esp_now_set_self_role(ESP_NOW_ROLE_COMBO);
    
    // Add the MAC address of the master device as a peer for ESP-NOW communication
    esp_now_add_peer(macMaster, ESP_NOW_ROLE_COMBO, 1, NULL, 0);

    // We can register the receiver callback function
    esp_now_register_recv_cb(onDataReceiver);
    }

    void loop() {
    // loop does nothing
    }


|

Commands
========

The following is a breakdown of the code with comments explaining each command:

Libraries and Struct Definition
--------------------------------
The following code defines a struct named force_data which contains two variables representing the force sensed on the index and thumb fingers.

.. code-block:: arduino

    #include <Arduino.h>
    #include <ESP8266WiFi.h>
    #include <espnow.h>
    #include <Servo.h>
    
    typedef struct force_data {
        uint16_t force_sensed_index = 0;
        uint16_t force_sensed_thumb = 0;
    } force_data;

    struct force_data forceData;

Create Servo Objects and Define Auxiliary Variables
---------------------------------------------------
The following code creates objects for two servos named servo_index and servo_thumb and defines some auxiliary variables for the code.

.. code-block:: arduino

    Servo servo_index;
    Servo servo_thumb;

    int limit = 180;
    int offset_index = 0;
    int offset_thumb = 0;


Callback Function for ESP-NOW Data Reception
---------------------------------------------
The following code defines a callback function that will be called whenever the device receives data using ESP-NOW. It copies the incoming 
data into the forceData struct, maps the force values to the servo positions, and feeds the ESP watchdog timer.

.. code-block:: arduino

    void onDataReceiver(uint8_t * mac, uint8_t *incomingData, uint8_t len) {
        memcpy(&forceData, incomingData, sizeof(forceData));
        servo_index.write(map(forceData.force_sensed_index, 0, 255, offset_index, limit));
        servo_thumb.write(map(forceData.force_sensed_thumb, 0, 255, offset_thumb, limit));
        ESP.wdtFeed();
    }

Setup Function
--------------

The following code is the setup function which runs once at the beginning of the code. It initializes the serial communication, attaches the servos to their pins, disconnects from any previous WiFi connections, performs a servo startup sequence, sets the device as a Wi-Fi station, initializes ESP-NOW and sets the device as both a sender and receiver, adds the master device as a peer for ESP-NOW communication, and registers the callback function for receiving data.

.. code-block:: arduino

    void setup() {
        Serial.begin(115200);

        servo_index.attach(14);
        servo_thumb.attach(12);

        WiFi.disconnect();
        ESP.eraseConfig();

        servo_index.write(0);
        servo_thumb.write(0);
        delay(500);
        servo_index.write(50);
        servo_thumb.write(50);
        delay(500);
        servo_index.write(0);
        servo_thumb.write(0);

        WiFi.mode(WIFI_STA);

        if (esp_now_init() != 0) {
          Serial.println("Error initializing ESP-NOW");
          return;
        }

        esp_now_set_self_role(ESP_NOW_ROLE_COMBO);
        esp_now_add_peer(macMaster, ESP_NOW_ROLE_COMBO, 1, NULL, 0);

        esp_now_register_recv_cb(onDataReceiver);
   }


Loop Function
--------------

The following code is the loop function, which runs continuously while the device is powered. It currently does nothing.

.. code-block:: arduino
    
    void loop() {
        // loop does nothing
    }