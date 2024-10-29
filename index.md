# Gesture Controlled Robot
The Gesture Controlled Robot is a robot that is controlled by a wearable controller using Bluetooth. Like the name suggests, an accelerometer on the wearable device is able to detect a user's hand gestures, allowing the user to control the car without even touching it! I had a great time working on this project-- it was all solderless and powered by Arduino. 

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Emilie H. | Singapore American School | Mechanical Engineering | Incoming Senior

# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/3dx1bezu284?si=NYBzxIwMh6Jx-Lbv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

*Materials Used*: Arduino Micro, Arduino IDE, Resistors, Jumper Wires, Velcro, Breadboard, HC05 Bluetooth Tranceiver Module, MPU-6050 6-Axis Accelerometer

*Greatest Challenge*: As I had little to no experience with electrical engineering or Arduino experience prior to this project, pairing the Bluetooth modules together seemed to be a daunting task. It involved configuring and wiring the HC05 into place by using Arduino IDE's serial monitor. My knowledge on I2C protocol was fuzzy, I had to learn which each "AT+" command meant in the serial monitor, and I began to question if any of my wires were correctly placed in the first place. This took me about three to four hours of learning, testing, and failing. Nevertheless, when I finally power cycled my Arduinos and they began to blink synchronously (meaning the modules are paired), my heart was ever so slightly relieved. Since I had finished, I could finally work on making my product wearable. 

*Highlight*: Coming up with the design for the controller was the most exciting part. As an aspiring mechanical engineer with a passion for design, I wondered how I could keep the controller minimalistic (as much I could with my resources) and comfortable. For this, I used a smaller breadboard, a piece of foam, and velcro strips. I hot glued the velcro onto the foam, stuck the breadboard's adhesive on top of the foam, putting everything together. This allows the controller to be wearable, comfortable, and also adjustable. 

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/mYbODG_Db3c?si=K6KnaWJDQS4g5GX7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my first milestone, I assembled the Chassi Car (the robot I will be controlling later on), wired the electronics that make it move, and completed some Arduino test code to configure the pins for future use. As a result, the robot moves! Through my code and assembly, I was able to get it moving forward and backward. This experience was extremely new to me as I've never worked with electronics OR Arduino independently, but I've already learned so much in the span of a week. 

*Key materials used:* Arduino UNO, Chassi Car, Screwdriver, Wire Kit, Breadboard, H-Bridges

*Challenges*: It was difficult to get my test code working as I didn't configure my pins effectively, resulting in one of my wheels moving in the wrong direction with every method call. Some debugging fixed the problem though, and it was interesting to see how hardware and software interact!

*Next steps:* For my second milestone, I hope to assemble the controller powered by gestures and write its code. If I complete this in time, I hope to make a modification and also make my car look more aesthetically pleasing through concealing the wiring. 

**Test Code for Milestone 1**
```c++

// this is for h-bridge 1
const int AIA_1 = 4;
const int AIB_1 = 5; 
const int BIA_1 = 2;
const int BIB_1 = 3;

// this is for h-bridge 2
const int AIA_2 = 9;
const int AIB_2 = 8;
const int BIA_2 = 11;
const int BIB_2 = 10;

void setup() {
  // put your setup code here, to run once:
  pinMode(AIA_1, OUTPUT);
  pinMode(AIB_1, OUTPUT);

  pinMode(BIA_1, OUTPUT);
  pinMode(BIB_1, OUTPUT);

  pinMode(AIA_2, OUTPUT);
  pinMode(AIB_2, OUTPUT);

  pinMode(BIA_2, OUTPUT);
  pinMode(BIB_2, OUTPUT);
  
}

void loop() {
  // put your main code here, to run repeatedly:
  forward();
 delay(2000);
 backward();
 delay(2000);
}

void backward()
{
  digitalWrite(AIA_1, HIGH);
  digitalWrite(AIA_2, LOW);

  digitalWrite(AIB_1, LOW);
  digitalWrite(AIB_2, HIGH);

  digitalWrite(BIA_1, LOW);
  digitalWrite(BIA_2, LOW);

  digitalWrite(BIB_1, HIGH);
  digitalWrite(BIB_2, HIGH);
}
void forward()
{

  digitalWrite(AIA_1, LOW);
  digitalWrite(AIA_2, HIGH);

  digitalWrite(AIB_1, HIGH);
  digitalWrite(AIB_2, LOW);

  digitalWrite(BIA_1, HIGH);
  digitalWrite(BIA_2, HIGH);

  digitalWrite(BIB_1, LOW);
  digitalWrite(BIB_2, LOW);

}


```


# Schematics 
Schematics are available via the GitHub page.

# Final Code
* Car Code
```c++
///Code for the car
// This is to receive data from the other Bluetooth module and read the gestures
// The robot should move accordingly! 

//watch out for AIA2 and AIB2

#include <SoftwareSerial.h>

#define tx 2
#define rx 3

SoftwareSerial configBt(rx, tx);

//character variable for command
char c = "";

//change based on motor pins
const int AIA_1 = 9;
const int AIB_1 = 8;
const int BIA_1 = 11;
const int BIB_1 = 10;

const int AIA_2 = 7;
const int AIB_2 = 4; 
const int BIA_2 = 6;
const int BIB_2 = 5;

void setup()
{
  //opens serial monitor and Bluetooth serial monitor
  Serial.begin(38400);
  configBt.begin(38400);
  pinMode(tx, OUTPUT);
  pinMode(rx, INPUT);

  //initializes all motor pins as outputs
  pinMode(AIA_1, OUTPUT);
  pinMode(AIB_1, OUTPUT);
  pinMode(BIB_1, OUTPUT);
  pinMode(BIA_1, OUTPUT);
  pinMode(AIA_2, OUTPUT);
  pinMode(AIB_2, OUTPUT);
  pinMode(BIB_2, OUTPUT);
  pinMode(BIA_2, OUTPUT);
  
}

void loop()
{
  //checks for Bluetooth data
  if (configBt.available()){
    //if available stores to command character
    c = (char)configBt.read();
    //prints to serial
    Serial.println(c);
  }

  //acts based on character
  switch(c){
    
    //forward case
    case 'F':
      forward();
      break;
      
    //left case
    case 'L':
      left();
      break;
      
    //right case
    case 'R':
      right();
      break;
      
    //back case
    case 'B':
      back();
      break;
      
    //default is to stop robot
    case 'S':
      freeze();
    }
}

//moves robot forward 
void forward(){
  
    //chages directions of motors
    digitalWrite(AIA_1, LOW);
  digitalWrite(AIA_2, HIGH);

  digitalWrite(AIB_1, HIGH);
  digitalWrite(AIB_2, LOW);

  digitalWrite(BIA_1, LOW);
  digitalWrite(BIA_2, LOW);

  digitalWrite(BIB_1, HIGH);
  digitalWrite(BIB_2, HIGH);

  }

//moves robot left
void left(){

    //changes directions of motors
    // im guessing input b is high and input a is low
 digitalWrite(AIA_1, HIGH); //ccw
  digitalWrite(AIA_2, HIGH); // clockwise

  digitalWrite(AIB_1, LOW); //ccw
  digitalWrite(AIB_2, LOW); //clockwise

  digitalWrite(BIA_1, LOW); //clockwise
  digitalWrite(BIA_2, HIGH);

  digitalWrite(BIB_1, HIGH); //clockwise
  digitalWrite(BIB_2, LOW);

  }

//moves robot right
void right(){

    //changes directions of motors
    // im guessing motor a is high and then b is low
    digitalWrite(AIA_1, LOW); // set to clockwise
  digitalWrite(AIA_2, LOW);

  digitalWrite(AIB_1, HIGH); // set to clockwise
  digitalWrite(AIB_2, HIGH);

  digitalWrite(BIA_1, HIGH);
  digitalWrite(BIA_2, LOW); // set to clockwise

  digitalWrite(BIB_1, LOW); 
  digitalWrite(BIB_2, HIGH); // set to clockwise

    /* digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW); */


  }

//moves robot backwards
void back(){

    //changes directions of motors
    digitalWrite(AIA_1, HIGH);
  digitalWrite(AIA_2, LOW);

  digitalWrite(AIB_1, LOW);
  digitalWrite(AIB_2, HIGH);

  digitalWrite(BIA_1, HIGH);
  digitalWrite(BIA_2, HIGH);

  digitalWrite(BIB_1, LOW);
  digitalWrite(BIB_2, LOW);

    

  }

//stops robot
void freeze(){

    //changes directions of motors
    digitalWrite(AIA_1, LOW);
    digitalWrite(AIA_2, LOW);

    digitalWrite(AIB_1, LOW);
    digitalWrite(AIB_2, LOW);

    digitalWrite(BIA_1, LOW);
    digitalWrite(BIA_2, LOW);

    digitalWrite(BIB_1, LOW);
    digitalWrite(BIB_2, LOW);

  }

```
* Controller Code
```c++
#include <Wire.h>

#define MPU6050_ADDRESS 0x68

int16_t accelerometerX, accelerometerY, accelerometerZ;

void setup()
{
  Wire.begin();
  Serial1.begin(38400);

  // Initialize MPU6050
  Wire.beginTransmission(MPU6050_ADDRESS);
  Wire.write(0x6B);  // PWR_MGMT_1 register
  Wire.write(0);     // set to zero (wakes up the MPU6050)
  Wire.endTransmission(true);

  delay(100); // Delay to allow MPU6050 to stabilize
}

void loop()
{
  readAccelerometerData();
  determineGesture();
  delay(700);
}

void readAccelerometerData()
{
  Wire.beginTransmission(MPU6050_ADDRESS);
  Wire.write(0x3B);  // starting with register 0x3B (ACCEL_XOUT_H)
  Wire.endTransmission(false);
  Wire.requestFrom(MPU6050_ADDRESS, 6, true);  // request a total of 6 registers

  // read accelerometer data
  accelerometerX = Wire.read() << 8 | Wire.read();
  accelerometerY = Wire.read() << 8 | Wire.read();
  accelerometerZ = Wire.read() << 8 | Wire.read();
}

void determineGesture()
{
  if (accelerometerY >= 6700) { // should be L
    Serial1.write('R');
    Serial.println('R');
  }
  else if (accelerometerY <= -4200) { // should be R
    Serial1.write('L');
    Serial.println('L');
  }
  else if (accelerometerX <= -3450) { // should be B
    Serial1.write('B');
    Serial.println('B');
  }
  else if (accelerometerX >= 3450) { // should be F
    Serial1.write('F');
    Serial.println('F');
  }
  else {
    Serial1.write('S');
     Serial.println('S');
  }
}
```
* Bluetooth Setup
```c++
//Code for Arduino Uno Bluetooth Connection
#include <SoftwareSerial.h>

#define tx 3
#define rx 2

SoftwareSerial configBt(rx, tx);
long tm, t, d;

void setup() {
  //Put my setup code here, to run once:
  Serial.begin(38400);
  configBt.begin(38400); // Corrected object name to configBt
  pinMode(tx, OUTPUT);
  pinMode(rx, INPUT);
}

void loop() {
  if (configBt.available()) {
    Serial.print((char)configBt.read());
  }
  if (Serial.available()) {
    configBt.write(Serial.read());
  }
}

```
|


