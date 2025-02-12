# SHORT_CIRCUIT
link: https://www.tinkercad.com/things/gfqq4AjWAwt-short-circuit-task/editel?sharecode=AbWKF-FnrkNPMByAqWUFE6bN-IkcKxYZ9rJBt0KeVGA 


const int redPin = 8;
const int yellowPin = 9;
const int greenPin = 10;
const int buttonPin = 13;

int buttonState = 0;  
int lastButtonState = 0; 

unsigned long previousMillis = 0;
const long interval = 1000; 

  void setup() {
  pinMode(redPin, OUTPUT);
  pinMode(yellowPin, OUTPUT);
  pinMode(greenPin, OUTPUT);

  pinMode(buttonPin, INPUT);

  digitalWrite(redPin, HIGH);
  digitalWrite(yellowPin, LOW);
  digitalWrite(greenPin, LOW);
}

void loop() {
  buttonState = digitalRead(buttonPin);
  
  if (buttonState == HIGH && lastButtonState == LOW) {
    delay(50);
    digitalWrite(redPin, HIGH);
    digitalWrite(yellowPin, LOW);
    digitalWrite(greenPin, LOW);
  } 
  else if (buttonState == LOW) {
    unsigned long currentMillis = millis();
    
    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;

      if (digitalRead(redPin) == HIGH) {
        digitalWrite(redPin, LOW);
        digitalWrite(greenPin, HIGH);
      }
      else if (digitalRead(greenPin) == HIGH) {
        digitalWrite(greenPin, LOW);
        digitalWrite(yellowPin, HIGH);
      }
      else if (digitalRead(yellowPin) == HIGH) {
        digitalWrite(yellowPin, LOW);
        digitalWrite(redPin, HIGH);
      }
    }
  }

  lastButtonState = buttonState;
}
