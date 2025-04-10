
#include <LiquidCrystal_I2C.h>
#define IR_SENSOR_PIN 6 
LiquidCrystal_I2C lcd(0x27,16,2);//has 16 coloumn and 2 rows 


int count=0;//count made 0
int prevvalue=0;
int currentvalue=0;


void setup() {

 lcd.init();
 lcd.backlight();


pinMode(IR_SENSOR_PIN,INPUT);



Serial.begin(9600);



}

void loop() {



int irState=digitalRead(IR_SENSOR_PIN);
lcd.setCursor(0,0);
lcd.print("Count : ");


if(irState==HIGH&&prevvalue==0&&currentvalue==0)
{
  
  prevvalue=0;
  currentvalue=1;
}
if(irState==HIGH&&prevvalue==0&&currentvalue==1)
{

prevvalue=1;
currentvalue=1;




}
if(irState==LOW&&prevvalue==1&&currentvalue==1)
{
  prevvalue=1;
  currentvalue=0;
  count=count+1;
  lcd.clear();
  lcd.setCursor(0,1);


  lcd.print(count);

}
if(irState==LOW&&prevvalue==1&&currentvalue==0)

{
  prevvalue=0;
  currentvalue=0;
}
delay(500);

}
