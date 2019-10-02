# sumobot-beginner-competition

const int A1A = 13;
const int A1B = 12;
const int B1A = 11;
const int B1B = 10;
const int trigPin = 8;
const int echoPin = 7;
const int pwmPin = 3;
int num;
long duration;
int distance;

void setup() {
  // put your setup code here, to run once:
  pinMode(B1A,OUTPUT);
  pinMode(B1B,OUTPUT);
  pinMode(A1A,OUTPUT);
  pinMode(A1B,OUTPUT);
  pinMode(trigPin,OUTPUT);
  pinMode(echoPin,INPUT);
  pinMode(pwmPin,OUTPUT);
  Serial.begin(9600);
  delay(5000);
}

void loop() {
  analogWrite(pwmPin,255);
  getUltrasonicDistance();
  num = analogRead(A0);
  Serial.println(A0);
  /*if (num > 1022) 
  {
    moveBackward();
    delay(500);
  
  else */
  {
    if (distance < 80 || (distance > 2170 && distance < 2250))
    {
      moveForward();
    }
    else 
    {
      spinLeft();
    }
  }
}

// Functions

int getUltrasonicDistance()
{
  // Clears the trigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  // Sets the trigPin on HIGH state for 10 micro seconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  // Calculating the distance
  distance = duration*0.034/2; //distance in cm
  return distance;
}

void moveStop()
{
  digitalWrite(A1A,LOW);
  digitalWrite(A1B,LOW);
  digitalWrite(B1A,LOW);
  digitalWrite(B1B,LOW);
}

void moveForward()
{
  digitalWrite(A1A,LOW);
  digitalWrite(A1B,HIGH);
  digitalWrite(B1A,HIGH);
  digitalWrite(B1B,LOW);
}

void moveRight()
{
  digitalWrite(A1A,LOW);
  digitalWrite(A1B,HIGH);
  digitalWrite(B1A,LOW);
  digitalWrite(B1B,HIGH);
}

void spinLeft()
{
  digitalWrite(A1A,HIGH);
  digitalWrite(A1B,LOW);
  digitalWrite(B1A,LOW);
  digitalWrite(B1B,LOW);
}

void moveBackward()
{
  digitalWrite(A1A,HIGH);
  digitalWrite(A1B,LOW);
  digitalWrite(B1A,LOW);
  digitalWrite(B1B,HIGH);
}
