#include <SoftwareSerial.h>
#include <LiquidCrystal.h>
#include <dht.h>
#include <Servo.h> 

Servo myservo;


int u=30;
float td;
float x=101.155*pow(2.71,6);
float ea;
float ems;
float C;
float B;
float tg;
float dp_dep;
float s;
float tnw;
float WBGTi;
float WBGTo;

SoftwareSerial mySerial(7, 8);
dht DHT;








//************************************************
int sensitivity=20;   //gas sensitivity

int timeout1=10;

int timeout2=15;

//************************************************






#define DHT11_PIN 18

int gasvalue1=0;
int gasvalue2=0;
int gasvalue3=0;

int set1=1023;;
int set2=1023;
int set3=1023;

int count1=timeout2;
int count2=timeout2;
int count3=timeout2;

int buzzer=9;

int relay1=10;
int relay2=11;
int relay3=12;


LiquidCrystal lcd(2,3,4,5,6,17);
void setup()
{

  
  Serial.begin(9600);
  mySerial.begin(9600);

  myservo.attach(19);
  myservo.write(30); //WINDOW CLOSE
 lcd.begin(16,2);  
 lcd.setCursor(0,0);
 pinMode(9,OUTPUT);
  pinMode(10,OUTPUT);
   pinMode(11,OUTPUT);
    pinMode(12,OUTPUT);

 digitalWrite(relay1,LOW);
  digitalWrite(relay2,LOW);
   digitalWrite(relay3,LOW);


    
   lcd.print("*****Welcome****");
    lcd.setCursor(0,1);
   lcd.print("Calibrating.....");
 
 delay(3000);

 
}
 void loop(){
  DHT.read11(DHT11_PIN);

lcd.clear();


 lcd.setCursor(0,0);
   lcd.print("T:");
 lcd.print(DHT.temperature,0);
  lcd.print((char)223);
   lcd.print("C");
   lcd.print(" H:");
 lcd.print(DHT.humidity,0);
    lcd.print("%");

float ta=DHT.temperature;
float RH=DHT.humidity;

td=(ta-(100-RH)/5);

ea=exp((17.67*(td-ta))/(td+243.5))*8.3*exp((17.502*ta)/(240.97+ta));
ems= 0.575*pow(ea,(1/7));
C=((0.315*(pow(u,0.58)))/5.3865e-8);
B = x+ems*pow((ta),4);
tg=(B+C*ta+7680000)/(C+256000);


td=ta-((100-RH)/5);
dp_dep = ta-td;
s=(dp_dep)/1.2;
tnw=ta-s;

WBGTi=0.7*tnw+0.3*tg;
WBGTo = 0.7*tnw+0.2*tg+0.1*ta;

//Serial.print("WBGT Indoor: ");

Serial.print(DHT.temperature);
Serial.print(",");
Serial.print(DHT.humidity);
Serial.print(",");
Serial.println(WBGTi);

//Serial.print("    WBGT Outdoor: ");
//Serial.println(WBGTo);


 lcd.setCursor(0,1);
   lcd.print("WBGTi: ");
   lcd.print(WBGTi);


//******************************************************

if(WBGTi<27.7){
   myservo.write(30); //WINDOW CLOSE
  
}
else if(WBGTi>27.8 && WBGTi <31){
   myservo.write(100); //WINDOW 50%
}

else if(WBGTi>31.5){
   myservo.write(160); //WINDOW FULL OPEN
}

//********************************************************



if(analogRead(A0)<set1){
  set1=analogRead(A0);
}


if(analogRead(A1)<set2){
  set2=analogRead(A1);
}

if(analogRead(A2)<set3){
  set3=analogRead(A2);
}




   

gasvalue1=analogRead(A0);
gasvalue2=analogRead(A1);
gasvalue3=analogRead(A2);



if(gasvalue1>set1+sensitivity){
   lcd.setCursor(0,1);
   lcd.print("Level 1 Smoke   ");
   level1();
}

if(gasvalue2>set2+sensitivity){
   lcd.setCursor(0,1);
   lcd.print("Level 2 Smoke   ");
    level2();
}

if(gasvalue3>set3+sensitivity){
   lcd.setCursor(0,1);
   lcd.print("Level 3 Smoke   ");
     level3();

   
}




 

 delay(5000);
}

void level1(){
  count1=timeout1;

  digitalWrite(buzzer,HIGH);

while(1){
lcd.clear();

 lcd.setCursor(0,0);
   lcd.print("Level 1 Alarm!!!");

    lcd.setCursor(0,1);
   lcd.print("Cancel?");

   

   lcd.print(count1);


count1=count1-1;
delay(1000);
  digitalWrite(buzzer,LOW);

if (count1==0) level1p2();
  
}

}

void level1p2(){

//cut off relay 1
 digitalWrite(relay1,HIGH);
count1=timeout2;
  digitalWrite(buzzer,HIGH);
while(1){


lcd.clear();

 lcd.setCursor(0,0);
   lcd.print("Level 1 Power off");


   

    lcd.setCursor(0,1);
   lcd.print("Cancel?");

   

   lcd.print(count1);

count1=count1-1;
delay(1000);
  digitalWrite(buzzer,LOW);
if (count1==0) phase3();

  
}


//-------------------------------------------------------------


  
}


void level2(){
  count2=timeout1;

  digitalWrite(buzzer,HIGH);

while(1){
lcd.clear();

 lcd.setCursor(0,0);
   lcd.print("Level 2 Alarm!!!");

    lcd.setCursor(0,1);
   lcd.print("Cancel?");

   

   lcd.print(count2);


count2=count2-1;
delay(1000);
  digitalWrite(buzzer,LOW);

if (count2==0) level2p2();
  
}

}

void level2p2(){

//cut off relay 1
 digitalWrite(relay2,HIGH);
count2=timeout2;
  digitalWrite(buzzer,HIGH);
while(1){


lcd.clear();

 lcd.setCursor(0,0);
   lcd.print("Level 2 Power off");


   

    lcd.setCursor(0,1);
   lcd.print("Cancel?");

   

   lcd.print(count2);

count2=count2-1;
delay(1000);
  digitalWrite(buzzer,LOW);
if (count2==0) phase3();

  
}





  
}

//----------------------------------------------------


void level3(){
  count3=timeout1;

  digitalWrite(buzzer,HIGH);

while(1){
lcd.clear();

 lcd.setCursor(0,0);
   lcd.print("Level 3 Alarm!!!");

    lcd.setCursor(0,1);
   lcd.print("Cancel?");

   

   lcd.print(count3);


count3=count3-1;
delay(1000);
  digitalWrite(buzzer,LOW);

if (count3==0) level3p2();
  
}

}

void level3p2(){

//cut off relay 1
 digitalWrite(relay3,HIGH);
count3=timeout2;
  digitalWrite(buzzer,HIGH);
while(1){


lcd.clear();

 lcd.setCursor(0,0);
   lcd.print("Level 3 Power off");


   

    lcd.setCursor(0,1);
   lcd.print("Cancel?");

   

   lcd.print(count3);

count3=count3-1;
delay(1000);
  digitalWrite(buzzer,LOW);
if (count3==0) phase3();

  
}





  
}





void phase3(){

//full power off


   if(count1==0){
sms();
   }

   if(count2==0){
sms1();
   }

   if(count3==0){
sms2();
   }
   

while(1){
   digitalWrite(relay1,HIGH);
  digitalWrite(relay2,HIGH);
   digitalWrite(relay3,HIGH);
lcd.clear();

 lcd.setCursor(0,0);
   lcd.print("Full Power off  ");

//trail activated


//sms sent
 digitalWrite(buzzer,HIGH);
   delay(200);

}
  
}

void sms(){

mySerial.print("\r");
delay(1000);                    //Wait for a second while the modem sends an "OK"
mySerial.print("AT+CMGF=1\r");    //Because we want to send the SMS in text mode
delay(1000);

mySerial.print("AT+CMGS=\"+8801627143179\"\r");    //Start accepting the text for the message
//to be sent to the number specified.
//Replace this number with the target mobile number.
delay(1000);
mySerial.print("Fire Detection Alert, Building No 1, Floor 1");   //The text for the message
delay(1000);
mySerial.write(0x1A);  //Equivalent to sending Ctrl+Z 
  
}

void sms1(){

mySerial.print("\r");
delay(1000);                    //Wait for a second while the modem sends an "OK"
mySerial.print("AT+CMGF=1\r");    //Because we want to send the SMS in text mode
delay(1000);

mySerial.print("AT+CMGS=\"+8801627143179\"\r");    //Start accepting the text for the message
//to be sent to the number specified.
//Replace this number with the target mobile number.
delay(1000);
mySerial.print("Fire Detection Alert, Building No 1, Floor 2");   //The text for the message
delay(1000);
mySerial.write(0x1A);  //Equivalent to sending Ctrl+Z 
  
}

void sms2(){

mySerial.print("\r");
delay(1000);                    //Wait for a second while the modem sends an "OK"
mySerial.print("AT+CMGF=1\r");    //Because we want to send the SMS in text mode
delay(1000);

mySerial.print("AT+CMGS=\"+8801627143179\"\r");    //Start accepting the text for the message
//to be sent to the number specified.
//Replace this number with the target mobile number.
delay(1000);
mySerial.print("Fire Detection Alert, Building No 1, Floor 3");   //The text for the message
delay(1000);
mySerial.write(0x1A);  //Equivalent to sending Ctrl+Z 
  
}

