#include "SIM900.h" //Includes library files from SIM900
#include <SoftwareSerial.h> //Includes library files from SoftwareSerial
#include "call.h" //Includes library files from call

#define ACTIVE LOW  

const int ledPin =  13;      // the number of the LED pin

CallGSM call;             
boolean started=false;
int buttonState = 31;    
const int buttonPin = 32;     // the number of the pushbutton pin
boolean calling = false;

void setup() //Setting up the pins for output and input
{
  
  Serial.begin(9600);
    pinMode(ledPin,OUTPUT);
    pinMode(buttonPin, INPUT);
    digitalWrite(buttonPin,HIGH);
    if (gsm.begin(9600)) 
    {
        Serial.println("\nstatus=READY");
        started=true;   
    } 
    else 
        Serial.println("\nstatus=IDLE");
}

void loop()
{
buttonState = digitalRead(buttonPin);
if (buttonState == ACTIVE) {
     if(calling)
     {
      digitalWrite(ledPin,LOW);
      calling = false;
      call.HangUp();
      delay(1000);
      }else
     {
      calling = true;
      digitalWrite(ledPin, HIGH);
      delay(1000);
      call.Call("+919876543210"); //Insert number of medical staff here 
}
