#include <Arduino.h>
#include <ESP32Servo.h>

Servo servo1;
Servo servo2;
Servo servo3;
Servo servo4;

const int PITCH_PIN = 34;
const int ROLL_PIN  = 35;


const int SERVO1_PIN = 13;
const int SERVO2_PIN = 14;
const int SERVO3_PIN = 25;
const int SERVO4_PIN = 26;

const float SERVO_CENTER = 90.0;

const float MAX_ANGLE = 30.0;

const float MAX_SERVO_DEFLECTION = 25.0;

void setup() {

  Serial.begin(115200);

  
  pinMode(PITCH_PIN, INPUT);
  pinMode(ROLL_PIN, INPUT);

  
  servo1.attach(SERVO1_PIN);
  servo2.attach(SERVO2_PIN);
  servo3.attach(SERVO3_PIN);
  servo4.attach(SERVO4_PIN);

  servo1.write(90);
  servo2.write(90);
  servo3.write(90);
  servo4.write(90);

  delay(1000);

  Serial.println();
  Serial.println(" # ");
  Serial.println(" ESP32 BENCH SIMULATION");
  Serial.println(" # ");
  Serial.println();
}

void loop() {

  unsigned long startTime = micros();


  int pitchRaw = analogRead(PITCH_PIN);
  int rollRaw  = analogRead(ROLL_PIN);

  float pitch = map(
    pitchRaw,
    0,
    4095,
    -MAX_ANGLE,
    MAX_ANGLE
  );

  float roll = map(
    rollRaw,
    0,
    4095,
    -MAX_ANGLE,
    MAX_ANGLE
  );


  pitch = constrain(
    pitch,
    -MAX_ANGLE,
    MAX_ANGLE
  );

  roll = constrain(
    roll,
    -MAX_ANGLE,
    MAX_ANGLE
  );


  float pitchCommand =
    (pitch / MAX_ANGLE) *
    MAX_SERVO_DEFLECTION;

  float rollCommand =
    (roll / MAX_ANGLE) *
    MAX_SERVO_DEFLECTION;


  float servo1Angle =
    SERVO_CENTER
    + pitchCommand
    + rollCommand;

  float servo2Angle =
    SERVO_CENTER
    + pitchCommand
    - rollCommand;

  float servo3Angle =
    SERVO_CENTER
    - pitchCommand
    + rollCommand;

  float servo4Angle =
    SERVO_CENTER
    - pitchCommand
    - rollCommand;

  servo1Angle = constrain(
    servo1Angle,
    65,
    115
  );

  servo2Angle = constrain(
    servo2Angle,
    65,
    115
  );

  servo3Angle = constrain(
    servo3Angle,
    65,
    115
  );

  servo4Angle = constrain(
    servo4Angle,
    65,
    115
  );

  servo1.write((int)servo1Angle);
  servo2.write((int)servo2Angle);
  servo3.write((int)servo3Angle);
  servo4.write((int)servo4Angle);

  unsigned long loopTime = micros() - startTime;

  Serial.print("Pitch: ");
  Serial.print(pitch, 1);

  Serial.print(" deg | Roll: ");
  Serial.print(roll, 1);

  Serial.print(" deg | ");

  Serial.print("S1: ");
  Serial.print(servo1Angle, 1);

  Serial.print(" | S2: ");
  Serial.print(servo2Angle, 1);

  Serial.print(" | S3: ");
  Serial.print(servo3Angle, 1);

  Serial.print(" | S4: ");
  Serial.print(servo4Angle, 1);

  Serial.print(" | Loop: ");
  Serial.print(loopTime);

  Serial.println(" us");

  delay(5);
}
