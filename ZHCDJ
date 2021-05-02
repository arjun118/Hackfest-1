#include <Stepper.h>	//Includes the files from the library for Stepper Motor
const int numberOfSteps = 50;	//Setting the number of steps in which the rotation of the motor will take place
Stepper myStepper1(numberOfSteps, 8,9,10,11); //Initializes the stepper motor object- myStepper1 with the pins
Stepper myStepper2(numberOfSteps, 4,5,6,7); //Initializes the stepper motor object- myStepper2 with the pins

int motor1=22; // Pin connected to Motor 1
int motor2=23; // Pin connected to Motor 2
int motor3=24; // Pin connected to Motor 3
int motor4=25; // Pin connected to Motor 4
int spraymotor=30; // Pin connected to Spray Motor

int llir=26; // Pin connected to Outer Left Infrared Sensor
int lir=27; // Pin connected to Inner Left Infrared Sensor
int rir=28; // Pin connected to Inner Right Infrared Sensor
int rrir=29; //Pin connected to Outer Right Infrared Sensor

int LLT=0; // Stores the return from the outer left IR sensor
int LT=0;  // Stores the return from the inner left IR sensor
int RRT=0; // Stores the return from the inner right IR sensor
int RT=0; // Stores the return from the outer right IR sensor

void LEFT (void); // Function definition to turn left
void RIGHT (void); // Function definition to turn right
void STOP (void); // Function definition to stop moving
void START (void); // Function definition to start moving
void TYPE1 (void); //Function definition of TYPE1- Spraying on front wall
void TYPE2 (void); //Function definition of TYPE2- Rotate arm under the bed
void TYPE3 (void); //Function definition of TYPE3- Rotate arm back to original position
void TYPE4 (void); //Function definition of TYPE4- Spraying on parallel right wall
void TYPE5 (void); //Function definition of TYPE1- Spraying on parallel left wall
void SPRAY1 (void); //Function definition to spray in front
void SPRAY2 (void); //Function definition to spray on the parallel side walls

const int TrigPin = 33; // Trigger Pin of Ultrasonic Sensor
const int EchoPin = 12; // Echo Pin of Ultrasonic Sensor

void setup() // Setting up the pins associated with the sensors and motors
{
  //Pin Setup for motors
  pinMode(motor1,OUTPUT);  
  pinMode(motor2,OUTPUT);
  pinMode(motor3,OUTPUT);
  pinMode(motor4,OUTPUT);
  pinMode(spraymotor,OUTPUT);

  //Pin Setup for Infrared Sensors
  pinMode(llir,INPUT);
  pinMode(lir,INPUT);
  pinMode(rrir,INPUT);
  pinMode(rir,INPUT);

  //Initialize the values in order to start movement
  digitalWrite(LLT,HIGH);
  digitalWrite(LT,HIGH);
  digitalWrite(RRT,HIGH);
  digitalWrite(RT,HIGH);
  
  //Initializing the speed of Stepper motors
  myStepper1.setSpeed(30);
  myStepper2.setSpeed(30);
  
  //Initialize the trigger and echo pins
  pinMode(TrigPin, OUTPUT);
  pinMode(EchoPin, INPUT);
   
}

void loop() 
{

   long duration,distance; //Stores the time between input and echo received, distance between the points
   
   	// Start all the motors
	analogWrite(motor1,255); 
	analogWrite(motor2,255);
	analogWrite(motor3,255);
	analogWrite(motor4,255);

while(1)
{
	digitalWrite(TrigPin, LOW); 
	delayMicroseconds(2);
	digitalWrite(TrigPin, HIGH);
	delayMicroseconds(10);
	digitalWrite(TrigPin, LOW);
  
	duration = pulseIn(EchoPin, HIGH); 
	distance = duration*0.034/2;   // Calculation of distance
	delay(100); 
  //Read signals from the sensors	
  LLT=digitalRead(llir); 
  LT=digitalRead(lir);
  RRT=digitalRead(rrir);
  RT=digitalRead(rir);
  if(distance<=10)	// If any obstacle is detected within a range of 10 cm the robot stops moving to prevent collision
  STOP();
  if(LLT==0 && LT==0 && RT==0 && RRT==0) // If no signal is received then stop
  STOP();
  else if(LLT==1 && LT==0 && RT==0 && RRT==0) // TYPE1 pattern
  TYPE1();
  else if(LLT==0 && LT==0 && RT==0 && RRT==1) // TYPE2 pattern
  TYPE2();
  else if(LLT==1 && LT==0 && RT==0 && RRT==1) // TYPE3 pattern
  TYPE3();
  else if(LLT==1 && LT==1 && RT==0 && RRT==0) // TYPE4 pattern
  TYPE4();
  else if(LLT==0 && LT==0 && RT==1 && RRT==1) //TYPE5 pattern
  TYPE5();
  else if(LLT==1 && LT==1 && RT==0 && RRT==1) // To turn right
  RIGHT();
  else if(LLT==1 && LT==0 && RT==1 && RRT==1) // To turn left
  LEFT();
}
}

void TYPE1(void)	//In front of the wall
{	
	STOP();
	SPRAY1();
	START();
}

void TYPE2(void)	//At the head of the bed
{
	STOP();
	myStepper1.step(-numberOfSteps);	//Vertical motor is rotated anti-clockwise
    	delay(500);
    	myStepper2.step(numberOfSteps);		//Horizontal motor is rotated clockwise
    	delay(500);
    	SPRAY2(); 				//Calls Spray2 function	
}
void TYPE3(void)	//At the foot of the bed
{
	STOP();
	myStepper1.step(-numberOfSteps);	//Vertical motor is rotated anti-clockwise
    	delay(500);
    	myStepper2.step(numberOfSteps);		//Horizontal motor is rotated clockwise
    	delay(500);
    	SPRAY2();				 //Calls Spray2 function	
}
void TYPE4(void)	//Parallel wall on the right
{
	myStepper2.step(numberOfSteps);		//Horizontal motor is rotated clockwise
    	delay(500);
    	SPRAY2();				//Calls Spray2 function
}
void TYPE5(void)	//Parallel wall on the left
{
	myStepper2.step(-numberOfSteps);	//Horizontal motor is rotated clockwise
    	delay(500);
    	SPRAY2();	//Calls Spray2 function
}

void SPRAY1(void)
{
	analogWrite(spraymotor,255);	//Spray motor begins in order to start the spraying
	delay(5000);		// Runs for 5 seconds
	analogWrite(spraymotor,0); //Spray motor stops the spraying
}

void SPRAY2(void)
{
	analogWrite(spraymotor,255);	//Spray motor begins in order to start the spraying
	int lPrev=0;
        int rPrev=0;
    	int llPrev=0;
    	int rrPrev=0;
	while((lPrev!=LT || rPrev!=RT) && llPrev!=LLT && rrPrev!=RRT)
	{
		LT=digitalRead(lir);
		RT=digitalRead(rir);
		LLT=digitalRead(llir);
		RRT=digitalRead(rrir);
		START();
	}
	analogWrite(spraymotor,0);   
}

void LEFT(void)
{
   analogWrite(motor3,0);
   analogWrite(motor4,30);   
   while(LT==0)
   {
    LT=digitalRead(lir);
    RT=digitalRead(rir);
    LLT=digitalRead(llir);
    RRT=digitalRead(rrir);
    if(LLT==1 && RT==1 && RRT==1)
    {
      int lPrev=LT;
      int rPrev=RT;
      int llPrev=LLT;
      int rrPrev=RRT;
      STOP();
      while((lPrev==LT)&&(rPrev==RT) && llPrev==LLT && rrPrev==RRT)
      {
         LT=digitalRead(lir);
         RT=digitalRead(rir);
         LLT=digitalRead(llir);
         RRT=digitalRead(rrir);
      }
    }
    analogWrite(motor1,255);
    analogWrite(motor2,0); 
   }
   analogWrite(motor3,255);
   analogWrite(motor4,0);
}

void RIGHT (void)
{
   analogWrite(motor1,0);
   analogWrite(motor2,30);

   while(RT==0)
   {
    LT=digitalRead(lir);
    RT=digitalRead(rir);
    LLT=digitalRead(llir);
    RRT=digitalRead(rrir);
    if(LLT==1 && LT==1 && RRT==1)
    {
      int lPrev=LT;
      int rPrev=RT;
      int llPrev=LLT;
      int rrPrev=RRT;
	  STOP();
      while((lPrev==LT)&&(rPrev==RT) && llPrev==LLT && rrPrev==RRT)
      {
         LT=digitalRead(lir);
         RT=digitalRead(rir);
         LLT=digitalRead(llir);
         RRT=digitalRead(rrir);
         
      }
    }
    analogWrite(motor3,255);
    analogWrite(motor4,0);
    }
   analogWrite(motor1,255);
   analogWrite(motor2,0);
}
void STOP (void) //Stops all the motors
{
analogWrite(motor1,0);
analogWrite(motor2,0);
analogWrite(motor3,0);
analogWrite(motor4,0);
  
}
void START (void) //Starts all the motors
{
analogWrite(motor1,255);
analogWrite(motor2,255);
analogWrite(motor3,255);
analogWrite(motor4,255);
  
}
