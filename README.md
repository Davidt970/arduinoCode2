# arduinoCode2
int shockSensorPin  = 2; //interruptpin 0
boolean sleeping;
int loopcounter = 0;
long starttimer = 0;
long betweenTime= 1000; // 1 second set to change(1000= 1 sec).
long awake = 0;


void setup() {
  // put your setup code here, to run once:
Serial.begin(9600);
pinMode(shockSensorPin, INPUT);
attachInterrupt(0,shakeInterrupt, FALLING);
}

void loop() {
  // put your main code here, to run repeatedly:
if(sleeping){   // if sleeping is true
  loopcounter++;
  if(loopcounter == 30000){
  Serial.println("No Motion");
  loopcounter = 0;
  }

  
 }else if(sleeping == false){
    loopcounter++;
   if(loopcounter == 30000){
    Serial.println("Motion Detected");
    loopcounter = 0;
    }
    awake = millis() - starttimer;
    if(awake > betweenTime){
      sleeping = true;
      Serial.println("RESET");
    }
  }
}

void shakeInterrupt(){
  sleeping = false;
  starttimer = millis();
  }

