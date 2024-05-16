+++
title = 'Lab expts sem 6'
date = 2024-03-23T15:34:19+05:30
tags = ["ai", "ml", "lab", "sem6", "expts", "network", "shell", "linux", "artificial intelligence", "machine learning"]
author = "Aum Pauskar, Shriram Naik"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Lab experiments of semester 6, has AIML temworks and unix based network programming"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Lab expts sem 6

## AIML

- Depth first search code

```py
def iterative_deepening_dfs(start, target, max_depth):
    depth = 0
    print("Depth: ", depth)
    bottom_reached = False
    while not bottom_reached and depth <= max_depth:
        result, path, bottom_reached = iterative_deepening_dfs_rec(
            start, target, 0, depth, [])
        if result is not None:
            return result
        depth += 1
        print("Increasing depth to " + str(depth), "\n")
    return None


def iterative_deepening_dfs_rec(node, target, current_depth, max_depth, path):
    print("Visiting Node " + str(node["value"]))
    if node["value"] == target:
        print("Found the node we're looking for!")
        return node, path, True
    if current_depth == max_depth:
        if len(node["children"]) > 0:
            return None, path, False
        else:
            return None, path, True
    bottom_reached = True
    for i in range(len(node["children"])):
        result, path_copy, bottom_reached_rec = iterative_deepening_dfs_rec(node["children"][i], target, current_depth + 1,
                                                                            max_depth, path + [node["value"]])
        if result is not None:
            return result, path_copy, True
        bottom_reached = bottom_reached and bottom_reached_rec
    return None, path, bottom_reached


def print_tree(node, prefix="", is_tail=True):
    print(prefix + ("└── " if is_tail else "├── ") + str(node["value"]))
    if node["children"]:
        for i, child in enumerate(node["children"]):
            print_tree(child, prefix + ("    " if is_tail else "│   "),
                       i == len(node["children"]) - 1)


tree = {
    "value": 1,
    "children": [
        {
            "value": 2,
            "children": [
                {"value": 5, "children": []},
                {"value": 6, "children": []}
            ]
        },
        {
            "value": 3,
            "children": [
                {"value": 7, "children": []},
                {"value": 8, "children": []}
            ]
        },
        {
            "value": 4,
            "children": [
                {"value": 9, "children": []},
                {"value": 10, "children": []}
            ]
        }
    ]
}

print("\nTree structure:")
print_tree(tree)

target_value = 10
print("\nTarget node:", target_value)

max_depth = 2
print("\n Max depth:", max_depth)
result_node = iterative_deepening_dfs(tree, target_value, max_depth)
if result_node:
    print("\nTarget node found:", result_node["value"])
else:
    print("\nTarget node not found in the tree.")
```

- Deapth first search code
```py
import heapq

class Node:
    def __init__(self, value, priority):
        self.value = value
        self.priority = priority
        self.visited = False
        self.adjacents = []

    def add_adjacent(self, node):
        self.adjacents.append(node)

class PriorityQueue:
    def __init__(self):
        self._queue = []
        self._index = 0

    def push(self, item, priority):
        heapq.heappush(self._queue, (priority, self._index, item))
        self._index += 1

    def pop(self):
        return heapq.heappop(self._queue)[-1]

def best_first_search(start, target):
    queue = PriorityQueue()
    queue.push((start, [start.value]), start.priority)  # Push a tuple of the node and the path

    while queue:
        current_node, path = queue.pop()  # Unpack the node and the path
        current_node.visited = True

        if current_node == target:
            return path  # Return the path if the target is found

        for adj in current_node.adjacents:
            if not adj.visited:
                queue.push((adj, path + [adj.value]), adj.priority)  # Add the node to the path

    return None  # Return None if no path is found



# Create nodes
nodeA = Node("A", 3)
nodeB = Node("B", 1)
nodeC = Node("C", 2)
nodeD = Node("D", 1)
nodeE = Node("E", 2)
nodeF = Node("F", 3)

# Add adjacents
nodeA.add_adjacent(nodeB)
nodeA.add_adjacent(nodeC)
nodeB.add_adjacent(nodeD)
nodeB.add_adjacent(nodeE)
nodeC.add_adjacent(nodeF)

# Perform search
path = best_first_search(nodeA, nodeF)

# Print result
if path:
    print("Path exists! Path:", ' -> '.join(path))
else:
    print("No path exists.")
```

- Dijkstra's algorithm
```py
import heapq

class Node:
    def __init__(self, value):
        self.value = value
        self.distance = float('inf')
        self.visited = False
        self.adjacents = []
        self.previous = None

    def add_adjacent(self, node, weight):
        self.adjacents.append((node, weight))

class PriorityQueue:
    def __init__(self):
        self._queue = []
        self._index = 0

    def push(self, item, priority):
        heapq.heappush(self._queue, (priority, self._index, item))
        self._index += 1

    def pop(self):
        return heapq.heappop(self._queue)[-1]

    def is_empty(self):
        return len(self._queue) == 0

def dijkstra(start):
    start.distance = 0
    queue = PriorityQueue()
    queue.push(start, start.distance)

    while not queue.is_empty():
        current_node = queue.pop()
        current_node.visited = True

        for adj, weight in current_node.adjacents:
            if not adj.visited:
                old_distance = adj.distance
                new_distance = current_node.distance + weight

                if new_distance < old_distance:
                    adj.distance = new_distance
                    adj.previous = current_node
                    queue.push(adj, adj.distance)
# Create nodes
nodeA = Node("A")
nodeB = Node("B")
nodeC = Node("C")
nodeD = Node("D")
nodeE = Node("E")
nodeF = Node("F")

# Add adjacents and weights
nodeA.add_adjacent(nodeB, 1)
nodeA.add_adjacent(nodeC, 3)
nodeB.add_adjacent(nodeD, 2)
nodeB.add_adjacent(nodeE, 3)
nodeC.add_adjacent(nodeF, 2)

# Perform Dijkstra's algorithm
dijkstra(nodeA)

# Print shortest path to each node
nodes = [nodeA, nodeB, nodeC, nodeD, nodeE, nodeF]
for node in nodes:
    path = []
    current = node
    while current is not None:
        path.append(current.value)
        current = current.previous
    path.reverse()
    print(' -> '.join(path))

```
## USP

### Running a code

We shall use fedora to run most of the code. The code will be written in ANSI C and. \
To run the code, we shall use the following commands:

```shell
gedit <filename.c>
cc filename.c
./a.out
```

**Sample code**

```c
#include <stdio.h>
int main()
{
    #if __STDC__ == 0
    printf("CC is not ANSI C compliant");
    #else
    printf("%s compiled at %s %s this statement at line %d", __FILE__, __TIME__, __DATE__, __LINE__);
    #endif
    return 0;
}
```

In order to compile and run this code open a **new instance in the terminal** and execute the following commands:

```shell
cc <filename.c> -o <filename.out>
./filename.out
```

A **shorter version** to run this code is

```shell
cc <filename.c> -o <filename.out> && ./filename.out
```

This can be done for same in a c++ file. To initialte a c++ file, use the following command:

```shell
gedit <filename.cpp>
```

To compile and execute the file run the following commands:

```shell
g++ <filename.cpp> -o <filename.out>
./filename.out
```

Similarly to the c file to run the command in one single line use the following command:

```shell
g++ <filename.cpp> -o <filename.out> && ./filename.out
```

**Checking the version of posix**

```cpp
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 199309L
#include <stdio.h>
#include <unistd.h>
#include <iostream.h>

using namespace std;

int main() {
    #ifdef _POSIX_VERSION
        cout << "POSIX compliant" << _POSIX_VERSION << endl;
    #else
        cout << "POSIX version is not defined" << endl;
    #endif
    return 0;
}
```
### TW1 - runtime constraints in C++

```cpp
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 1993309L
#include <iostream>
#include <limits.h>
#include <unistd.h>

using namespace std;

void compileTime() {
    cout << "\n\nMANIFEST CONSTANTS\n\n";
    #ifdef _SC_CLK_TCK
        cout << "SYSTEM SUPPORTS CLK_TCK which is " << _SC_CLK_TCK << endl;
    #else
        cout << "SYSTEM DOES NOT SUPPORT CLK_TCK" << endl;
    #endif

    #ifdef _POSIX_CHILD_MAX
        cout << "Man number of child processes is " << _POSIX_CHILD_MAX << endl;
    #else
        cout << "CHILD_MAX is not defined" << endl;
    #endif

    #ifdef _POSIX_PATH_MAX
        cout << "Maximum path length is " << _POSIX_PATH_MAX << endl;
    #else
        cout << "PATH_MAX is not defined" << endl;
    #endif
    #ifdef _POSIX_OPEN_MAX
        cout << "Maximum number of open files per process is " << _POSIX_OPEN_MAX << endl; 
    #else
        cout << "OPEN_MAX is not defined" << endl;
    #endif
    #ifdef _POSIX_NAME_MAX
        cout << "Maximum number of characters in a filename is " << _POSIX_NAME_MAX << endl;
    #else
        cout << "SYSTEM DOES NOT SUPPORT _POSIX_NAME_MAX" << endl;
    #endif
}

void runTime() {
    cout << "\n\nRUNTIME CONSTANTS\n\n";
    long arg_max = sysconf(_SC_ARG_MAX);
    cout << "Maximum length of arguments to exec is " << arg_max << endl;
    long child_max = sysconf(_SC_CHILD_MAX);
    cout << "Maximum number of child processes is " << child_max << endl;
    long clk_tck = sysconf(_SC_CLK_TCK);
    cout << "Number of clock ticks per second is " << clk_tck << endl;
    long open_max = sysconf(_SC_OPEN_MAX);
    cout << "Maximum number of open files per process is " << open_max << endl;
    long name_max = sysconf(_PC_NAME_MAX);
    cout << "Maximum number of characters in a filename is " << name_max << endl;
    long path_max = pathconf("/", _PC_PATH_MAX);
    cout << "Maximum path length is " << path_max << endl;
}

int main() {
    compileTime();
    runTime();
    return 0;
}
```

**Output**
```bash


MANIFEST CONSTANTS

SYSTEM SUPPORTS CLK_TCK which is 2
Man number of child processes is 25
Maximum path length is 256
Maximum number of open files per process is 20
Maximum number of characters in a filename is 14


RUNTIME CONSTANTS

Maximum length of arguments to exec is 2097152
Maximum number of child processes is 30544
Number of clock ticks per second is 100
Maximum number of open files per process is 1048576
Maximum number of characters in a filename is 65536
Maximum path length is 4096
```


## IOT
### Format
1. Title
2. Objective 
3. Brief Theory
4. Interfacing Block Diagram and manual calculations if any
5. Algorithm
6. Code
7. Output (Printout)
8. Conclusion
9. Course learning outcome
10. References

**Note:** The termworks may be different forr different batches

### TW1
1. **Title**: Interfacing LED's with Arduino - Generating morse code using led's controlled by arduino
2. **Objective:** The objective of this project is to create a pattern generator using LEDs interfaced with an Arduino, where the user inputs an alphanumeric character via serial input, and the corresponding Morse code is displayed using LED
3. **Brief theory**
    LEDs (Light Emitting Diodes) are semiconductor devices that emit light when an electric current passes through them. LEDs are widely used in electronic devices for various purposes due to their efficiency, compact size, and low power consumption. In this project, LEDs are employed to visually represent Morse code sequences. Each dot or dash of the Morse code is translated into a corresponding LED blink pattern, allowing users to observe and interpret the transmitted message. By interfacing LEDs with an Arduino microcontroller, we can automate the process of Morse code generation, making it accessible and versatile for educational, communication, or signaling purposes. This project highlights the synergy between digital electronics, communication systems, and human-computer interaction, showcasing how technology can bridge the gap between different modes of communication.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/9lMny52Fx4W-led-morse-code?sharecode=RRKPmBDFXpidk-w_oGs9z8sG91tTj4J9dfFONOixKPc)
5. **Algorithm:**
    - Receive input character via serial input.
    - Convert the character to Morse code.
    - Output the Morse code using LEDs.
6. **Code:**
    ```cpp
    // Define the size of the dictionary
    const int DICTIONARY_SIZE = 26;

    // Structure to represent a key-value pair
    struct MorsePair {
    char key;          // English alphabet character
    const char* value; // Morse code counterpart
    };

    // Array of key-value pairs representing the Morse code dictionary
    const MorsePair morseDictionary[DICTIONARY_SIZE] = {
    {'A', ".-"}, {'B', "-..."}, {'C', "-.-."}, {'D', "-.."}, {'E', "."}, {'F', "..-."},
    {'G', "--."}, {'H', "...."}, {'I', ".."}, {'J', ".---"}, {'K', "-.-"}, {'L', ".-.."},
    {'M', "--"}, {'N', "-."}, {'O', "---"}, {'P', ".--."}, {'Q', "--.-"}, {'R', ".-."},
    {'S', "..."}, {'T', "-"}, {'U', "..-"}, {'V', "...-"}, {'W', ".--"}, {'X', "-..-"},
    {'Y', "-.--"}, {'Z', "--.."}
    };

    // Define the pin for the LED
    const int LED_PIN = 13;

    void setup() {
    // Initialize Serial communication
    Serial.begin(9600);

    // Set LED pin as an output
    pinMode(LED_PIN, OUTPUT);
    }

    void loop() {
    // Prompt the user to enter a string
    Serial.println("Enter a string (A-Z):");

    // Read the user input
    while (!Serial.available()); // Wait for input
    String input = Serial.readStringUntil('\n'); // Read input until newline character

    // Translate input to Morse code and blink LED accordingly
    translateAndBlink(input);
    }

    // Function to translate a string to Morse code and blink LED
    void translateAndBlink(String input) {
    // Iterate through each character in the input string
    for (int i = 0; i < input.length(); i++) {
        // Convert character to uppercase
        char c = toupper(input.charAt(i));

        // Find Morse code counterpart in the dictionary
        const char* morseCode = findMorseCode(c);

        // Blink LED according to Morse code
        blinkMorseCode(morseCode);
    }
    }

    // Function to find Morse code for a given character
    const char* findMorseCode(char c) {
    for (int i = 0; i < DICTIONARY_SIZE; i++) {
        if (morseDictionary[i].key == c) {
        return morseDictionary[i].value;
        }
    }
    return ""; // Return empty string if character not found
    }

    // Function to blink LED according to Morse code
    void blinkMorseCode(const char* morseCode) {
    for (int i = 0; morseCode[i] != '\0'; i++) {
        if (morseCode[i] == '.') {
        digitalWrite(LED_PIN, HIGH);
        delay(250); // Dot duration
        digitalWrite(LED_PIN, LOW);
        delay(250); // Inter-element gap
        } else if (morseCode[i] == '-') {
        digitalWrite(LED_PIN, HIGH);
        delay(750); // Dash duration
        digitalWrite(LED_PIN, LOW);
        delay(250); // Inter-element gap
        } else if (morseCode[i] == ' ') {
        delay(750); // Inter-character gap
        }
    }
    delay(1250); // Inter-word gap
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1ZJ7CIzWlfuGDxl6ibK-RWAXvuKJzKh404-0vqsSofgQ/edit?usp=drive_link)
8. **Conclusion:** This project successfully demonstrates the interfacing of LEDs with an Arduino to generate Morse code patterns corresponding to user-input alphanumeric characters. It illustrates the practical application of Morse code and LED interfacing in educational or communication systems.
9. **Course learning outcome:** Understanding serial communication with Arduino.
Implementing logic for character-to-Morse code conversion.
Applying digital output to control LEDs.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW2
1. **Title**: Interfacing Arduino with a push button for glowing up the LED
2. **Objective**: The objective of this project is to interface a push button with an Arduino board to control the illumination of an LED. When the push button is pressed, the LED will turn on, and when it is released, the LED will turn off.
3. **Brief theory**
    - Push Button: A push button is a momentary switch that completes an electrical circuit when pressed. It is commonly used in electronic projects to provide user input or trigger actions.
    - LED (Light Emitting Diode): An LED is a semiconductor device that emits light when current flows through it. It is often used in electronic projects for visual indicators or illumination purposes.
    - Arduino: Arduino is an open-source electronics platform based on easy-to-use hardware and software. It consists of a microcontroller board and a development environment for writing and uploading code to the board.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/jnvAr1ZuwJy-push-button-basic?sharecode=bAq576muQKyDizDCJWcTdD9HF5hn9nONR0r8JFUCRkk)
5. **Algorithm:**
    - Initialize the Arduino board and configure the push button and LED pins as inputs and outputs, respectively.
    - Continuously monitor the state of the push button.
    - If the push button is pressed (input HIGH), turn on the LED by setting its pin to HIGH.
    - If the push button is released (input LOW), turn off the LED by setting its pin to LOW.
6. **Code:**
    ```cpp
    // constants won't change. They're used here to set pin numbers:
    const int buttonPin = 12;  // the number of the pushbutton pin
    const int ledPin = 13;    // the number of the LED pin

    // variables will change:
    int buttonState = 0;  // variable for reading the pushbutton status

    void setup() {
    // initialize the LED pin as an output:
    pinMode(ledPin, OUTPUT);
    // initialize the pushbutton pin as an input:
    pinMode(buttonPin, INPUT);
    }

    void loop() {
    // read the state of the pushbutton value:
    buttonState = digitalRead(buttonPin);

    // check if the pushbutton is pressed. If it is, the buttonState is HIGH:
    if (buttonState == HIGH) {
        // turn LED on:
        digitalWrite(ledPin, HIGH);
    } else {
        // turn LED off:
        digitalWrite(ledPin, LOW);
    }
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1dF2PvUYFOZPXXnzVaKNE12ylT1uJX4PeAAjsG9yl0AI/edit?usp=drive_link)
8. **Conclusion:** This project demonstrates the basic concept of interfacing a push button with an Arduino to control an LED. By understanding how to read digital inputs from a push button and control digital outputs to an LED, users can create interactive systems and prototypes for various applications.
9. **Course learning outcome**
    - Understanding of digital input and output operations with Arduino.
    - Implementation of push button interfacing techniques for user input.
    - Practical application of LED control for visual feedback or illumination.
    - Introduction to basic circuit design and prototyping using microcontrollers.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW3
1. **Title**: Interfacing Arduino with a button to simulate a dice roll
2. **Objective**: The objective of this project is to interface a push button with an Arduino to generate and display a random number from 1-6, simulating a dice roll, on a 16x2 LCD display.
3. **Brief theory:** A push button is a momentary switch used to provide user input to microcontroller-based systems. LEDs are used to indicate the result of the simulated dice roll. The Arduino generates random numbers to mimic the rolling of a dice.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/d8LVjEjIsCN-push-button-dice?sharecode=mSXd9vECBXWRtyY0c9PEN3wPcHlT0o6yElkI8aDNCnw)
5. **Algorithm:**
    - Setup the push button and LED connections.
    - Initialize the LCD display.
    - Wait for the push button press.
    - Generate a random number between 1 and 6.
    - Display the number on the LCD.
    - Light up LEDs corresponding to the number rolled.
6. **Code:**
    ```cpp
    // C++ code
    //
    #include <LiquidCrystal_I2C.h>

    // defining constants
    const int buttonPin = 12;
    const int ledPin = 13;

    // global variables
    int buttonState = 0;
    int die;

    // defining lcd object
    LiquidCrystal_I2C lcd_1(32, 16, 2);

    void setup()
    {
    // lcd setup
    lcd_1.init();
    lcd_1.setCursor(0, 0);
    lcd_1.backlight();
    lcd_1.display();
    
    // button setup
    pinMode(buttonPin, INPUT);
    
    // random seed 
    randomSeed(analogRead(0));
    
    // button setup
    pinMode(ledPin, OUTPUT);
    }

    void refreshDisplay(int arg) {
    lcd_1.clear();
    lcd_1.setCursor(0, 0);
    lcd_1.print(arg);
    }

    int rollDice() {
    // Check if the button is pressed
    if (digitalRead(buttonPin) == HIGH) {
        // Generate a random number between 1 and 6 (inclusive)
        int randomNumber = random(1, 7);
        refreshDisplay(randomNumber);
        digitalWrite(ledPin, HIGH);
        delay(1000);
        return randomNumber;
    } else {
        // If button is not pressed, return -1 as an indication
        digitalWrite(ledPin, LOW);
        return -1;
    }
    }

    void loop()
    {
    // only for debugging
    die = rollDice();
    Serial.println(die);
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1an_sI5c3DNORjg-2KgW2bp_Qqr3NABo0Yw9quRhTN6g/edit?usp=drive_link)
8. **Conclusion:** This project effectively demonstrates the integration of push buttons, LEDs, and LCD displays with Arduino to create a simulated dice roll. It serves as a practical example for understanding user input, random number generation, and visual feedback in embedded systems.
9. **Course learning outcome**
    - Understanding digital input with Arduino.
    - Implementing random number generation.
    - Interfacing and controlling LED and LCD displays.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019

### TW4
1. **Title**: Interfacing Arduino with SR04 Ultrasonic Sensor for Distance Measurement and buzzer for alert
2. **Objective**: The objective of this project is to create a simulated parking sensor system by interfacing an SR04 ultrasonic sensor with a buzzer. The system aims to detect obstacles in a parking space and provide audible feedback to the user through the buzzer, mimicking the behavior of a real parking sensor.
3. **Brief theory**
    - SR04 Sensor: The SR04 is an ultrasonic distance sensor that measures distance by emitting ultrasonic waves and calculating the time it takes for the waves to bounce back after hitting an obstacle. It consists of a transmitter, receiver, and control circuit.
    - Buzzer: A buzzer is an electromechanical device that produces sound when an electric current is passed through it. It is commonly used in electronic projects to provide audible alerts or feedback to users.
    - Parking Sensor: In real-world applications, parking sensors use ultrasonic sensors to detect nearby obstacles when parking a vehicle. They provide feedback to the driver through visual or audible signals to assist in parking maneuvers.
4. **Interfacing block diagram:** [Check tinkercad](https://www.tinkercad.com/things/h4zhyniMwh8-copy-of-ultrasonic-distance-sensor-with-buzzer?sharecode=g99HqYIqaZYtFaHEj4ZybbZIXg2_4tryGFaNdn7FFx8)
5. **Algorithm**
    - Initialize the Arduino board and configure the SR04 sensor and buzzer pins.
    - Continuously trigger the SR04 sensor to send ultrasonic waves and measure the time it takes for the waves to bounce back.
    - Calculate the distance to the nearest obstacle based on the time-of-flight of the ultrasonic waves.
    - If an obstacle is detected within a certain threshold distance, activate the buzzer to emit an audible alert.
    - Adjust the frequency or intensity of the buzzer based on the proximity of the obstacle to simulate different warning levels.
6. **Code**
    ```cpp
    const int triggerPin = 6;  // Trigger pin of the ultrasonic sensor
    const int echoPin = 7;     // Echo pin of the ultrasonic sensor
    const int buzzerPin = 9;   // Buzzer pin

    long duration;
    int distance;

    void setup() {
    pinMode(triggerPin, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(buzzerPin, OUTPUT);
    Serial.begin(9600);  // Initialize serial communication at 9600 bps
    }

    void loop() {
    // Clear the trigger pin
    digitalWrite(triggerPin, LOW);
    delayMicroseconds(2);

    // Set the trigger pin HIGH for 10 microseconds
    digitalWrite(triggerPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(triggerPin, LOW);

    // Read the echo pin, and calculate the distance
    duration = pulseIn(echoPin, HIGH);
    distance = duration * 0.034 / 2;  // Speed of sound wave divided by 2 (go and back)

    Serial.print("Distance: ");
    Serial.println(distance);

    // Set buzzer beeping rate based on distance
    if (distance < 10) {
        tone(buzzerPin, 1000);  // Continuous beep
        delay(100);  // Small delay to avoid overload
        noTone(buzzerPin);
        Serial.println("TRIPLE CAUTION, high frequency!!!");
    } else if (distance < 20) {
        tone(buzzerPin, 1000);
        delay(200);
        noTone(buzzerPin);
        delay(200);
        Serial.println("DOUBLE CAUTION, mid frequency!!!");
    } else if (distance < 30) {
        tone(buzzerPin, 1000);
        delay(400);
        noTone(buzzerPin);
        delay(400);
        Serial.println("CAUTION, low frequency!!!");
    } else if (distance < 50) {
        tone(buzzerPin, 1000);
        delay(800);
        noTone(buzzerPin);
        delay(800);
        Serial.println("Appropriate distace, v low frequency!!!");
    } else {
        noTone(buzzerPin);  // No beep
    }

    delay(1000);  // Delay between readings
    }
    ```
7. **Output:** [Check here](https://docs.google.com/document/d/1CaE9CIDSQp94Wd2X4D6-2GYObaCcoGroknS6wvDIBjM/edit?usp=drive_link)
8. **Conclusion:** This project demonstrates the implementation of a simulated parking sensor system using an SR04 ultrasonic sensor and a buzzer. By interfacing these components with an Arduino board and analyzing sensor data, the system can provide audible feedback to users when obstacles are detected, aiding in parking maneuvers. While this simulation does not replace the functionality of real parking sensors, it serves as an educational and prototyping tool for understanding sensor interfacing and feedback mechanisms.
9. **Course learning outcomes:**
    - Understanding of ultrasonic sensor operation and distance measurement.
    - Implementation of buzzer control for audible alerts.
    - Application of sensor data analysis for obstacle detection.
    - Integration of sensor feedback systems with microcontroller-based projects.
10. **References**
    1. Arduino Official Website: https://www.arduino.cc/
    2. Tinkercad: https://www.tinkercad.com/users/3yIYe1Hze1e
    3. GitHub: https://github.com/AumPauskar/micro-iot-projects/
    4. Arshdeep Bagha, Vijay Madishetti, Internet of Things A Hands- on Approach, Universities Press, 2014
    5. Sudip Misra, Anandarup Mukherjee, Arijit Roy, Introduction to IoT, Cambridge University Press, 2021
    6. Mayur Ramgir, Internet of Things- Architecture, Implementation, and Security, Pearson Education India, 2019