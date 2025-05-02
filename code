#include <LiquidCrystal.h>

// LCD Pins
#define LCD_RS 4
#define LCD_EN 5
#define LCD_D4 12
#define LCD_D5 13
#define LCD_D6 14
#define LCD_D7 15

// LDR Pin
#define LDR_PIN 2 // Updated to GPIO 2

// IR Sensor Pins
#define IR_SENSOR_1 10  // GPIO pin for IR Sensor 1
#define IR_SENSOR_2 6  // GPIO pin for IR Sensor 2

// Threshold for significant change
const int threshold = 50;

LiquidCrystal lcd(LCD_RS, LCD_EN, LCD_D4, LCD_D5, LCD_D6, LCD_D7);
int ldrValue = 0;
int prevLdrValue = 0;
bool irSensor1State = false;
bool irSensor2State = false;

void setup() {
  // Initialize Serial Monitor
  Serial.begin(115200);

  // Initialize LCD
  lcd.begin(16, 2);
  lcd.print("Initializing...");
  delay(2000);
  lcd.clear();

  // Initialize IR Sensor pins
  pinMode(IR_SENSOR_1, INPUT);
  pinMode(IR_SENSOR_2, INPUT);
}

void loop() {
  // Read ADC value from the LDR
  ldrValue = analogRead(LDR_PIN);

  // Calculate voltage
  float voltage = ldrValue * (3.3 / 4095.0);
  Serial.print("LDR ADC Value: ");
  Serial.println(ldrValue);
  Serial.print("LDR Voltage: ");
  Serial.println(voltage, 3);

  // Check for changes in LDR
  if (abs(ldrValue - prevLdrValue) > threshold) {
    lcd.clear();
    lcd.print("Change Detected");
    Serial.println("Change Detected");
  } else {
    lcd.clear();
    lcd.print("No Change");
    Serial.println("No Change");
  }

  // Update previous LDR value
  prevLdrValue = ldrValue;

  // Read IR Sensor states
  irSensor1State = digitalRead(IR_SENSOR_1);
  irSensor2State = digitalRead(IR_SENSOR_2);

  // Display IR Sensor states on Serial Monitor
  Serial.print("IR Sensor 1: ");
  Serial.println(irSensor1State ? "Obstacle Detected" : "No Obstacle");
  Serial.print("IR Sensor 2: ");
  Serial.println(irSensor2State ? "Obstacle Detected" : "No Obstacle");

  // Display IR Sensor states on LCD
  lcd.setCursor(0, 1); // Move to the second row
  if (irSensor1State || irSensor2State) {
    lcd.print("IR: Obstacle Det.");
  } else {
    lcd.print("IR: Clear Path  "); // Ensure old text is overwritten
  }

  // Short delay before next reading
  delay(500);
}
