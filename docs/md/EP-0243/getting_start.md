# Getting Started Guide with CAN NODE Controller

## Table of Contents

1. [Download and Install Arduino IDE](#download-and-install-arduino-ide)
2. [Connect the CAN NODE Controller Board](#connect-the-can-node-controller-board)
3. [Connect the Ethernet Cable](#connect-the-ethernet-cable)
4. [Connect the CAN Temperature Sensor Module](#connect-the-can-temperature-sensor-module)
5. [Upload a Sketch to Arduino UNO R4](#upload-a-sketch-to-arduino-uno-r4)
6. [Demo Code for CAN NODE controller](#demo-code-for-can-node-controller)
7. [Code Explainations](#code-explainations)

## Download and Install Arduino IDE

1. **Download Arduino IDE**: Visit the official Arduino website at [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software) to download the latest version of the Arduino IDE for your operating system.
2. **Install Arduino IDE**: Follow the installation instructions provided on the download page to install the IDE on your computer.

## Connect the CAN NODE Controller Board

1. **Locate the CAN NODE Controller Board**: Ensure you have the CAN NODE Controller Board and connect it to the Arduino UNO R4.
2. **Connect to Arduino UNO R4**: Connect the CAN NODE Controller Board to the Arduino UNO R4 using the appropriate headers or cables. Typically, this involves connecting the CAN high and CAN low lines to the corresponding pins on the Arduino board.

## Connect the Ethernet Cable

1. **Ethernet Connection**: Since your CAN NODE Controller Board uses an Ethernet cable for CAN protocol data, connect one end of the Ethernet cable to the board's Ethernet port.
2. **CAN Node Sensor Module Connection**: Connect the other end of the Ethernet cable to your CAN Temperature sensor module.

## Connect the CAN Temperature Sensor Module

1. **Identify the CAN Temperature Sensor Module**: Ensure you have the correct CAN Temperature Sensor Module.
2. **Connect to CAN NODE Controller Board**: Connect the CAN Temperature Sensor Module to the CAN NODE Controller Board according to the manufacturer's instructions,just connect the ethernet cable to it. 

## Upload a Sketch to Arduino UNO R4

1. **Open Arduino IDE**: Launch the Arduino IDE on your computer.
2. **Select the Correct Board**: Go to `Tools > Board` and select `YOUR_ARDUNO_BOARD_MODEL`.
3. **Select the Correct Port**: Go to `Tools > Port` and select the port to which your Arduino UNO R4 is connected.
4. **Write or Open a Sketch**: You can either write a new sketch or open an existing one. 
5. **Upload the Sketch**: Click the `Upload` button to compile and upload the sketch to your Arduino UNO R4.

## Demo code for CAN Node Controller

```cpp 
#include <Arduino_CAN.h>

void setup() {
    Serial.begin(115200); // initializing the serial port 
    while (!Serial) { }   // make sure the serial port is ready 

    if (!CAN.begin(CanBitRate::BR_250k))    // initializing CAN bus 
    {
        Serial.println("CAN.begin(...) failed.");
        for(;;){}
    }
}

void loop()
{
    float Temp;  // set a variable for Temperature sensor 

    if (CAN.available())
    {
        CanMsg const msg = CAN.read();  // read message from can bus

        uint8_t Length = msg.data_length; // get data length 

        Temp = msg.data[1] + msg.data[2] * 0.125;  // calculate the Temperature 

        Serial.println(msg.id) ;  // grab the msg.id to check if the sensor is
        valid sensor and make sure which one is which. 
        
        if (msg.id == 2620894157)  
            // CAN NODE Temperature Sensor Module in Dinning room. 
        {
            Serial.print("Dinning Room's Temperature: ");
            Serial.println(Temp);
        }

        if (msg.id == 2620566477) 
            // CAN NODE Temperature Sensor Module in Living room
        {
            Serial.print("Living Room's Temperature: ");
            Serial.println(Temp);
        }
    }
}

```

### Code Explainations

This code is an Arduino sketch designed to interact with a CAN (Controller Area Network) bus to read temperature data from two different rooms. Here's a summary of what each part of the code does:

- The `#include <Arduino_CAN.h>` directive includes the library necessary for CAN bus communication.
- The commented out `#include <LiquidCrystal_I2C.h>` and related code are for an I2C LCD display, which is not used in this sketch.

- In the `setup()` function:
  - The serial communication is initialized at a baud rate of 115200 for debugging purposes.
  - The code waits for the serial port to connect, which is useful for Leonardo boards.
  - It attempts to initialize the CAN bus at a bitrate of 250k. If initialization fails, it prints an error message and enters an infinite loop.

- In the `loop()` function:
  - The temperature variable `Temp` is declared to store the temperature readings.
  - The code checks if there is any message available on the CAN bus using `CAN.available()`.
  - If a message is available, it reads the message using `CAN.read()`.
  - It extracts the length of the message data and calculates the temperature from the first two data bytes of the message.
  - It prints the message ID to the serial monitor.
  - If the message ID matches a specific value (2620894157), it prints the temperature for the dining room.
  - If the message ID matches another value (2620566477), it prints the temperature for the bedroom.
  - The commented out sections are for displaying the temperature on an LCD display, which is not active in this code.
  - There is a commented out delay and lcd clear function, which are not used in this sketch.

Overall, the sketch is designed to read temperature data from a CAN bus and print the temperatures for two different rooms to the serial monitor.

### Congratulations!

You have successfully set up your Arduino UNO R4 with the CAN NODE Controller Board, Ethernet connection for CAN protocol, and CAN Temperature Sensor Module. You are now ready to start exploring more complex projects and experiments.

