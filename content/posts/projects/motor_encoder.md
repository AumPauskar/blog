+++
title = 'Motor_encoder'
date = 2023-11-21T22:20:04+05:30
draft = false
+++

# Motor Encoder
![Sample](/images/cmc/display_and_4x4.png)

## Components
- Arduino Uno
- 4x4 Keypad
- I2C LCD
- DC Motor with encoder

## Connections
pending
## Code
```c
// ----------
// keypad setup
#include <Keypad.h>

const byte numRows= 4; //number of rows on the keypad
const byte numCols= 4; //number of columns on the keypad

// global keypad variables
String enteredValue = "";

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
   correctEncoderValue = encoderValue/4;
  
   Serial.println(correctEncoderValue);
  
  if ( 0<=correctEncoderValue && correctEncoderValue < 3000) {
   analogWrite(motorA,127);
   digitalWrite(motorB,LOW);
  } else {
   analogWrite(motorA,0);
   digitalWrite(motorB,LOW);
  }
   delay(100);
  
  char keypressed = myKeypad.getKey();
  if (keypressed != NO_KEY)
  {
  Serial.println(keypressed);
  }
  
  if (keypressed){
    if (keypressed != 'D' && keypressed != 'A') {
    	Serial.println(keypressed);
    	lcd_1.print(keypressed);
    	lcd_1.setCursor(++LCDRow, 10);
    } else if (keypressed == 'A') {
      	lcd_1.clear();
        lcd_1.print("Enter value:");
      	lcd_1.setCursor(++LCDRow, 10);
    } else {
      LCDRow = 0;
      lcd_1.clear();
      lcd_1.print("Value updated");
      delay(500);
    }
  }

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