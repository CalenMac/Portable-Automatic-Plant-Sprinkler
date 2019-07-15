
//Define the moisture sensor pins
const int analogInPin0 = A0;  // 
const int analogInPin1 = A1;
const int analogInPin2 = A2;

//the value readed from each moisture sensor
int moistureValue0 = 0;        //the variable to store the moisture of the sensor1
int moistureValue1 = 0;        //the variable to store the moisture of the sensor1
int moistureValue2 = 0;        //the variable to store the moisture of the sensor1

//the sum of the 30 times sampling
long int moistureSum0 = 0;   //we need to sampling the moisture 30 times and get its average value
long int moistureSum1 = 0;
long int moistureSum2 = 0;


void setup() {
  // initialize serial communications at 9600 bps:
  Serial.begin(9600); 
}

void loop() {
  // read the analog in value:

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
