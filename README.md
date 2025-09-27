# OBSTACLE-DETECTION-SYSTEM-USING-ULTRASONIC-SENSOR

## Aim:
To design and simulate a distance measurement system using an ultrasonic sensor HC-SR04 interfaced with an Arduino Uno board in Tinkercad.

## Hardware / Software Tools required:
1.	Arduino Uno R3
2.	HC-SR04 Ultrasonic Distance Sensor
3.	Jumper Wires
4.	USB Cable (for simulation purpose in Tinkercad)

   
## Theory:

The ultrasonic distance sensor (HC-SR04) is a widely used electronic component for non-contact distance measurement. It operates on the principle of echo-ranging, where it emits an ultrasonic pulse and listens for its reflection from an object. The time taken for the echo to return is directly proportional to the distance of the object from the sensor. This sensor has two main pins—Trigger and Echo. The Trigger pin is used to send a short pulse (usually 10 microseconds), and the Echo pin receives the reflected signal. The Arduino microcontroller calculates the time interval between sending and receiving the ultrasonic pulse and converts it into distance using a specific formula. 
The speed of sound in air is approximately 343 meters per second (or 0.034 cm per microsecond). Since the sound travels to the object and back, the measured time is divided by 2. The formula used is: distance = (duration × 0.034) / 2. The sensor is highly suitable for robotics, object detection, and security systems where accurate distance measurement is crucial. The Arduino Uno serves as the brain of this project and controls the sensor, processes the pulse duration, and outputs the result via the serial monitor. 
Tinkercad provides a simulation environment where this circuit can be virtually built, connected, and tested. Through this setup, users can analyze how the sensor interacts with different distances, and visualize its output in real-time without requiring physical components. This setup not only helps in understanding sensor interfacing but also enhances coding skills through implementation in the Arduino IDE. It is an ideal beginner project for learning microcontroller and sensor interfacing.



## Circuit Diagram:
 
## Procedure: //Modify the procedure based on your circuit

Step 1: Set Up the Tinkercad Environment
1.	Log in to Tinkercad: Open Tinkercad in your web browser and log into your account.
2.	Create a New Circuit: In the Tinkercad dashboard, click on “Circuits”, then select “Create New Circuit” to open a new workspace.
Step 2: Add Components to the Circuit
3.	Arduino Uno: Drag and drop an Arduino Uno R3 board from the components panel onto the workspace.
4.	Ultrasonic Sensor: Search for the HC-SR04 Ultrasonic Distance Sensor and place it on the workspace.
5.	Wires: Use jumper wires to make electrical connections between components.
Step 3: Connect the Ultrasonic Sensor to the Arduino
6.	Ultrasonic Sensor Pins:
o	VCC Pin: Connect to 5V pin on the Arduino.
o	GND Pin: Connect to GND on the Arduino.
o	Trig Pin: Connect to Digital Pin 3 on the Arduino.
o	Echo Pin: Connect to Digital Pin 2 on the Arduino.


7.	Wire Connections:
o	Use the color-coded jumper wires (e.g., red for VCC, black for GND, green for Trig, and blue for Echo) to make it easier to identify connections.
Step 4: Write the Arduino Code
8.	Open Code Editor: Click on the “Code” button at the top right and switch to “Text” mode to write the code in C/C++.
Step 5: Simulate the Circuit
10.	Start Simulation: Click the green “Start Simulation” button at the top of the workspace to run the circuit and code.
11.	Monitor Output: Click the “Serial Monitor” at the bottom to view the live distance values being measured by the sensor in centimeters.
Step 6: Test and Validate
12.	Change Object Distance: Move the virtual object in front of the ultrasonic sensor and observe changes in distance readings in the serial monitor.
13.	Check Accuracy: Ensure the distance measurements vary correctly based on the object’s position.
Step 7: Save Your Work
14.	Stop Simulation: Click the “Stop Simulation” button to end the test.
15.	Save Circuit: Click “Save” to store your design and code for future use or presentation.


## Code:
~~~
// Obstacle Detection using HC-SR04 (Arduino)
// Trigger = D9, Echo = D10, LED = D6, Buzzer = D7
const int trigPin = 9;
const int echoPin = 10;
const int ledPin  = 6;
const int buzzerPin = 7;

long duration;
float distanceCM;
const float thresholdCM = 25.0; // change to set detection range

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  digitalWrite(ledPin, LOW);
  digitalWrite(buzzerPin, LOW);
  Serial.begin(9600);
}

void loop() {
  // send 10us pulse to trigger
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // read echo pulse duration (microseconds)
  duration = pulseIn(echoPin, HIGH, 30000); // timeout 30ms to avoid lock
  if (duration == 0) {
    // no echo received (out of range)
    distanceCM = -1;
  } else {
    // Convert to distance: Sound speed ~343 m/s → 29.1 µs per cm for round trip.
    // Common approximation: distance_cm = duration / 58.0
    distanceCM = duration / 58.0;
  }

  // Print to serial for debugging
  if (distanceCM > 0) {
    Serial.print("Distance: ");
    Serial.print(distanceCM);
    Serial.println(" cm");
  } else {
    Serial.println("Out of range");
  }

  // Obstacle detection logic
  if (distanceCM > 0 && distanceCM <= thresholdCM) {
    // Obstacle detected
    digitalWrite(ledPin, HIGH);
    // buzzer beep pattern
    tone(buzzerPin, 1000); // 1kHz tone
  } else {
    digitalWrite(ledPin, LOW);
    noTone(buzzerPin);
  }

  delay(150); // small delay between measurements
}
~~~

## Output:
~~~~
 https://go.screenpal.com/watch/cTQtfXnDtZX
~~~

## Result


Result:
The simulation successfully measured the distance between the ultrasonic sensor  HC-SR04 and the object. The real-time distance values were accurately displayed on the serial monitor in centimeters.
