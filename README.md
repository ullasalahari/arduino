# arduino
# Ultrasonic Distance Meter using Arduino Uno (HC-SR04)

A beginner-friendly Arduino project that measures the distance to an object using an **HC-SR04 Ultrasonic Sensor**, an **Arduino Uno**, and **jumper wires**, displaying real-time distance readings in centimeters on the Serial Monitor.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Components Required](#components-required)
- [Circuit Connections](#circuit-connections)
- [Arduino Code](#arduino-code)
- [Sample Output Preview](#sample-output-preview)
- [How It Works](#how-it-works)
- [Getting Started](#getting-started)
- [Author](#author)

---

## 📖 Overview
This project uses ultrasonic sound waves to calculate the distance between the HC-SR04 sensor and an obstacle. It is built purely with basic hardware components and is ideal for beginners learning sensor interfacing and serial communication.

---

## 🛠️ Components Required
* **Microcontroller:** Arduino Uno
* **Sensor:** HC-SR04 Ultrasonic Sensor
* **Wiring:** Male-to-Female Jumper Wires (4 wires)
* **Cable:** USB Type-B Cable (to connect Arduino Uno to PC)
* **Software:** Arduino IDE

---

## 🔌 Circuit Connections

Connect the 4 pins of the HC-SR04 sensor directly to the Arduino Uno using jumper wires:

| HC-SR04 Pin | Arduino Uno Pin | Description |
| :--- | :--- | :--- |
| **VCC** | `5V` | Power Supply |
| **GND** | `GND` | Ground |
| **Trig** | `Digital Pin 9` | Trigger Input (Sends ultrasonic pulse) |
| **Echo** | `Digital Pin 10` | Echo Output (Receives reflected pulse) |

---

## 💻 Arduino Code

```cpp
// Define the pins connected to the sensor
const int trigPin = 9;
const int echoPin = 10;

// Variables to store the travel time and calculated distance
long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT);  // Sets the echoPin as an Input
  Serial.begin(9600);       // Starts serial communication at 9600 baud
}

void loop() {
  // Clear the trigPin by setting it LOW
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  // Send a 10-microsecond HIGH pulse to trigger the ultrasonic burst
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Read the echoPin and return the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);

  // Calculate the distance in centimeters
  // Speed of sound is ~0.034 cm/us; divide by 2 for the round trip
  distance = duration * 0.034 / 2;

  // Print the distance to the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  delay(200); // Wait 200 milliseconds before the next reading
}
```

---

## 🖥️ Sample Output Preview

When you open the **Serial Monitor** in the Arduino IDE (at **9600 baud**), you will see live distance readings updating every 200 milliseconds as you move an object in front of the sensor:

```text
Distance: 45 cm
Distance: 44 cm
Distance: 32 cm
Distance: 18 cm
Distance: 10 cm
Distance: 10 cm
```

---

## ⚙️ How It Works
1. The Arduino sends a **10-microsecond HIGH pulse** to the `Trig` pin.
2. The HC-SR04 emits an 8-cycle ultrasonic burst at **40 kHz**.
3. When the sound wave hits an object, it bounces back to the `Echo` pin.
4. The Arduino measures the travel time (`duration`) using the `pulseIn()` function and calculates distance using the speed of sound (`0.034 cm/µs`):
   $$\text{Distance (cm)} = \frac{\text{Duration} \times 0.034}{2}$$

---

## 🚀 Getting Started

1. **Wire the Circuit:** Connect the HC-SR04 sensor to the Arduino Uno using jumper wires according to the pin table above.
2. **Connect to PC:** Plug your Arduino Uno into your computer using the USB cable.
3. **Open Code:** Open the `.ino` file in the **Arduino IDE**.
4. **Select Board & Port:** Go to `Tools > Board` and select **Arduino Uno**, then go to `Tools > Port` and select your active COM port.
5. **Upload:** Click the **Upload** button (`→`) in the top-left corner.
6. **View Readings:** Open the **Serial Monitor** (`Ctrl + Shift + M`), set the baud rate to **9600**, and place your hand or an object in front of the sensor to see live measurements.
