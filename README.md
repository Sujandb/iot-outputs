CODE :-

/*************************************************************
  Blynk is a platform with iOS and Android apps to control
  ESP32, Arduino, Raspberry Pi and the likes over the Internet.
  You can easily build mobile and web interfaces for any
  projects by simply dragging and dropping widgets.

    Downloads, docs, tutorials: https://www.blynk.io
    Sketch generator:           https://examples.blynk.cc
    Blynk community:            https://community.blynk.cc
    Follow us:                  https://www.fb.com/blynkapp
                                https://twitter.com/blynk_app

  Blynk library is licensed under MIT license
 *************************************************************
  Blynk.Edgent implements:
  - Blynk.Inject - Dynamic WiFi credentials provisioning
  - Blynk.Air    - Over The Air firmware updates
  - Device state indication using a physical LED
  - Credentials reset using a physical Button
 *************************************************************/

/* Fill in information from your Blynk Template here */
/* Read more: https://bit.ly/BlynkInject */
//#define BLYNK_TEMPLATE_ID           "TMPxxxxxx"
//#define BLYNK_TEMPLATE_NAME         "Device"
#define BLYNK_TEMPLATE_ID "TMPL3VQo-0pzz"
#define BLYNK_TEMPLATE_NAME "esp32quickstart"
#define BLYNK_FIRMWARE_VERSION        "0.1.0"


#define BLYNK_PRINT Serial
//#define BLYNK_DEBUG

#define APP_DEBUG

// Uncomment your board, or configure a custom board in Settings.h
//#define USE_ESP32_DEV_MODULE
//#define USE_ESP32C3_DEV_MODULE
//#define USE_ESP32S2_DEV_KIT
//#define USE_WROVER_BOARD
//#define USE_TTGO_T7
//#define USE_TTGO_T_OI

#include "BlynkEdgent.h"
#include<WiFi.h>
char ssid[] = "iQOO 7";
char pass[] = "vishnusa";

void setup()
{
  Serial.begin(115200);
  delay(100);

  BlynkEdgent.begin();
}

void loop() {
  BlynkEdgent.run();
}



#include "BlynkEdgent.h"
#include <Deneyap_Servo.h>
int ldr1 = A0;
int ldr2 = A1;
int pos;
int voltage1 = 12;
int voltage2 = 11;
Servo myservo; 



void servo_ldr()
{
  int  ldr1_read = analogRead(ldr1);
  int  ldr2_read = analogRead(ldr2);
  Serial.print("light1 = ");
  Serial.println(ldr1_read);
  Serial.print("light2 = ");
  Serial.println(ldr2_read);
  int map1 = map(ldr1_read,0,8191,52,0);
  int map2 = map(ldr2_read,0,8191,53,105);
  if(ldr1_read>=ldr2_read)
  {
      myservo.write(map1);
      delay(30);
  }
  else
  {
      myservo.write(map2);
      delay(30);
  } 
}
/*BLYNK_WRITE(V0)
{
  int pinValue = param.asInt();
  digitalWrite(42,pinValue);

}
BLYNK_WRITE(V1)
{
  int pinValue = param.asInt();
  digitalWrite(5,pinValue);

}
BLYNK_WRITE(V2)
{
  int pinValue = param.asInt();
  digitalWrite(6,pinValue);

}*/

void setup()
{
  WiFi.begin(ssid,pass);
  pinMode(ldr1,INPUT);
  pinMode(ldr2,INPUT);
  pinMode(voltage1,INPUT);
  pinMode(voltage2,INPUT);
  Serial.begin(9600);
  myservo.attach(9); 
  delay(100);

  BlynkEdgent.begin();
}

void loop() {
  for(i=0;i<50;i++)
  {
  servo_ldr();
  float volt1 = analogRead(voltage1);
  
  float volt2 = analogRead(voltage2);

  float vout_solar = (volt1/15500)*25;
  float vout_battery = (volt2/15500)*25;
  
  Serial.print("solar voltage = ");
  Serial.println(vout_solar);
  Serial.print("battery voltage = ");
  Serial.println(vout_battery);

  float map_volt1 = map(vout_battery,3.3,4.2,0,100);
  
  Blynk.virtualWrite(V0, vout_solar);
  Blynk.virtualWrite(V1,vout_battery);
  Blynk.virtualWrite(V2, mapping);
  
  //Blynk.virtualWrite(V4, millis() / 1000);
  delay(2000);
  BlynkEdgent.run();
  }
}






OUTPUT ON BLYNK IOT:-

![Screenshot 2023-11-23 181543](https://github.com/Sujandb/iot-outputs/assets/109717277/ef73f8b2-36cc-46e9-9b75-aeb3945828dd)
![Screenshot 2023-11-23 174353](https://github.com/Sujandb/iot-outputs/assets/109717277/ab38a558-d448-43cf-9ce5-64224730b39b)
![Screenshot 2023-11-23 174333](https://github.com/Sujandb/iot-outputs/assets/109717277/a65d61f4-462c-41b0-a2fb-c53ea8440ef4)
![Screenshot 2023-11-23 174317](https://github.com/Sujandb/iot-outputs/assets/109717277/b1ebfb18-16a4-423e-8b15-a2e2e1d70f49)
![Screenshot 2023-11-23 174305](https://github.com/Sujandb/iot-outputs/assets/109717277/bf8d2d33-2db1-4c8c-b084-5de34c24e7d7)
# iot-outputs
