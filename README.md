# sm23a-ultra.sonic.and.ldr
# parte 01 : Ultrasonic Sensor Arduino and LCD 16x2 Project
# Introduction
The goal of this project is to demonstrate how to interface an ultrasonic sensor with an Arduino and display the measured distance on an LCD 16x2 screen. Ultrasonic sensors work by emitting a sound wave and measuring the time it takes for the wave to bounce back after hitting an object. This time can be converted into a distance measurement.
# Components
Arduino Uno or compatible board
Ultrasonic Sensor (HC-SR04)
LCD 16x2 Display (compatible with the Hitachi HD44780 driver)
Breadboard and jumper wires
Potentiometer (for LCD contrast adjustment)
# Circuit Connection
We start with Arduino Uno connected to 16 by two LCD.
Four pins of data and enable pin and register select pins connected to Arduino.
The VCC and ground connected to 5 volts and ground in Arduino Uno. Read Write and contrast pins connected to ground the backlight led positive pin connected to VCC.
The negative pin of the backlight led connected to negative through one kilo ohm resistor. Here is the HC-SR04 ultrasonic sensor it has two elements one element called trigger that’s the ultrasonic transmitter and hat’s the receive element called echo.
VCC connected to five volts and ground connected to the ground and here is the trigger or transmit pin connected to Arduino to pin number nine.
And the echo connected to pin number ten.
# Arduino Code

#include <LiquidCrystal.h> // includes the LiquidCrystal Library

LiquidCrystal lcd(1, 2, 4, 5, 6, 7); // Creates an LCD object. Parameters: (rs, enable, d4, d5, d6, d7)

const int trigPin = 9;

const int echoPin = 10;

long duration;

int distanceCm, distanceInch;

void setup() {

lcd.begin(16,2); // Initializes the interface to the LCD screen, and specifies the dimensions (width and height) of the display

pinMode(trigPin, OUTPUT);

pinMode(echoPin, INPUT);

}

void loop() {

digitalWrite(trigPin, LOW);

delayMicroseconds(2);

digitalWrite(trigPin, HIGH);

delayMicroseconds(10);

digitalWrite(trigPin, LOW);

duration = pulseIn(echoPin, HIGH);

distanceCm= duration*0.034/2;

distanceInch = duration*0.0133/2;

lcd.setCursor(0,0); // Sets the location at which subsequent text written to the LCD will be displayed

lcd.print("Distance: "); // Prints string "Distance" on the LCD

lcd.print(distanceCm); // Prints the distance value from the sensor

lcd.print(" cm");

delay(10);

lcd.setCursor(0,1);

lcd.print("Distance: ");

lcd.print(distanceInch);

lcd.print(" inch");

delay(10);

}
