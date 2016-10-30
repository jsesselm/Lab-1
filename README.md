int ledPin1 = 9;
int ledPin2 = 10;
int ledPin3 = 11;
int buttonPin1 = 2;
int buttonPin2 = 4;
int buttonPin3 = 7;
int pot = A1;
int buttonState1 = 0;
int buttonState2 = 0;
int buttonState3 = 0;
int sensorValue = 0;

void setup() {
  Serial.begin(9600);
  pinMode(ledPin1, OUTPUT);
  pinMode(ledPin2, OUTPUT);
  pinMode(ledPin3, OUTPUT);
  pinMode(buttonPin1, INPUT);
  pinMode(buttonPin2, INPUT);
  pinMode(buttonPin3, INPUT);
}

void loop() {
  sensorValue = analogRead(pot);
  int potentiometer = map(sensorValue, 0, 1024, 0, 255);
  buttonState1 = digitalRead(buttonPin1);
  buttonState2 = digitalRead(buttonPin2);
  buttonState3 = digitalRead(buttonPin3);
  Serial.print("button state: ");
  Serial.print(buttonState1);
  Serial.print(buttonState2);
  Serial.print(buttonState3);
  Serial.print(", Sensor value: ");
  Serial.print(sensorValue);
  Serial.print(", brightnes: ");
  Serial.println(potentiometer);
  
  if (buttonState1 == HIGH) {
    analogWrite(ledPin2, 255);
    delay(potentiometer/2);
    analogWrite(ledPin2, 0);
    delay(potentiometer);
    analogWrite(ledPin1, 255);
    delay(potentiometer/2);
    analogWrite(ledPin1, 0);
    delay(potentiometer);
  }
  
  else {
    analogWrite(ledPin1, 0);
  }
  
  if (buttonState2 == HIGH) {
    analogWrite(ledPin2, potentiometer);
    delay(potentiometer);
    analogWrite(ledPin2, 0);
    delay(potentiometer);

    for(int i=0; i<255; i++) {
      analogWrite(ledPin2, i);
      delay(potentiometer/50);
    }  
    
    for(int j=255; j>1; j--) {
      analogWrite(ledPin2, j);
      delay(potentiometer/50);
    }
  } 
  
  else {
    analogWrite(ledPin2, 0);
  }
  
  if (buttonState3 == HIGH) {
    analogWrite(ledPin3, 255);
    delay(potentiometer);
    analogWrite(ledPin3,100);
    delay(potentiometer/2);
    analogWrite(ledPin2, 200);
    delay(potentiometer/2);
    analogWrite(ledPin2,50);
    delay(potentiometer);
    analogWrite(ledPin1, 100);
    delay(potentiometer);
    analogWrite(ledPin1,20);
    delay(potentiometer);
  } 
  
  else {
    analogWrite(ledPin3, 0);
  }
}
