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
--------

The following is a breakdown of the code with comments explaining each command:

- ``#include <Arduino.h>``: This command includes the Arduino core library, which provides basic functions for working with the board.
- ``#include <esp_now.h>``: This command includes the ESP-NOW library, which provides functions for using the ESP-NOW protocol.
- ``#include <WiFi.h>``: This command includes the WiFi library, which provides functions for connecting to a WiFi network.
- ``uint8_t mac_peer1[] = { 0x48, 0x55, 0x19, 0xC6, 0x6E, 0x30 };``: This command defines the MAC address of the first device that will receive the force data.
- ``esp_now_peer_info_t peer1;``: This command defines a struct that contains information about the first device that will receive the force data.
- ``typedef struct force_data { uint16_t force_sensed_index = 0; uint16_t force_sensed_thumb = 0; };``: This command defines a struct that contains the force data sensed by the two sensors.
- ``struct force_data forceData;``: This command initializes the force_data struct.
- ``byte raw_value_index = 0, raw_value_thumb = 0; uint8_t received_value_index = 0, received_value_thumb = 0;``: These commands define variables for the raw and received force data.
- ``void setup() {...}``: This function is called once at the beginning of the program and is used to initialize the board.
- ``Serial.begin(115200);``: This command initializes the serial communication with a baud rate of 115200.
- ``WiFi.mode(WIFI_STA);``: This command sets the device as a WiFi Station, which allows it to connect to a WiFi network.
- ``if (esp_now_init() != ESP_OK) {...}``: This command initializes the ESP-NOW protocol and checks if it was initialized successfully.
- ``memcpy(peer1.peer_addr, mac_peer1, 6); peer1.channel = 1; peer1.encrypt = 0;``: These commands set the address, channel, and encryption settings for the first device that will receive the force data.
- ``if (esp_now_add_peer(&peer1) == ESP_OK) {...}``: This command adds the first device to the ESP-NOW network and checks if it was added successfully.
- ``void loop() {...}``: This function is called repeatedly and is used to execute the main program logic.
- ``if (Serial.available() > 1) {...}``: This command checks if there is serial data available to read.
- ``raw_value_index = (byte)(Serial.read()); raw_value_thumb = (byte)(Serial.read());``: These commands read the raw force data from the serial input.
- ``received_value_index = map((int)(raw_value_index), 36, 255, 0, 255); received_value_thumb = map((int)(raw_value_thumb), 36, 255, 0, 255);``: These commands map the raw force data to a range of 0-255 using the ``map()`` function.
- ``forceData.force_sensed_index = received_value_index; forceData.force_sensed_thumb = received_value_thumb;``: These commands store the mapped force data in the forceData struct.
- ``esp_now_send(peer1.peer_addr, (uint8_t *)&forceData, sizeof(forceData));``: This command sends the forceData struct to the first device using the ESP-NOW protocol.
- ``Serial.println("-----------------"); Serial.print("index finger: "); Serial.print(forceData.force_sensed_index); Serial.print("\tthumb: "); Serial.println(forceData.force_sensed_thumb);``: These commands print the force data to the serial monitor.

