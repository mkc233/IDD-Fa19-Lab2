# Digital Timer
 

## Part A. Solder your LCD panel

**Take a picture of your soldered panel and add it here!**
![LCD Setup](https://github.com/mkc233/IDD-Fa19-Lab2/blob/master/LcdDisplay.jpg)

## Part B. Writing to the LCD
 
**a. What voltage level do you need to power your display?**
I need 5 volts to power the display, per the schematic it also says the operating voltage is 5 volts at the VDD.

**b. What voltage level do you need to power the display backlight?**
Per directions in this lab it seems to be able to be powered by 3.3 volts.  
   
**c. What was one mistake you made when wiring up the display? How did you fix it?**
I didn't make any mistake wiring wise it was able to turn on the display on the first try.  However, my wiring is very messing it would probably be better next time to plan on the wiring to make it easier to troubleshoot.

**d. What line of code do you need to change to make it flash your name instead of "Hello World"?**
I need to change the lcd.print() and add the string "Michael"

**e. Include a copy of your Lowly Multimeter code in your lab write-up.**
```
// include the library code:
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

int sensorPin = A0;    // select the input pin for the potentiometer
int sensorValue = 0;  // variable to store the value coming from the sensor

void setup() {
    // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("Lowly Multimeter");
}

void loop() {
  // read the value from the sensor:
  sensorValue = analogRead(sensorPin);
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the voltage
  lcd.print(sensorValue);
}
```

## Part C. Using a time-based digital sensor


**Upload a video of your working rotary encoder here.**

[Rotary Encoder](https://youtu.be/ANHClgahPaw)


## Part D. Make your Arduino sing!

**a. How would you change the code to make the song play twice as fast?**
 To make the song play twice as fast I changed the pauseBetweenNotes variable by dividing it by 2.
 
**b. What song is playing?**
The Star Wars intro song is playing.

## Part E. Make your own timer

**a. Make a short video showing how your timer works, and what happens when time is up!**

[Cooking Timer](https://youtu.be/M8FLRsfIUu8)  

Simple cooking timer which asks the user to input the time desired for cooking in seconds by pushing the red button.  Once the user is ready to start the timer, the user will push the white button.  At the end of the countdown, the blue LED will go off and the display will notifity the user that the food is ready to eat.

Cooking Timer Code
```

// include the library code:
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
int time = millis();
int start = 0;
int countdown = 0;
int button = 7;

void setup() { 
  Serial.begin(9600);
  pinMode(7,INPUT_PULLUP);
  pinMode(8,INPUT_PULLUP);
  pinMode(9,OUTPUT);
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("Please set time");
}

void loop() {
  //Serial.println(digitalRead(button));
if (digitalRead(7) == 0){
  countdown+=1;
  delay(100);
  lcd.setCursor(0,1);
  lcd.print(countdown);
}

if (digitalRead(8) == 0){
  start = 1;
  lcd.clear();
}
if(start == 1){
  lcd.setCursor(0,0);
  lcd.print("Cooking........");
  for(int i = countdown; i >= 0; i--){
   if (i < 10){
    lcd.setCursor(1,1);
    lcd.print(" ");
    lcd.setCursor(0,1);
    lcd.print(i);
   }
  lcd.setCursor(0,1);
  lcd.print(i);
  delay(1000);
  }
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Ready to Eat!");
  lcd.setCursor(0,1);
  lcd.print("Enjoy!");
  digitalWrite(9, HIGH);
  exit(0);
}
}
```

**b. Post a link to the completed lab report your class hub GitHub repo.**
