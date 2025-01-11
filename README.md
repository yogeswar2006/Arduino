# Arduino
Ultrasonic sensor is connected with Arduino along with Led and buzzer .whenever sensor detects object in short radius ,the buzzer will sound along blinking of led
// Define the pin numbers for the ultrasonic sensor and LED
const int trigPin = 11;
const int echoPin = 10;
const int ledPin = 8;
const int BuzzerPin = 3;

// Variables for the duration and distance
long duration;
int distance;

void setup() {
  // Initialize the serial communication
  Serial.begin(9600);
  
  // Set the ultrasonic sensor pins as input and output
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  
  // Set the LED pin as output
  pinMode(ledPin, OUTPUT);
  pinMode(BuzzerPin, OUTPUT);
}

void loop() {
  // Clear the trigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  // Set the trigPin on HIGH state for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Read the echoPin and calculate the duration
  duration = pulseIn(echoPin, HIGH);
  
  // Calculate the distance (duration * speed of sound / 2)
  distance = duration * 0.034 / 2;
  
  // Print the distance to the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  
  // If the distance is less than or equal to 10 cm, turn on the LED
  if (distance <= 40) {
    digitalWrite(ledPin, HIGH);
    digitalWrite(BuzzerPin,HIGH);
  } else {
    // Otherwise, turn off the LED
    digitalWrite(ledPin, LOW);
    digitalWrite(BuzzerPin, LOW);
  }
  
  // Add a short delay before the next loop
  delay(200);
}
