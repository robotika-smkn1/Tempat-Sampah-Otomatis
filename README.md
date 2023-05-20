
# :pushpin: Tempat-Sampah-Otomatis



<p align="center">
  <img src="https://i.postimg.cc/tRZw0xQ4/logo-removebg-preview.png" alt="robotika smkn1 kotabekasi logo"/ style="height:350px;" "width: 350px;">
</p>


[![Version](https://img.shields.io/badge/VENOM-1.0.17-brightgreen.svg?maxAge=259200)]()
[![Stage](https://img.shields.io/badge/Release-Stable-brightgreen.svg)]()
![licence](https://img.shields.io/badge/license-GPLv3-brightgreen.svg)
[![Coverity Scan Build Status](https://scan.coverity.com/projects/aircrack-ng/badge.svg)](##Link##)



## :inbox_tray: Media Social Instagram

To keep this collection up-to-date need contributors who can add more Program Arduino scripts
||
|--------------|
|:mailbox_with_mail: [artha_sa_](https://www.instagram.com/artha_sa_/)
|:mailbox_with_mail: [dicky_asqaelani26](https://www.instagram.com/dicky_asqaelani26/)
|:mailbox_with_mail: [rahmatnurraya](https://www.instagram.com/rahmatnurraya990/)
|:mailbox_with_mail: [applepi_fthur](https://www.instagram.com/applepi_fthur/)
|:mailbox_with_mail: [robotika-smkn1](https://www.instagram.com/robotika.smkn1kotabekasi/)


# :moneybag: [Donate](https://saweria.co/arthasyarif)


# :briefcase: Barang & Bahan
- Arduino Uno
- Kabel Male & Female
- Servo Sg/Mg
- Sensor Ultra Sonic ( Hc-sr04 )


# :mag: Ilustrasi Arduino

<p align="center">
  <img src="https://i.postimg.cc/qBXmvgWr/Untitled-1.png" style="height:205px;" "width:205px;"/>
</p>


# :clipboard: Source Code By Robotika SMKN 1

```bash
/*
 * 
 * All the resources for this project: smkn1kotabekasi.sch.id
 * Modified by Robotika smkn1 kotabekasi
 * 
 * Created by Robotika smkn1 kotabekasi
 * 
 */

#include <Wire.h>   
#include <Servo.h>
Servo myservo; 
#define trigPin 8
#define echoPin 9 
const int buzzer = 11;
const int ledPin = 13;
long duration; 
int distance = 0; 
int pos = 0;   
int safetyDistance;

void setup()
{
    myservo.attach(10);
pinMode(trigPin, OUTPUT); // setting triggerpin sebagai output
pinMode(echoPin, INPUT); // setting echopin sebagai Input
pinMode(buzzer, OUTPUT);
pinMode(ledPin, OUTPUT);
Serial.begin(9600); // setting kecepatan pengiriman serial monitor

}
void loop()
{
digitalWrite(trigPin, HIGH);// aktifkan sensor ultrasonic
delayMicroseconds(10); // selama 10 microseconds
digitalWrite(trigPin, LOW); // matikan sensor ultrasonic
duration = pulseIn(echoPin, HIGH); // baca rentan waktu dari trigPin High sampai echoPin high
distance= duration*0.034/2; //konversi selang waktu ke CM


if (safetyDistance <= 30) // Hanya menampilkan jarak jika jaraknya kurang dari 300 cm / 3 meter
{
Serial.println(distance); // kirim data jarak ke PC
   myservo.write(130);
   delay(3000);
  digitalWrite(buzzer, HIGH);
  digitalWrite(ledPin, HIGH);  
}

else
{
  digitalWrite(buzzer, LOW);
  digitalWrite(ledPin, LOW);
  
    myservo.write(0);         
  }
}
 

```
