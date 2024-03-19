# Arduino Object Detector Using Ultrasonic Sensor and Servo Motor

This Arduino project utilizes an ultrasonic sensor and a servo motor to detect objects within a certain range. The servo motor sweeps from one angle to another while the ultrasonic sensor measures the distance to detect any objects in its path.

## Installation

1. Clone this repository to your local machine using `git clone https://github.com/shivaganesht/arduino-object-detector.git`
2. Open the project in the Arduino IDE.

## Usage
![Arduino Object Detector Using Ultrasonic Sensor And Servo Motor](https://github.com/shivaganesht/arduino-object-detector/assets/69391183/44a26b93-877c-4ac9-ba61-292dd16c4972)

1. Connect your Arduino board to your computer.
2. Upload the code to your Arduino board.
3. The servo motor will sweep from 15 degrees to 165 degrees and back, while the ultrasonic sensor measures the distance to detect any objects.
4. The distance measurements will be printed to the serial monitor in the format `angle,distance`.

## Code Overview

```cpp
#include <Servo.h>

#define trigPin 8
#define echoPin 9

long duration;
int distance;

Servo myservo;

int calculateDistance()
{
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;
  return distance;
}

void setup()
{
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  myservo.attach(11);
  Serial.begin(9600);
}

void loop()
{
  int i;
  for (i = 15; i <= 165; i++)
  {
    myservo.write(i);
    delay(15);
    calculateDistance();
    Serial.print(i);
    Serial.print(",");
    Serial.print(distance);
    Serial.print(".");
  }
  for (i = 165; i >= 15; i--)
  {
    myservo.write(i);
    delay(15);
    calculateDistance();
    Serial.print(i);
    Serial.print(",");
    Serial.print(distance);
    Serial.print(".");
  }
}
```

## Conclusion

This project demonstrates how to use an ultrasonic sensor and a servo motor with Arduino to create an object detection system. The servo motor sweeps back and forth while the ultrasonic sensor measures the distance to detect objects. It can be further expanded and customized for various applications.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
