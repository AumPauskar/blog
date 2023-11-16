+++
title = 'Arduino'
date = 2023-11-16T10:37:04+05:30
draft = false
+++

# Arduino
14 IO, 6/\/\
ESP 8266 wifi

Sketch  - name of the program
Setup - IO setup
Loop - while loop
DHT 11 sol moisture
SR04 ultrasonic
HC05 bluetooth
ESP 01 wifi 

- Q. LED blink
```c
const int ledVar = 13;
void setup() {
  pinMode(ledVar, OUTPUT);
}

void loop() {
  digitalWrite(ledVar, HIGH);
  delay(1000);
  digitalWrite(ledVar, LOW);
  delay(1000);
}
```
- Q. Interface dht 11 with arduino uno and display humidity and temperature on serial monitor
```c
#include <dht.h>
dht DHT;
#define dhtPin 4

void setup() {
  Serial.begin(9600);

}

void loop() {
  // put your main code here, to run repeatedly:
  int val = DHT.read11(dhtPin);
  Serial.print("Temprature: ");
  Serial.println(DHT.temperature);
  Serial.print("Humidity: ");
  Serial.println(DHT.humidity);
  delay(2000);
}
```


- If else
```c
// Q. Interface dht 11 with arduino uno and display humidity and temperature on serial monitor
#include <dht.h>
dht DHT;
#define dhtPin 4
const int ledVar = 13;

void setup() {
  Serial.begin(9600);
  pinMode(ledVar, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  int val = DHT.read11(dhtPin);
  Serial.print("Temprature: ");
  // float temp = DHT.temperature;
  if ( DHT.temperature > 25.00) {
    digitalWrite(ledVar, HIGH);
  } else {
    digitalWrite(ledVar, LOW);
  }
  Serial.println(DHT.temperature);
  Serial.print("Humidity: ");
  Serial.println(DHT.humidity);
  delay(2000);
}
```


- Button operation
```c
const char led1 = A5;
const char led2 = A4;
const char led3 = A3;
const char led4 = A2;
const int b1 = 13;
const int b2 = 12;
const int b3 = 11;
const int b4 = 10;
int buttonState1, buttonState2, buttonState3, buttonState4;

void setup() {
  // put your setup code here, to run once:
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);
  pinMode(b1, INPUT);
  pinMode(b2, INPUT);
  pinMode(b3, INPUT);
  pinMode(b4, INPUT);
  Serial.begin(9600);
}

void loop() {
  // put your main code here, to run repeatedl
  if (digitalRead(b1) == LOW) {
    digitalWrite(led1, HIGH);
    digitalWrite(led2, LOW);
    digitalWrite(led3, LOW);
    digitalWrite(led4, LOW);
    
  } else if (digitalRead(b2) == LOW){
    digitalWrite(led1, LOW);
    digitalWrite(led2, HIGH);
    digitalWrite(led3, LOW);
    digitalWrite(led4, LOW);
  } else if (digitalRead(b3) == LOW){
    digitalWrite(led1, LOW);
    digitalWrite(led2, LOW);
    digitalWrite(led3, HIGH);
    digitalWrite(led4, LOW);
  } else if (digitalRead(b4) == LOW){
    digitalWrite(led1, LOW);
    digitalWrite(led2, LOW);
    digitalWrite(led3, LOW);
    digitalWrite(led4, HIGH);
  } else {
    digitalWrite(led1, LOW);
    digitalWrite(led2, LOW);
    digitalWrite(led3, LOW);
    digitalWrite(led4, LOW);
  }
}
```
- LCD
```c
#include <LiquidCrystal.h>
 const int rs = 6, en = 7, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
 LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

 
 void setup() {
  lcd.begin(16,2);
  lcd.print(" Hello ");
  lcd.setCursor(0,1);
  lcd.print(" World ");
}

void loop() {
  // put your main code here, to run repeatedly:
  lcd.noDisplay();
  lcd.display();
  delay(5000);
}
```

- IoT internship project
```c
/*Problem statement
Interface LCD with Arduino Uno to display the right to left 
scrolling message IoT Internship
*/
// title, problem statement, onjective, components, interfacing block diagram
// libraries
#include <LiquidCrystal.h>

// programming constants
const int rs = 6, en = 7, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
int initialDelay = 1000;
int pixelDelay = 300;
char message[] = "IoT Internship";

void setup() {
  lcd.begin(16, 2);
  lcd.print(message);
  delay(initialDelay);
}

void loop() {
  // given count values to properly scroll through the screen
  for (int positionCounter = 0; positionCounter < 13; positionCounter++) {
    lcd.scrollDisplayLeft();
    delay(pixelDelay);
  }

  for (int positionCounter = 0; positionCounter < 29; positionCounter++) {
    lcd.scrollDisplayRight();
    delay(pixelDelay);
  }
  for (int positionCounter = 0; positionCounter < 16; positionCounter++) {
    lcd.scrollDisplayLeft();
    delay(pixelDelay);
  }

  delay(1000);

}
```