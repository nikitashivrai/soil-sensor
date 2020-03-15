# soil-sensor

#include "UbidotsMicroESP8266.h"
const int sensor_pin = A0;  
#define TOKEN "aio_ttYK411PIZ6L82nRRlca1hOoXH2L"
#define WIFISSID "AndroidAP8085" 
#define PASSWORD"galaxy@123"
Ubidots client (TOKEN);
void setup() {
  Serial.begin(9600);
  client.wifiConnection(WIFISSID,PASSWORD);

}

void loop() {
  float moisture_percentage;

  moisture_percentage = ( 100.00 - ( (analogRead(sensor_pin)/1023.00) * 100.00 ) );

  Serial.print("Soil Moisture(in Percentage) = ");
  Serial.print(moisture_percentage);
  Serial.println("%");
  client.add("soilmoisture",moisture_percentage);

  delay(1000);
  client.sendAll(true);
}
