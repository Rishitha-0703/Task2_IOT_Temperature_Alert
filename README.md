const int tempPin = A0;
const int ledPin = 8;
const int buzzerPin = 9;

const float threshold = 30.0;

void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int reading = analogRead(tempPin);

  float voltage = reading * (5.0 / 1023.0);
  float temperatureC = (voltage - 0.5) * 100.0;

  Serial.print("Temperature: ");
  Serial.print(temperatureC);
  Serial.println(" C");

  if (temperatureC > threshold) {
    digitalWrite(ledPin, HIGH);
    tone(buzzerPin, 1000);
  } else {
    digitalWrite(ledPin, LOW);
    noTone(buzzerPin);
  }

  delay(1000);
}
