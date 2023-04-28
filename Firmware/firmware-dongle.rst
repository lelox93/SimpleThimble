The dongle firmware code 
++++++++++++++++++++++++++++

This firmware enables an ESP32 device to function as a dongle that can read serial data from a connected device 
and transmit it wirelessly to an ESP8266 device using the ESP-NOW protocol.

The ESP32 dongle reads serial data from a connected device and transmits it wirelessly to the ESP8266 device 
using the low-power ESP-NOW protocol, which is specifically designed for IoT devices.

The code to upload tot he ESP32 dongle is the following:

.. code-block:: arduino

    #include <Arduino.h>
    #include <esp_now.h>
    #include <WiFi.h>

    // Define ESP8266 Mac address (first peer)
    uint8_t mac_peer1[] = { 0x48, 0x55, 0x19, 0xC6, 0x6E, 0x30 };

    // Define peer info struct for first device
    esp_now_peer_info_t peer1;

    // Define struct containing force sensed data
    typedef struct force_data {
    uint16_t force_sensed_index = 0;
    uint16_t force_sensed_thumb = 0;
    };

    // Initialize force_data struct
    struct force_data forceData;

    // Define variables for raw and received force sensed data
    byte raw_value_index = 0, raw_value_thumb = 0;
    uint8_t received_value_index = 0, received_value_thumb = 0;


    void setup() {
        // Start serial communication
        Serial.begin(115200);

        // Set device as a Wi-Fi Station
        WiFi.mode(WIFI_STA);

        // Init ESP-NOW
        if (esp_now_init() != ESP_OK) {
            Serial.println("Error initializing ESP-NOW");
            return;
        }

        // Set peer1's address and channel, and disable encryption
        memcpy(peer1.peer_addr, mac_peer1, 6);
        peer1.channel = 1;
        peer1.encrypt = 0;

        // Register peer1
        Serial.println("Registering a peer 1");
        if (esp_now_add_peer(&peer1) == ESP_OK) {
            Serial.println("Peer 1 added");
        }
    }


    void loop() {
        // Check for available serial data
        if (Serial.available() > 1) {

            // Read raw force sensed data from serial input
            raw_value_index = (byte)(Serial.read());
            raw_value_thumb = (byte)(Serial.read());

            // Map raw force sensed values to a range of 0-255
            received_value_index = map((int)(raw_value_index), 36, 255, 0, 255);
            received_value_thumb = map((int)(raw_value_thumb), 36, 255, 0, 255);

            // Store mapped force sensed values in forceData struct
            forceData.force_sensed_index = received_value_index;
            forceData.force_sensed_thumb = received_value_thumb;

            // Send forceData to peer1 using ESP-NOW
            esp_now_send(peer1.peer_addr, (uint8_t *)&forceData, sizeof(forceData));

            // Print force sensed data to serial monitor
            Serial.println("-----------------");
            Serial.print("index finger: ");
            Serial.print(forceData.force_sensed_index);
            Serial.print("\tthumb: ");
            Serial.println(forceData.force_sensed_thumb);
        }
    }


|

Commands
========

The following is a breakdown of the code with comments explaining each command:

Libraries and Struct Definition
-------------------------------
The following code defines a struct named force_data which contains two variables representing the force sensed on the index and thumb fingers.

.. code-block:: arduino
    
    #include <Arduino.h>
    #include <esp_now.h>
    #include <WiFi.h>

    // Define struct containing force sensed data
    typedef struct force_data {
    uint16_t force_sensed_index = 0;
    uint16_t force_sensed_thumb = 0;
    };

    // Initialize force_data struct
    struct force_data forceData;

    // Define variables for raw and received force sensed data
    byte raw_value_index = 0, raw_value_thumb = 0;
    uint8_t received_value_index = 0, received_value_thumb = 0;


Setup Function
--------------
The following code is the setup function which runs once at the beginning of the code:
Starts serial communication
Sets device as a Wi-Fi Station
Initializes ESP-NOW
Sets peer1's address and channel, and disables encryption
Registers peer1.

.. code-block:: arduino
    
    void setup() {
        // Start serial communication
        Serial.begin(115200);

        // Set device as a Wi-Fi Station
        WiFi.mode(WIFI_STA);

        // Init ESP-NOW
        if (esp_now_init() != ESP_OK) {
            Serial.println("Error initializing ESP-NOW");
            return;
        }

        // Set peer1's address and channel, and disable encryption
        memcpy(peer1.peer_addr, mac_peer1, 6);
        peer1.channel = 1;
        peer1.encrypt = 0;

        // Register peer1
        Serial.println("Registering a peer 1");
        if (esp_now_add_peer(&peer1) == ESP_OK) {
            Serial.println("Peer 1 added");
        }
    }

Loop Function
-------------
The following code is the loop function, which runs continuously while the device is powered. It checks for available serial data, reads the raw force sensed data from serial input, maps the raw force sensed values to a range of 0-255, stores the mapped force sensed values in forceData struct, and sends forceData to peer1 using ESP-NOW.

.. code-block:: arduino

    void loop() {
    // Check for available serial data
    if (Serial.available() > 1) {

        // Read raw force sensed data from serial input
        raw_value_index = (byte)(Serial.read());
        raw_value_thumb = (byte)(Serial.read());

        // Map raw force sensed values to a range of 0-255
        received_value_index = map((int)(raw_value_index), 36, 255, 0, 255);
        received_value_thumb = map((int)(raw_value_thumb), 36, 255, 0, 255);

        // Store mapped force sensed values in forceData struct
        forceData.force_sensed_index = received_value_index;
        forceData.force_sensed_thumb = received_value_thumb;

        // Send forceData to peer1 using ESP-NOW
        esp_now_send(peer1.peer_addr, (uint8_t *)&forceData, sizeof(forceData));

        // Print force sensed data to serial monitor
        Serial.println("-----------------");
        Serial.print("index finger: ");
        Serial.print(forceData.force_sensed_index);
        Serial.print("\tthumb: ");
        Serial.println(forceData.force_sensed_thumb);
    }
    }