#include <Servo.h> 

#define triger 250
//Define the parameters of the flower1
#define servoPosition0 20  //the position of the flower1, the range of the servo position is 10~160
#define triggerValue0 135  //the trigger value of the moisture, the minimum value is 0, means the moisture is 0, the soil is very dry. the maximum value is 1024.
#define wateringTime0 35  //the time for watering the flower1, millisecond. delay 35ms, uses about 70ML water

//Define the parameters of the flower2
#define servoPosition1 60  //the position of the flower2
#define triggerValue1 180  //the trigger value of the moisture
#define wateringTime1 20  //the time for watering the flower2,millisecond

//Define the parameters of the flower3
#define servoPosition2 105  //the position of the flower3
#define triggerValue2 200  //the trigger value of the moisture
#define wateringTime2 15  //the time for watering the flower3,millisecond


Servo horizontalServo;  // create servo object to control a servo         
Servo verticalServo;

//Define the moisture sensor pins
const int analogInPin0 = A0;  // 
const int analogInPin1 = A1;
const int analogInPin2 = A2;


//the value readed from each moisture sensor
int moistureValue0 = 0;        
int moistureValue1 = 0;
int moistureValue2 = 0;

//the sum of the 30 times sampling
long int moistureSum0 = 0;   //we need to sampling the moisture 30 times and get its average value, this variable is used to store the sum of the 30 times sampled value
long int moistureSum1 = 0;
long int moistureSum2 = 0;

//Define the water pump contorl pins
const int pumpAnodePin =  6;      //pin 6 connect to the anode of the pump
const int pumpCathodePin =  7;   //pin 7 connect to the cathode of the pump

void setup() 
{ 
  Serial.begin(9600); 
  horizontalServo.attach(8);  // attaches the horizontal servo on pin 8 to the servo object 
  verticalServo.attach(9);  //attaches the vertical servo on pin 9 to the servo object
  initPosition();
  delay(500);
  pinMode(pumpAnodePin, OUTPUT);
  pinMode(pumpCathodePin, OUTPUT);
} 

void initPosition()//Init the position of the servos
{
  verticalServo.write(15); 
  horizontalServo.write(25);  
  delay(1000);
}

void loop() 
{
    
  delay(1000);
  moistureSampling();
 
  if(moistureValue0 < triggerValue0)
  {
    proWatering(servoPosition0, wateringTime0);
    return;
   } 
   if(moistureValue1 < triggerValue1)
  {
    proWatering(servoPosition1, wateringTime1);
    return;
   } 
   if(moistureValue2 < triggerValue2)
  {
    proWatering(servoPosition2, wateringTime2);
    return;
   } 
}

void moistureSampling()// read the value of the soil moisture
{
  for(int i = 0; i < 30; i++)//samping 30 time within 3 seconds
  {
    moistureSum0 = moistureSum0 + analogRead(analogInPin0);  
    moistureSum1 = moistureSum1 + analogRead(analogInPin1);
    moistureSum2 = moistureSum2 + analogRead(analogInPin2);
    delay(100);
  }
  moistureValue0 = moistureSum0 / 30;//get the average value
  moistureValue1 = moistureSum1 / 30;
  moistureValue2 = moistureSum2 / 30;

  // print the results to the serial monitor:
  Serial.print("Moisture0 = " );                       
  Serial.print(moistureValue0);      
  Serial.print("\t Moisture1 = ");      
  Serial.print(moistureValue1); 
  Serial.print("\t Moisture2 = ");  
  Serial.println(moistureValue2); 
  Serial.println(); 
  
  moistureSum0 = 0;//reset the variable
  moistureSum1 = 0;
  moistureSum2 = 0;
  delay(4000);     //delay 4 seconds 
}


void proWatering(int servoPosition, int wateringTime)  //sweep watering 
{
  horizontalServo.write(servoPosition - 10);  // setting the servo to the position of the flower
  delay(500); //waiting the servo go to right position
  digitalWrite(pumpAnodePin, HIGH);  //the pump start working
  digitalWrite(pumpCathodePin, LOW);
  
  for(int pos1 = 15; pos1 < 33; pos1 +=6)//
  {
    verticalServo.write(pos1); 
    for(pos = servoPosition - 10; pos <= servoPosition + 10; pos += 1)  // goes from 0 degrees to 180 degrees //25,160
    {                                  // in steps of 1 degree 
      horizontalServo.write(pos);              // tell servo to go to position in variable 'pos'  
      delay(wateringTime);                       // waits for the servo to reach the position
    } 

    verticalServo.write(pos1+3);
    for(pos = servoPosition + 10; pos>= servoPosition - 10; pos-=1)     // goes from 180 degrees to 0 degrees 
    {                                
      horizontalServo.write(pos);              // tell servo to go to position in variable 'pos' 
      delay(wateringTime);                       // waits for the servo to reach the position 
    } 
  }
  
  for(int pos1 = 33; pos1 > 15; pos1 -= 6)//
  {
    verticalServo.write(pos1); 
    for(pos = servoPosition - 10; pos <= servoPosition + 10; pos += 1)  // goes from 0 degrees to 180 degrees //25,160
    {                                  // in steps of 1 degree 
      horizontalServo.write(pos);              // tell servo to go to position in variable 'pos'  
      delay(wateringTime);                       // waits 15ms for the servo to reach the position 
    } 

     verticalServo.write(pos1-3);
    for(pos = servoPosition + 10; pos >= servoPosition -10; pos-=1)     // goes from 180 degrees to 0 degrees 
    {                                
      horizontalServo.write(pos);              // tell servo to go to position in variable 'pos' 
      delay(wateringTime);                       // waits 15ms for the servo to reach the position 
    } 
  }
  digitalWrite(pumpAnodePin, LOW);
  digitalWrite(pumpCathodePin, LOW);
  delay(500);
  initPosition();
}

void watering(int servoPosition, int wateringTime)
{
  Serial.println(servoPosition);
  horizontalServo.write(servoPosition);
  delay(1000);
 digitalWrite(pumpAnodePin, HIGH);
  delay(10000);
  digitalWrite(pumpAnodePin, LOW);
  delay(3000);
}


/*(void basicWatering(int servoPosition, int wateringTime) //watering in one point
{
  Serial.println(servoPosition);
  horizontalServo.write(servoPosition);
  delay(800);
 digitalWrite(pumpAnodePin, HIGH);
  delay(wateringTime);
  digitalWrite(pumpAnodePin, LOW);
  delay(500);
  initPosition();
}
