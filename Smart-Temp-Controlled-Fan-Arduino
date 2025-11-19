#include <Wire.h>
#include <WiFi.h>
#include <LiquidCrystal_I2C.h>   // Use ESP32-compatible version (see note below)

#define LM35_PIN   34     // LM35 analog input
#define GREEN_LED  15
#define RED_LED    13

// DFRobot Motor Driver Pins
#define MOTOR_PWM  26     // Connect to PWM pin on motor module
#define MOTOR_DIR  27     // Connect to DIR pin on motor module

LiquidCrystal_I2C lcd(0x27, 16, 2);

// PWM settings
const int freq = 5000;
const int resolution = 8;  // 8-bit = 0-255

void setup() {
  Serial.begin(115200);
  delay(500);
  Serial.println("===== SMART FAN SYSTEM STARTING =====");

  pinMode(GREEN_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  pinMode(MOTOR_DIR, OUTPUT);
  digitalWrite(MOTOR_DIR, HIGH);  // Forward direction (fan cooling)

  // === NEW ESP32 PWM API (2023+) - ONLY ONE LINE NEEDED ===
  ledcAttach(MOTOR_PWM, freq, resolution);
  // ========================================================

  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("System Ready");
  delay(2000);
}

void loop() {
  int raw = analogRead(LM35_PIN);
  float voltage = raw * (3.3 / 4095.0);
  float tempC = voltage * 100.0;

  Serial.printf("Temp: %.2f °C\n", tempC);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(tempC, 1);
  lcd.print(" C");

  // Smart temperature control
  if (tempC >= 28.0) {
    digitalWrite(MOTOR_DIR, HIGH);
    ledcWrite(MOTOR_PWM, 255);   // Full speed
    ledOn(RED_LED);
    ledOff(GREEN_LED);
    lcd.setCursor(0, 1);
    lcd.print("FAN: ON  100%");
  } 
  else if (tempC >= 25.0) {
    digitalWrite(MOTOR_DIR, HIGH);
    ledcWrite(MOTOR_PWM, 200);   // High speed
    ledOn(RED_LED);
    ledOff(GREEN_LED);
    lcd.setCursor(0, 1);
    lcd.print("FAN: ON   80%");
  }
  else if (tempC >= 15.0) {
    digitalWrite(MOTOR_DIR, HIGH);
    ledcWrite(MOTOR_PWM, 130);   // Medium-low (starts reliably)
    ledOff(GREEN_LED);
    ledOn(RED_LED);
    lcd.setCursor(0, 1);
    lcd.print("FAN: ON   50%");
  }
  else {
    ledcWrite(MOTOR_PWM, 0);     // OFF
    ledOff(RED_LED);
    ledOn(GREEN_LED);
    lcd.setCursor(0, 1);
    lcd.print("FAN: OFF     ");
  }

  delay(1000);
}

void ledOn(int pin)  { digitalWrite(pin, HIGH); }
void ledOff(int pin) { digitalWrite(pin, LOW); }
