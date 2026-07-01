# Arduino Assignment 2 — Beeping Countdown
This is my submission for Assignment 2 in the Programming C++ for
Engineers Using Arduino course at [GHANA COMMUNICATION TECHNOLOGY UNIVERSITY].

## What this project does
A 7-segment display counts down from 9 to 0. On each step, a passive buzzer plays a short beep. When the countdown reaches 0, the buzzer plays a longer tone to signal completion.

## Hardware used
 Arduino Uno
 1 x passive buzzer (piezo)
 1 x single-digit 7-segment display (common cathode)
 1 x 220 ohm resistor (on the COM pin)
 Breadboard and jumper wires
 
## Concepts demonstrated
 - The tone() and noTone() functions
 -  Passive vs active buzzers
 -   7-segment display wiring (common cathode)
 - 2D arrays for digit patterns (lookup table)
 -  Functions with parameters
 -   while and for loops
 -    Serial Monitor output
 
## How to run it
 
1. Wire the buzzer to pin 8.
2. Wire the 7-segment segments a-g to Arduino pins 2, 3, 4, 5, 6, 7, 9
   (direct wires, no resistors).
3. Connect the COM pin of the display to GND via a 220 ohm resistor.
4. Open the .ino file in the Arduino IDE.
5. Select Tools > Board > Arduino Uno and the correct Port.
6. Click Upload.


 ##Code

byte digits[10][7] = {
  {1, 1, 1, 1, 1, 1, 0}, // 0 
  {0, 1, 1, 0, 0, 0, 0}, // 1
  {1, 1, 0, 1, 1, 0, 1}, // 2
  {1, 1, 1, 1, 0, 0, 1}, // 3
  {0, 1, 1, 0, 0, 1, 1}, // 4
  {1, 0, 1, 1, 0, 1, 1}, // 5
  {1, 0, 1, 1, 1, 1, 1}, // 6
  {1, 1, 1, 0, 0, 0, 0}, // 7
  {1, 1, 1, 1, 1, 1, 1}, // 8
  {1, 1, 1, 1, 0, 1, 1}, // 9
};


int segmentPins[7] = {2, 3, 4, 5, 6, 7, 9}; // 
int numSegments = 7;
int buzzerPin = 8; 


void showDigit(int n) {
  if (n < 0 || n > 9) return; 

  for (int i = 0; i < numSegments; i++) {
    digitalWrite(segmentPins[i], digits[n][i]);
  }
}

void setup() {
  Serial.begin(9600);

  
  for (int i = 0; i < numSegments; i++) {
    pinMode(segmentPins[i], OUTPUT);
  }

  pinMode(buzzerPin, OUTPUT); 

  Serial.println("=== Countdown Start ===");
  
  int count = 9; 
  while (count >=1 ) {
    Serial.print("Counting: ");
    Serial.println(count);

    showDigit(count); 
    tone(buzzerPin, 1000, 200); 
    delay(1000); 
    count = count - 1; 
  }

  // End sequence
  showDigit(0); 
  tone(buzzerPin, 1500, 800); 
  Serial.println("=== Countdown Complete ===");
}

void loop() {
  
}
 
## Author
 
[TETTEH-NOMO SABINA EDUDZI] - [2526401768]
