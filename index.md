# Gesture Controlled Robot
The Gesture Controlled Robot is a robot that is controlled by a wearable controller using Bluetooth. Like the name suggests, an accelerometer on the wearable device is able to detect a user's hand gestures, allowing the user to control the car without even touching it! I had a great time working on this project-- it was all solderless and powered by Arduino. 

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Emilie H. | Singapore American School | Mechanical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/3dx1bezu284?si=NYBzxIwMh6Jx-Lbv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

(insert technical description)

*Materials Used*: Arduino Micro, Arduino IDE, Resistors, Jumper Wires, Velcro, Breadboard, HC05 Bluetooth Tranceiver Module, MPU-6050 6-Axis Accelerometer

*Greatest Challenge*: As I had little to no experience with electrical engineering or Arduino experience prior to this project, pairing the Bluetooth modules together seemed to be a daunting task. It involved configuring and wiring the HC05 into place by using Arduino IDE's serial monitor. My knowledge on I2C protocol was fuzzy, I had to learn which each "AT+" command meant in the serial monitor, and I began to question if any of my wires were correctly placed in the first place. This took me about three to four hours of learning, testing, and failing. Nevertheless, when I finally power cycled my Arduinos and they began to blink synchronously (meaning the modules are paired), my heart was ever so slightly relieved. Since I had finished, I could finally work on making my product wearable. 

*Highlight*: Coming up with the design for the controller was the most exciting part. As an aspiring mechanical engineer with a passion for design, I wondered how I could keep the controller minimalistic (as much I could with my resources) and comfortable. For this, I used a smaller breadboard, a piece of foam, and velcro strips. I hot glued the velcro onto the foam, stuck the breadboard's adhesive on top of the foam, putting everything together. This allows the controller to be wearable, comfortable, and also adjustable. 

*Next Steps*: 



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
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Final Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino UNO R3 | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Digital Multimeter | What the item is used for | $Price | <a href="https://www.amazon.com/AstroAI-Digital-Multimeter-Voltage-Tester/dp/B01ISAMUA6/ref=sxin_17_pa_sp_search_thematic_sspa?content-id=amzn1.sym.e8da13fc-7baf-46c3-926a-e7e8f63a520b%3Aamzn1.sym.e8da13fc-7baf-46c3-926a-e7e8f63a520b&cv_ct_cx=digital+multimeter&dib=eyJ2IjoiMSJ9.5LQumrfBR8l0mKnJCJlRg73dxpou0gqYD_ffU3srgs0Utegwth8GcQCSVXVzeZeLSJx5J3itz5TLdmJHsrVITQ.-00jRPoT-bBy26YC4LzQ-S4cYdztgmSMGb83_WEm6HY&dib_tag=se&keywords=digital+multimeter&pd_rd_i=B01ISAMUA6&pd_rd_r=e1ff2570-7e4a-4906-bc55-6f819d48d1bc&pd_rd_w=h7HgL&pd_rd_wg=0ZcFH&pf_rd_p=e8da13fc-7baf-46c3-926a-e7e8f63a520b&pf_rd_r=R6YKX3NXTDQ1PQP4H8RM&qid=1715911879&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sr=1-1-7efdef4d-9875-47e1-927f-8c2c1c47ed49-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9zZWFyY2hfdGhlbWF0aWM&psc=1"> Link </a> |
| Sticky Double-Sided Adhesive | What the item is used for | $Price | <a href="https://www.amazon.com/Art3d-Sticky-Double-Sided-Command-Adhesive/dp/B0B58FGF8H/ref=sr_1_1_sspa?crid=2N0JOMEZLJ2DS&dib=eyJ2IjoiMSJ9.qGUGB_MXfmbL0MW7bqNJbxvZC9pzliDJ9KYyRNNrctnh03kCcUXONRrcPYdGeo7Jwzrm83HyF8Jsb1RkcdlLPAw-8RkxbTCMiW6UI1Fpnjv9GjXUg9VBOLxmLVUbmMp5J7gFXKKLTWQ-w_L4Q9rykEUqKmjv-v6GRykMMZLY2cVt__lLxMIlwr6qBnQLWpHiklifUJwjiURxO--TTt2VReYgmN0z7118ifSucrkvRrg.mwA0L4zMSlJP2RO8IBba7dVqwa1Lkr8KvY1JmeQEfCg&dib_tag=se&keywords=velcro+tape+pieces&qid=1716734034&sprefix=velcro+tape+piece%2Caps%2C89&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1"> Link </a> |
| 9V Batteries | What the item is used for | $Price | <a href="https://www.amazon.com/PILOCEL-6LR61-Long-Lasting-Valentines-Leak-Proof/dp/B0BJ26CHZB/ref=sr_1_3_sspa?crid=3511SX6MYKKBL&dib=eyJ2IjoiMSJ9.Z-4XNUoLU7xDvPhZtJr843dKP65QhCM0ndq0Foy"> Link </a> |
| Solderless Breadboard Power Supply Module | What the item is used for | $Price | <a href="https://www.amazon.com/ALAMSCN-Solderless-Breadboard-Battery-Arduino/dp/B08JYPMCZY/ref=sxts_b2b_sx_reorder_acb_business?content-id=amzn1.sym.f63a3b0b-3a29-4a8e-8430-073528fe007f%3Aamzn1.&th=1"> Link </a> |


