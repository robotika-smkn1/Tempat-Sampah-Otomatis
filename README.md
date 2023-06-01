
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
- Servo Sg 90
- Sensor Ultra Sonic ( Hc-sr04 ) 2x
- Buzzer
- Led Gree ( Mendeteksi Sampah Kosong )
- Led Red ( Mendeteksi Sampah Penuh )
- Resistor 220 ohm 2x
- Lcd I2C ( Opsional )


# :mag: Ilustrasi Arduino

<p align="center">
  <img src="https://i.postimg.cc/XYtMwZ71/New.png" style="height:205px;" "width:205px;"/>
</p>


# :clipboard: Source Code Tanpa LCD-i2C By Robotika SMKN 1

```bash
/*
 * 
 * All the resources for this project: smkn1kotabekasi.sch.id
 * Modified by Robotika smkn1 kotabekasi
 * 
 * Created by Robotika smkn1 kotabekasi
 * 
 */

#include <Servo.h>

const int trigPin1 = 2; // Pin Trig Sensor Ultrasonik 1
const int echoPin1 = 3; // Pin Echo Sensor Ultrasonik 1
const int trigPin2 = 4; // Pin Trig Sensor Ultrasonik 2
const int echoPin2 = 5; // Pin Echo Sensor Ultrasonik 2
const int servoPin = 6; // Pin Servo Motor
const int buzzerPin = 7; // Pin Buzzer
const int greenLedPin = 8; // Pin LED Hijau
const int redLedPin = 9; // Pin LED Merah

Servo myservo;

void setup() {
  pinMode(trigPin1, OUTPUT);
  pinMode(echoPin1, INPUT);
  pinMode(trigPin2, OUTPUT);
  pinMode(echoPin2, INPUT);
  pinMode(servoPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  pinMode(greenLedPin, OUTPUT);
  pinMode(redLedPin, OUTPUT);

  myservo.attach(servoPin);

  // Inisialisasi LED Hijau dan LED Merah mati
  digitalWrite(greenLedPin, LOW);
  digitalWrite(redLedPin, LOW);
}

void loop() {
  // Sensor Ultrasonik 1 - Deteksi Sampah Masuk
  long duration1, distance1;
  digitalWrite(trigPin1, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin1, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin1, LOW);
  duration1 = pulseIn(echoPin1, HIGH);
  distance1 = duration1 * 0.034 / 2;

  if (distance1 < 10) { // Jarak pendeteksian jika sampah masuk
    if (digitalRead(redLedPin) == LOW) { // Cek jika sampah tidak penuh
      myservo.write(180); // Gerakkan servo ke posisi tertentu
      digitalWrite(buzzerPin, HIGH); // Nyalakan buzzer
      delay(90); // Delay 200 ms
      digitalWrite(buzzerPin, LOW); // Matikan buzzer
      delay(90); // Delay 200 ms
      digitalWrite(buzzerPin, HIGH); // Nyalakan buzzer
      delay(90); // Delay 200 ms
      digitalWrite(buzzerPin, LOW); // Matikan buzzer
      delay(200); // Delay 600 ms
    }
  } else {
    myservo.write(0); // Kembali ke posisi awal
    digitalWrite(buzzerPin, LOW); // Matikan buzzer
  }

  // Sensor Ultrasonik 2 - Deteksi Sampah Penuh atau Kosong
  long duration2, distance2;
  digitalWrite(trigPin2, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin2, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin2, LOW);
  duration2 = pulseIn(echoPin2, HIGH);
  distance2 = duration2 * 0.034 / 2;

  if (distance2 < 10) { // Jarak pendeteksian jika sampah penuh
    digitalWrite(greenLedPin, LOW); // Matikan LED Hijau
    digitalWrite(redLedPin, HIGH); // Nyalakan LED Merah
    myservo.write(0); // Kembali ke posisi awal
    digitalWrite(buzzerPin, LOW); // Matikan buzzer
  } else {
    digitalWrite(greenLedPin, HIGH); // Nyalakan LED Hijau
    digitalWrite(redLedPin, LOW); // Matikan LED Merah
  }

  delay(5); // Delay 1 detik
}

```



# :clipboard: Source Code Menggunakan LCD-i2C By Robotika SMKN 1

```bash
/*
 * 
 * All the resources for this project: smkn1kotabekasi.sch.id
 * Modified by Robotika smkn1 kotabekasi
 * 
 * Created by Robotika smkn1 kotabekasi
 * 
 */
 
 
#include <Servo.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

const int trigPin1 = 2; // Pin Trig Sensor Ultrasonik 1
const int echoPin1 = 3; // Pin Echo Sensor Ultrasonik 1
const int trigPin2 = 4; // Pin Trig Sensor Ultrasonik 2
const int echoPin2 = 5; // Pin Echo Sensor Ultrasonik 2
const int servoPin = 6; // Pin Servo Motor
const int buzzerPin = 7; // Pin Buzzer
const int greenLedPin = 8; // Pin LED Hijau
const int redLedPin = 9; // Pin LED Merah

Servo myservo;
LiquidCrystal_I2C lcd(0x27, 16, 2); // Inisialisasi LCD-I2C, sesuaikan alamat LCD sesuai dengan konfigurasi hardware

void setup() {
  pinMode(trigPin1, OUTPUT);
  pinMode(echoPin1, INPUT);
  pinMode(trigPin2, OUTPUT);
  pinMode(echoPin2, INPUT);
  pinMode(servoPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  pinMode(greenLedPin, OUTPUT);
  pinMode(redLedPin, OUTPUT);

  myservo.attach(servoPin);

  // Inisialisasi LED Hijau dan LED Merah mati
  digitalWrite(greenLedPin, LOW);
  digitalWrite(redLedPin, LOW);

  // Inisialisasi LCD
  lcd.begin(); // Inisialisasi LCD dengan ukuran 16 kolom dan 2 baris
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("ROBOTIKA SMKN 1");
}

void loop() {
  // Sensor Ultrasonik 1 - Deteksi Sampah Masuk
  long duration1, distance1;
  digitalWrite(trigPin1, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin1, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin1, LOW);
  duration1 = pulseIn(echoPin1, HIGH);
  distance1 = duration1 * 0.034 / 2;

  if (distance1 < 10) { // Jarak pendeteksian jika sampah masuk
    if (digitalRead(redLedPin) == LOW) { // Cek jika sampah tidak penuh
      myservo.write(180); // Gerakkan servo ke posisi tertentu
      digitalWrite(buzzerPin, HIGH); // Nyalakan buzzer
      delay(90); // Delay 200 ms
      digitalWrite(buzzerPin, LOW); // Matikan buzzer
      delay(90); // Delay 200 ms
      digitalWrite(buzzerPin, HIGH); // Nyalakan buzzer
      delay(90); // Delay 200 ms
      digitalWrite(buzzerPin, LOW); // Matikan buzzer
      delay(200); // Delay 600 ms
    }
  } else {
    myservo.write(0); // Kembali ke posisi awal
    digitalWrite(buzzerPin, LOW); // Matikan buzzer
  }

  // Sensor Ultrasonik 2 - Deteksi Sampah Penuh atau Kosong
  long duration2, distance2;
  digitalWrite(trigPin2, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin2, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin2, LOW);
  duration2 = pulseIn(echoPin2, HIGH);
  distance2 = duration2 * 0.034 / 2;

  if (distance2 < 10) { // Jarak pendeteksian jika sampah penuh
    digitalWrite(greenLedPin, LOW); // Matikan LED Hijau
    digitalWrite(redLedPin, HIGH); // Nyalakan LED Merah
    myservo.write(0); // Kembali ke posisi awal
    digitalWrite(buzzerPin, LOW); // Matikan buzzer
    lcd.setCursor(0, 1);
    lcd.print("Sampah Penuh    "); // Menampilkan teks "Sampah Penuh" pada LCD
  } else {
    digitalWrite(greenLedPin, HIGH); // Nyalakan LED Hijau
    digitalWrite(redLedPin, LOW); // Matikan LED Merah
    lcd.setCursor(0, 1);
    lcd.print("Sampah Kosong   "); // Menampilkan teks "Sampah Kosong" pada LCD
  }

  delay(5); // Delay 1 detik
}

```
