# Other basic experiment Demo 

### Experiment 1: Blinking an LED

#### Application Scenario
Create a simple LED blinker to signal an event, such as a heartbeat monitor or a warning indicator.

#### Working Principle

The LED is connected to one of the GPIO pins of the Pico 2 WH. By toggling the pin's voltage between HIGH and LOW, the LED will turn on and off.

#### Circuit Wiring

1. Connect the longer leg (anode) of the LED to GPIO pin 15.
2. Connect the shorter leg (cathode) of the LED to a 220Ω resistor.
3. Connect the other end of the resistor to the GND pin on the Pico 2 WH.

#### MicroPython Demo Code

```python
from machine import Pin
import time

# Define the GPIO pin connected to the LED
led = Pin(15, Pin.OUT)

while True:
    led.value(1)  # Turn on the LED
    time.sleep(1)  # Wait for 1 second
    led.value(0)  # Turn off the LED
    time.sleep(1)  # Wait for 1 second
```

#### Code Explanation

* **Pin(15, Pin.OUT)**: Initializes GPIO pin 15 as an output pin.
* **led.value(1)**: Sets the pin to HIGH, turning on the LED.
* **time.sleep(1)**: Pauses the program for 1 second.
* **led.value(0)**: Sets the pin to LOW, turning off the LED.


### Experiment 2: Reading a Flame Sensor

#### Application Scenario

Detect the presence of fire or flame in a room for a safety monitoring system.

#### Working Principle

The flame sensor detects infrared light emitted by flames and outputs a digital signal (HIGH or LOW) based on the presence of fire.

#### Circuit Wiring

* Connect the VCC pin of the flame sensor to the 3.3V pin on the Pico 2 WH.
* Connect the GND pin of the flame sensor to the GND pin on the Pico 2 WH.
* Connect the OUT pin of the flame sensor to GPIO pin 14 on the Pico 2 WH.

#### MicroPython Demo Code 

```Python

from machine import Pin
import time

# Define the GPIO pin connected to the flame sensor
flame_sensor = Pin(14, Pin.IN)

while True:
    if flame_sensor.value() == 1:
        print("Flame detected!")
    else:
        print("No flame detected.")
    time.sleep(0.5)
```

#### Code Explanation

* **Pin(14, Pin.IN)**: Initializes GPIO pin 14 as an input pin.
* **flame_sensor.value()**: Reads the digital value from the flame sensor (1 for flame detected, 0 for no flame).
* **print()**: Outputs the result to the console.

### Experiment 3: Measuring Soil Moisture

#### Application Scenario
Monitor the moisture level of a plant's soil to automate watering.

#### Working Principle
The soil moisture sensor measures the conductivity of the soil. Higher conductivity indicates more moisture.

#### Circuit Wiring

* Connect the VCC pin of the soil moisture sensor to the 3.3V pin on the Pico 2 WH.
* Connect the GND pin of the sensor to the GND pin on the Pico 2 WH.
* Connect the OUT pin of the sensor to GPIO pin 13 on the Pico 2 WH.

#### MicroPython Demo Code

```Python
from machine import Pin
import time

# Define the GPIO pin connected to the soil moisture sensor
soil_sensor = Pin(13, Pin.IN)

while True:
    if soil_sensor.value() == 1:
        print("Soil is dry.")
    else:
        print("Soil is moist.")
    time.sleep(1)
```

#### Code Explanation

* **Pin(13, Pin.IN)**: Initializes GPIO pin 13 as an input pin.
* **soil_sensor.value()**: Reads the digital value from the soil moisture sensor (1 for dry soil, 0 for moist soil).
* **print()**: Outputs the moisture status to the console.

### Experiment 4: Controlling a Servo Motor

#### Application Scenario

Control a robotic arm or a small mechanical device using the servo motor.

#### Working Principle

The servo motor is controlled by a PWM (Pulse Width Modulation) signal. The position of the servo is determined by the duration of the pulse.

#### Circuit Wiring

* Connect the VCC pin of the servo to the 3.3V pin on the Pico 2 WH.
* Connect the GND pin of the servo to the GND pin on the Pico 2 WH.
* Connect the signal pin of the servo to GPIO pin 12 on the Pico 2 WH.

#### MicroPython Demo Code

```Python
from machine import Pin, PWM
import time

# Define the GPIO pin connected to the servo
servo = PWM(Pin(12), freq=50)  # 50 Hz PWM frequency for servo

while True:
    servo.duty(30)  # Set servo to 0 degrees
    time.sleep(1)
    servo.duty(77)  # Set servo to 90 degrees
    time.sleep(1)
    servo.duty(123)  # Set servo to 180 degrees
    time.sleep(1)
```

#### Code Explanation

* **PWM(Pin(12), freq=50)**: Initializes GPIO pin 12 as a PWM pin with a frequency of 50 Hz.
* **servo.duty()**: Sets the duty cycle to control the servo position (30 for 0°, 77 for 90°, 123 for 180°).
* **time.sleep(1)**: Pauses the program for 1 second.

### Experiment 5: Measuring Distance with an Ultrasonic Sensor

#### Application Scenario

Measure the distance to an object for applications like obstacle detection in robotics.

#### Working Principle

The ultrasonic sensor emits a sound wave and measures the time it takes for the echo to return. The distance is calculated using the speed of sound.

#### Circuit Wiring

* Connect the VCC pin of the ultrasonic sensor to the 3.3V pin on the Pico 2 WH.
* Connect the GND pin of the sensor to the GND pin on the Pico 2 WH.
* Connect the TRIG pin of the sensor to GPIO pin 11 on the Pico 2 WH.
* Connect the ECHO pin of the sensor to GPIO pin 10 on the Pico 2 WH.

#### MicroPython Demo Code

```Python
from machine import Pin, time_pulse_us
import time

# Define GPIO pins connected to the ultrasonic sensor
trig = Pin(11, Pin.OUT)
echo = Pin(10, Pin.IN)

while True:
    trig.value(0)
    time.sleep_us(2)
    trig.value(1)
    time.sleep_us(10)
    trig.value(0)
    
    pulse_time = time_pulse_us(echo, 1)
    distance = pulse_time * 0.034 / 2  # Speed of sound = 340 m/s
    print(f"Distance: {distance:.2f} cm")
    time.sleep(1)
```

#### Code Explanation
* **trig.value(1)**: Sends a short pulse to the TRIG pin to start the measurement.
* **time_pulse_us(echo, 1)**: Measures the duration of the ECHO pulse in microseconds.
* **distance = pulse_time * 0.034 / 2**: Calculates the distance in centimeters.
* **print()**: Outputs the distance to the console.

----

### Additional Experiments with Raspberry Pi Pico 2 WH

This section provides additional experiments using the Raspberry Pi Pico 2 WH and various sensors included in the starter kit. Each experiment includes a practical application scenario, an explanation of the working principle, circuit wiring instructions, and a MicroPython demo code with detailed explanations.

---

### Experiment 6: Detecting Light Intensity with a Light Sensor

#### Application Scenario

Create an automatic lighting system that turns on when the ambient light is too low.

#### Working Principle

The light sensor detects the intensity of ambient light and outputs an analog voltage proportional to the light level. This voltage can be read using the Pico 2 WH's ADC (Analog-to-Digital Converter).

#### Circuit Wiring

1. Connect the VCC pin of the light sensor to the 3.3V pin on the Pico 2 WH.
2. Connect the GND pin of the sensor to the GND pin on the Pico 2 WH.
3. Connect the OUT pin of the sensor to GPIO pin 26 (ADC0) on the Pico 2 WH.

#### MicroPython Demo Code

```python

from machine import ADC, Pin
import time

# Define the ADC pin connected to the light sensor
adc = ADC(Pin(26))

while True:
    light_value = adc.read_u16()  # Read the raw ADC value
    light_level = light_value / 65535 * 100  # Convert to percentage
    print(f"Light Level: {light_level:.2f}%")
    time.sleep(1)
```

#### Code Explanation

- `ADC(Pin(26))`: Initializes GPIO pin 26 as an ADC input.
- `adc.read_u16()`: Reads the raw 16-bit ADC value from the light sensor.
- `light_value / 65535 * 100`: Converts the raw value to a percentage.
- `print()`: Outputs the light level to the console.

---

### Experiment 7: Measuring Temperature with a Thermistor

#### Application Scenario

Monitor the temperature of a room or an object for a weather station or a heating system.

#### Working Principle

A thermistor is a temperature-sensitive resistor. Its resistance changes with temperature, and this change can be measured using the ADC.

#### Circuit Wiring

1. Connect one end of the thermistor to the 3.3V pin on the Pico 2 WH.
2. Connect the other end of the thermistor to GPIO pin 27 (ADC1).
3. Connect a 10kΩ resistor from GPIO pin 27 to GND.

#### MicroPython Demo Code

```python
from machine import ADC
import math
import time

# Define the ADC pin connected to the thermistor
adc = ADC(27)

# Thermistor constants (for a 10kΩ thermistor)
B = 3435
R0 = 10000  # Resistance at 25°C

while True:
    raw_value = adc.read_u16()
    voltage = raw_value / 65535 * 3.3  # Convert to voltage
    R = R0 * (1 / (math.exp((B / (298.15)) * (1 - (voltage / (3.3 - voltage))))))
    temperature = 1 / ((math.log(R / R0) / B) + (1 / 298.15)) - 273.15
    print(f"Temperature: {temperature:.2f}°C")
    time.sleep(1)
```

#### Code Explanation

- `ADC(27)`: Initializes GPIO pin 27 as an ADC input.
- `adc.read_u16()`: Reads the raw 16-bit ADC value.
- `voltage = raw_value / 65535 * 3.3`: Converts the raw value to voltage.
- `R = R0 * (1 / (math.exp((B / (298.15)) * (1 - (voltage / (3.3 - voltage)))))`: Calculates the resistance of the thermistor.
- `temperature = 1 / ((math.log(R / R0) / B) + (1 / 298.15)) - 273.15`: Converts resistance to temperature using the Steinhart-Hart equation.
- `print()`: Outputs the temperature to the console.

---

### Experiment 8: Detecting Sound with a Sound Sensor

#### Application Scenario

Create a noise detector to trigger an alarm when a loud sound is detected.

#### Working Principle

The sound sensor detects sound pressure levels and outputs a digital signal when the sound exceeds a certain threshold.

#### Circuit Wiring

1. Connect the VCC pin of the sound sensor to the 3.3V pin on the Pico 2 WH.
2. Connect the GND pin of the sensor to the GND pin on the Pico 2 WH.
3. Connect the OUT pin of the sensor to GPIO pin 16 on the Pico 2 WH.

#### MicroPython Demo Code

```python
from machine import Pin
import time

# Define the GPIO pin connected to the sound sensor
sound_sensor = Pin(16, Pin.IN)

while True:
    if sound_sensor.value() == 1:
        print("Loud sound detected!")
    else:
        print("No sound detected.")
    time.sleep(0.5)
```

#### Code Explanation

- `Pin(16, Pin.IN)`: Initializes GPIO pin 16 as an input pin.
- `sound_sensor.value()`: Reads the digital value from the sound sensor (1 for loud sound, 0 for no sound).
- `print()`: Outputs the sound detection status to the console.

---

### Experiment 9: Controlling a Buzzer

#### Application Scenario

Create an alarm system that buzzes when a specific condition is met (e.g., motion detected).

#### Working Principle

The buzzer generates sound by vibrating a diaphragm. It can be controlled by toggling the GPIO pin's voltage.

#### Circuit Wiring

1. Connect the positive pin of the buzzer to GPIO pin 17 on the Pico 2 WH.
2. Connect the negative pin of the buzzer to the GND pin on the Pico 2 WH.

#### MicroPython Demo Code

```python
from machine import Pin
import time

# Define the GPIO pin connected to the buzzer
buzzer = Pin(17, Pin.OUT)

while True:
    buzzer.value(1)  # Turn on the buzzer
    time.sleep(0.5)  # Buzz for 0.5 seconds
    buzzer.value(0)  # Turn off the buzzer
    time.sleep(1)  # Wait for 1 second
```

#### Code Explanation

- `Pin(17, Pin.OUT)`: Initializes GPIO pin 17 as an output pin.
- `buzzer.value(1)`: Sets the pin to HIGH, turning on the buzzer.
- `time.sleep(0.5)`: Pauses the program for 0.5 seconds.
- `buzzer.value(0)`: Sets the pin to LOW, turning off the buzzer.

---

### Experiment 10: Using a Rotary Encoder

#### Application Scenario

Create a volume control or menu navigation system using the rotary encoder.

#### Working Principle

The rotary encoder converts mechanical rotation into digital pulses. It outputs two signals (A and B) that can be used to determine rotation direction and speed.

#### Circuit Wiring

1. Connect the VCC pin of the rotary encoder to the 3.3V pin on the Pico 2 WH.
2. Connect the GND pin of the encoder to the GND pin on the Pico 2 WH.
3. Connect the A pin to GPIO pin 18.
4. Connect the B pin to GPIO pin 19.

#### MicroPython Demo Code

```python
from machine import Pin
import time

# Define GPIO pins connected to the rotary encoder
pin_a = Pin(18, Pin.IN)
pin_b = Pin(19, Pin.IN)

last_state = pin_a.value()
encoder_value = 0

def read_encoder():
    global last_state, encoder_value
    current_state = pin_a.value()
    if current_state != last_state:
        if pin_b.value() != current_state:
            encoder_value -= 1
        else:
            encoder_value += 1
    last_state = current_state

while True:
    read_encoder()
    print(f"Encoder Value: {encoder_value}")
    time.sleep(0.1)
```

#### Code Explanation

- `Pin(18, Pin.IN)` and `Pin(19, Pin.IN)`: Initializes GPIO pins 18 and 19 as input pins.
- `read_encoder()`: Reads the encoder signals and updates the encoder value based on the rotation direction.
- `print()`: Outputs the encoder value to the console.

---


### Conclusion

These experiments provide a foundation for using the Raspberry Pi Pico 2 WH with various sensors and components. Feel free to modify the code and circuit to suit your needs and explore more advanced applications!
Happy experimenting!

### Support

If you encounter any issues or have questions while using the kit, please refer to the instruction manual or contact our support team for assistance. We are here to help you on your journey into the exciting world of electronics and programming!

Happy experimenting with your Raspberry Pi Pico 2 WH Starter Kit!
