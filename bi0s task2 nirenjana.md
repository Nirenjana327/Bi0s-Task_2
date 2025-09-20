# 1\.

![][image1]  
const int nLEDs \= 5;  
int ledPins\[nLEDs\] \= {2,4,15,16,5};   // pins used  
void setup() {  
   
  for (int i \= 0; i \< nLEDs; i\++) {  
    pinMode(ledPins\[i\], OUTPUT); //sets the pin as output so it can control the LED  
// pin \- which digital pin is used    
// mode \- whether input or output   
  }  
}  
void loop() {  
 // to blink led in the order from led left to right  
  for (int i \= 0; i \< nLEDs; i\++) {  
    digitalWrite(ledPins\[i\], HIGH);  //  digitalwrite : It sets the voltage level of a digital output pin(ON/OFF)  
    delay(500);    // waits for 500ms                  
    digitalWrite(ledPins\[i\], LOW);    
    delay(500);  
  }

//to blink led in the order from led right to left

  for (int i \= nLEDs \- 1; i \>= 0; i\--) {  
    digitalWrite(ledPins\[i\], HIGH);    
    delay(500);                        
    digitalWrite(ledPins\[i\], LOW);  
    delay(500);  
  }  
}  
Cathode of led connected to GND(Ground)  
Anode of led connected to GPIO Pins(General Purpose Input/Output pins)

# 2\.

![][image2]// Define the pins for each segment (a to g) and the common cathode pin  
const int segmentPins\[8\] \= {15, 2, 4, 16, 17, 22, 23};  
const int commonCathodePin \= 9;

// Define the numbers to display on the seven-segment display  
const byte numbers\[11\] \= {  
  B00000010, // 0  
  B10011110,// 1  
  B00100100, //2  
  B00001100,//3  
  B10011000, //4  
  B01001000,//5  
  B01000000, //6  
  B00011110, // 7  
  B00000000,// 8  
  B00011000, // 9  
};

void setup() {  
  // Set segment pins as outputs  
  for (int i \= 0; i \< 7; i\++) {  
    pinMode(segmentPins\[i\], OUTPUT);  
  }

  // Set common cathode pin as output  
  pinMode(commonCathodePin, OUTPUT);  
}

void loop() {  
  // Count from 0 to 9  
  for (int i \= 0; i \< 10; i\++)  
  {  
    displayNumber(i);  
   // while(1);  
    delay(1000); // Display each number for 1 second

   // for (int j \= 0; j \< 8; j++) {  
   // digitalWrite(segmentPins\[j\], LOW);  
  //}  
  }  
}

// Function to display a digit on the seven-segment display  
void displayNumber(int num) {  
  // Turn off all segments  
  for (int i \= 0; i \< 8; i\++) {  
    digitalWrite(segmentPins\[i\], HIGH);  
  }

  // Activate segments based on the number to be displayed  
  for (int i \= 0; i \< 8; i\++) {  
    if (bitRead(numbers\[num\], i) \== LOW) {  
      digitalWrite(segmentPins\[7\-i\], LOW);  
    }  
  }

  // Turn on the common cathode to display the digit  
 // digitalWrite(commonCathodePin, LOW);  
}

![][image3]	\\  
Its just a reference  
    

# 

# 3

\#include \<ESP32Servo.h\>

Servo myservo1;  
Servo myservo2;  
int input;  
int HOURS  ;  
int MINUTES  ;

void setup()  
{  
  myservo1.attach(2); // Attach servo1 (minutes hand) to pin 2  
  myservo2.attach(4); // Attach servo2 (hours hand) to pin 4  
  **Serial**.begin(115200); // baud rate  
  **Serial**.println("ENTER HOURS:");  
  **Serial**.println("ENTER MINUTES:");  
}

void loop() {  
  HOURS  \= 0; // Reset HOURS before reading new value

    //`Serial.available()` checks **how many bytes** have arrived at the serial port and are waiting to be read.

    if (**Serial**.available() \> 0) {  
    HOURS \= **Serial**.parseInt(); // Read an integer from Serial as HOURS  
    int anglehrs\=HOURS\*15; // Convert hours into angle  
    myservo2.write(anglehrs) ; // Move hour-hand servo to calculated angle  
    }  
   MINUTES  \= 0 ;  
    if (**Serial**.available() \> 0) {  
    MINUTES\= **Serial**.parseInt();  
    int angleminute \= MINUTES\*3 ;  
    myservo1.write(angleminute);  
  }  
![][image4]![][image5]![][image6]

# 4\.

Referred youtube video  
Referred lcd datasheet

The circuit uses a  battery to power an LCD along with a potentiometer, resistors, DIP switches, and slide switches. The LCD’s VSS pin is connected to ground and VDD to the positive terminal of the battery. A potentiometer is connected across the battery to control the display contrast, with its center pin wired to the contrast input of the LCD.

DIP switches are connected to the LCD’s data pins( b/w DB0–DB7), allowing binary values to be entered manually. One side of the switches is tied to the battery’s positive terminal, while the other side passes through resistors to ground before reaching the LCD. Slide switches are used for control: one connected to the RS (Register Select) pin and another to the Enable pin( push button switch ) , with their side terminals wired to the positive and negative terminals of the battery.

The LCD is operated in 4-bit mode. To display a character, its binary code is divided into two 4-bit parts. For example, the ASCII code for “H” (01001000) is split into 0100 and 1000 With RS initially off,. The lower 4 bits are then entered the same way and latched with another Enable pulse. Once both halves are input, the character appears on the LCD.

Got the values to be entered for initialising and for typing character from the datasheet of lcd  
![][image7]

![][image8]

# 5\.

DDRB controls direction of Port B pins.  
When bit=1 , pin is OUTPUT  
When bit \=0 ,pin , is INPUT  
 DDRB \= 16 means binary 00010000 → PB4 set as OUTPUT.  
PORTB controls output level of Port B pins.  
 Setting PORTB \= 16 (00010000) makes PB4 HIGH (LED ON if connected there)  
Setting PORTB \= 0 makes all Port B pins LOW → LED OFF

Referred bare metal programming guides and also youtube videos


