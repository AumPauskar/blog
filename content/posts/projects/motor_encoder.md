+++
title = 'Modulated motor control with arduino'
date = 2023-11-21T22:20:04+05:30
draft = false
descrption = 'An IOT based solution for slot cutting in commutators'
+++

# Motor Encoder
![Sample](/images/cmc/display_and_4x4.png)

## Components
- Arduino Uno
- 4x4 Keypad
- I2C LCD
- DC Motor with encoder
- L293D Motor Driver

## Connections

### Display connections
| | From (I2C display) | To (arduino)|
| --- | --- | --- |
| 1 | VCC | 5V |
| 2 | GND | GND |
| 3 | SDA | SDA |
| 4 | SCL | SCL |

### Keypad connections
| | From (Keypad) | To (arduino)|
| --- | --- | --- |
| 1 | Row 1 | D13 |
| 2 | Row 2 | D12 |
| 3 | Row 3 | D11 |
| 4 | Row 4 | D10 |
| 5 | Col 1 | D9 |
| 6 | Col 2 | D8 |
| 7 | Col 3 | D7 |
| 8 | Col 4 | D4 |

### Motor connections
| | From (Motor) | To |
| --- | --- | --- |
| 1 | Motor negative | Output 4 (L293D) |
| 2 | Motor positive | Output 3 (L293D) |
| 3 | Encoder ground | GND (L293D) |
| 4 | Channel B | D3 (arduino) |
| 5 | Channel A | D2 (arduino) |
| 6 | Encoder power | 5V (arduino) |

### L293D connections
| | From (L293D) | To (arduino)|
| --- | --- | --- |
| 1 | Power 1 | 5V |
| 2 | Input 4 | D5 |
| 3 | Output 4 | refer above |
| 4 | Ground | GND (both arduino/motor) |
| 5 | Ground | GND (both arduino/motor) |
| 6 | Output 3 | refer above |
| 7 | Input 3 | D6 |
| 8 | Enable 3,4 | 5V |
| 9 | Enable 1,2 | 5V |
| 10 | Input 1 | N/A |
| 11 | Output 1 | N/A |
| 12 | Ground | GND |
| 13 | Ground | GND |
| 14 | Output 2 | N/A |
| 15 | Input 2 | N/A |
| 16 | Power 2 | 5V |

## Code
```c
// ----------
// keypad setup
#include <Keypad.h>

const byte numRows= 4; //number of rows on the keypad
const byte numCols= 4; //number of columns on the keypad

// global keypad variables
String enteredValue = "";
int encoderSpeed = 0;
float debugEncoderSpeed = 0.00; // (encoderSpeed * 100) / 255

//keymap defines the key pressed according to the row and columns just as appears on the keypad
char keymap[numRows][numCols]= 
{
{'1', '2', '3', 'A'}, 
{'4', '5', '6', 'B'}, 
{'7', '8', '9', 'C'},
{'*', '0', '#', 'D'}
};

//Code that shows the the keypad connections to the arduino terminals
byte rowPins[numRows] = {13,12,11,10}; //Rows 0 to 3
byte colPins[numCols]= {9,8,7,4}; //Columns 0 to 3

Keypad myKeypad= Keypad(makeKeymap(keymap), rowPins, colPins, numRows, numCols);

// ----------
// lcd setup
#include <Adafruit_LiquidCrystal.h>
Adafruit_LiquidCrystal lcd_1(0);
int LCDRow = 0;

#define motorA 5
#define motorB 6
int encoderPin1 = 2;
int encoderPin2 = 3;
volatile int lastEncoded = 0;
volatile long encoderValue = 0;
volatile long correctEncoderValue =0;
 
long lastencoderValue = 0;
 
int lastMSB = 0;
int lastLSB = 0;

void setup() {
  Serial.begin (9600);
  pinMode(encoderPin1, INPUT);
  pinMode(encoderPin2, INPUT);
  digitalWrite(encoderPin1, HIGH); //turn pullup resistor on
  digitalWrite(encoderPin2, HIGH); //turn pullup resistor on
  attachInterrupt(0, updateEncoder, CHANGE);
  attachInterrupt(1, updateEncoder, CHANGE);
  
  pinMode(motorA,OUTPUT);
  pinMode(motorB,OUTPUT);
  
  lcd_1.begin(16, 2);
  lcd_1.print("Enter value:");
  lcd_1.setCursor(LCDRow, 10);
}

void loop() {
  // encoder control statements
  correctEncoderValue = encoderValue/4;
  
  Serial.println(correctEncoderValue);
  
  if ( 0<=correctEncoderValue && correctEncoderValue < 3000) {
    analogWrite(motorA,encoderSpeed);
    digitalWrite(motorB,LOW);
  } else {
    analogWrite(motorA,0);
    digitalWrite(motorB,LOW);
  }
  delay(100);
  
  // keypad control statements
  char keypressed = myKeypad.getKey();
  if (keypressed != NO_KEY) {
  Serial.println(keypressed);
  }
  
  // getting the key pressed from the user
  if (keypressed){
    // gets triggered for numeric key presses
    if (keypressed != 'D' && keypressed != 'A' && keypressed != 'B' && keypressed != 'C') {
    	Serial.println(keypressed);
    	lcd_1.print(keypressed);
    	lcd_1.setCursor(++LCDRow, 10);
      enteredValue += keypressed;
    // a - clear the entered value
    } else if (keypressed == 'A') {
      lcd_1.clear();
      lcd_1.print("Enter value:");
      lcd_1.setCursor(++LCDRow, 10);
      enteredValue = "";
      encoderSpeed = 0;
    // d - update the entered value
    } else {
      LCDRow = 0;
      lcd_1.clear();
      lcd_1.print("Value updated");
      delay(500);

      // taking the encoder speed from the user
      // encoder value lies between 0 and 255
      // we take the value only if its between 0 and 255
      if (enteredValue == "") {
        encoderSpeed = 0;
        Serial.println("Case 1: Blank entered value");
      } else if (enteredValue.toInt() > 0 && enteredValue.toInt() < 255) {
        encoderSpeed = enteredValue.toInt();
        Serial.println("Case 2: Accepted entered value");
      } else {
        encoderSpeed = 0;
        Serial.println("Case 3: Out of of bounds entered value");
      }
    } // special keypresses end
  } // keypressed trigger end
  debugEncoderSpeed = (encoderSpeed * 100) / 255;
  Serial.println(debugEncoderSpeed);

}

void updateEncoder(){
  int MSB = digitalRead(encoderPin1); //MSB = most significant bit
  int LSB = digitalRead(encoderPin2); //LSB = least significant bit
 
  int encoded = (MSB << 1) |LSB; //converting the 2 pin value to single number
  int sum  = (lastEncoded << 2) | encoded; //adding it to the previous encoded value
 
  if(sum == 0b1101 || sum == 0b0100 || sum == 0b0010 || sum == 0b1011) encoderValue ++;
  if(sum == 0b1110 || sum == 0b0111 || sum == 0b0001 || sum == 0b1000) encoderValue --;
 
  lastEncoded = encoded; //store this value for next time
}
```
## How to use this
Click the link below and press simulate. You can see the debug output in the serial monitor. \
To enter a value press a key on the keypad. To update the value press `D` and to clear the value press `A`.

## Project link
[Click here](https://www.tinkercad.com/things/kJJREOZtcHx-cmc-design-prototype?sharecode=HJKZDsnFYIpmZhIDVKmV0iDLYmKJa7yxwVPAtEHZbDs)
## References
- [Arduino DC Motor with Encoder](https://www.tinkercad.com/things/ht6ujHLBsCy-encoder-motor-control)
- [4x4 keypad and display](https://www.tinkercad.com/things/fJzU6N77aHS-interfacing-4x4-keypad-and-16x2-lcd-with-arduino)