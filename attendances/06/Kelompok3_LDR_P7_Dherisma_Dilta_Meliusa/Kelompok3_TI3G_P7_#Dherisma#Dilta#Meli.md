## LDR dan HC-SR04 
## Laporan Praktikum Pertemuan 7 IoT
### Kelompok 3 
Nama Anggota Kelompok :
1. Dherisma Hanindita Utami (07)
2. Dilta Febiana (08)
3. Meliusa Nora Hariyanti (13)

### Praktikum 1 - Membaca data intensitas cahaya
Berikut source code untuk membaca data intensitas cahaya <br>
File main.cpp
```
#include <Arduino.h>

#define sensorLDR A0
int nilaiSensor;

void setup()
{
  Serial.begin(115200);
  Serial.println("Contoh Penggunaan Sensor LDR");
  delay(3000);
}

void loop()
{
  nilaiSensor = analogRead(sensorLDR);
  Serial.print("Nilai Sensor : ");
  Serial.println(nilaiSensor);
  delay(1000);
}
```
File platform.ini
```
[env:esp12e]
platform = espressif8266
board = esp12e
framework = arduino

monitor_speed = 115200
```
Untuk hasil output dari kode program diatas seperti berikut :
<image src= "1.jpg">
Hasil Output di Rangkaiannya sebagai berikut :
<image src= "2.jpg">
lalu ketika ditutup ldr nya ditutup maka lampunya nyala satu.
<image src= "3.jpg">

### Praktikum 2 - Membaca data jarak benda
Syntax Program :
Setelah rangkaian elektrik telah selesai anda rangkai, selanjutnya hal yang perlu anda lakukan adalah menulis syntax program sesuai dengan nomor pin dari rangkaian elektrik tersebut. Berikut ini langkah-langkah dalam menulis serta uploading pada nodeMCU:
```
#define triggerPin D1
#define echoPin D2

void setup() {
   Serial.begin (115200);
   pinMode(triggerPin, OUTPUT);
   pinMode(echoPin, INPUT);
  //  pinMode(BUILTIN_LED, OUTPUT);
}

void loop() {
   long duration, jarak;
   digitalWrite(triggerPin, LOW);
   delayMicroseconds(2);
   digitalWrite(triggerPin, HIGH);
   delayMicroseconds(10);
   digitalWrite(triggerPin, LOW);
   duration = pulseIn(echoPin, HIGH);
   jarak = duration * 0.034 / 2;
   Serial.print(jarak);
   Serial.println(" cm");
   delay(2000);
}
```
Output di monitor sebagai berikut :
<image src= "4.jpg">
Rangkaian :
<image src= "5.jpg">
Rangkaian di Wokwi :
<image src= "6.jpg">
source code di wokwi :
<image src= "7.jpg">
Output di wokwi :
<image src= "11.png">

## TUGAS
1. Buatlah sebuah rangkaian untuk LED, sensor cahaya dan sensor suhu menggunakan fritzing, kemudian buatlah program dengan skenario sebagai berikut

    Ketika cahaya redup dan suhu kategori dingin maka LED warna biru akan berkedip-kedip.
    Ketika cahaya terang dan suhu tergolong tinggi, LED merah akan menyala.
    Ketika tidak memiliki LED RGB, silakan memanfaatkan LED build in adalah LED bawaan esp8266, biasanya berwarna biru atau merah 2.<br>
    Jawab :
```
#include <Arduino.h>
#include <SimpleDHT.h>

#define pinDHT 7 // SD3 pin signal sensor DHT

byte temperature = 0;
byte humidity = 0;

SimpleDHT11 dht11(D0); // instan sensor dht11

#define sensorLDR A0
int nilaiSensor;
// Deklarasi pin untuk setiap LED
#define pinDHT 7 // SD3 pin signal sensor DHT
#define RED_PIN D1
#define GREEN_PIN D7
#define BLUE_PIN D3

int nilaiSuhu;

void setup()
{
  pinMode(RED_PIN, OUTPUT);
  pinMode(GREEN_PIN, OUTPUT);
  pinMode(BLUE_PIN, OUTPUT);
  Serial.begin(115200);
  Serial.println("Contoh Penggunaan Sensor LDR");
  delay(3000);
}

void loop()
{

  int err = SimpleDHTErrSuccess;

  if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
  {
    Serial.print("Pembacaan DHT11 gagal, err=");
    Serial.println(err);
    delay(1000);
    return;
  }

  nilaiSensor = analogRead(sensorLDR);
  if (nilaiSensor <= 500 && temperature < 31)
  {
    digitalWrite(RED_PIN, HIGH);
    digitalWrite(GREEN_PIN, LOW);
    digitalWrite(BLUE_PIN, LOW);
  }
  else
  {
    digitalWrite(RED_PIN, LOW);
    digitalWrite(GREEN_PIN, LOW);
    digitalWrite(BLUE_PIN, HIGH);
  }

  Serial.print("Sample OK: ");
  Serial.print((int)temperature);
  Serial.print(" *C, ");
  Serial.println("");
  Serial.print("Nilai Sensor : ");
  Serial.println(nilaiSensor);
  delay(1000);
}
```
Output dirangkaian :<br>
Jika cahaya redup dan kategori suhu dingin maka LED akan nyala warna biru.
<image src= "9.jpg">
Jika cahaya terang dan suhu tinggi maka akan nyala LED Merah.
<image src= "8.jpg">

    Buatlah rangkaian dan kode programnya dimana:

    Terdapat tambahan 1 LED RGB,

    LED Blue menyala jika jarak yang terbaca 1 cm
    LED Green menyala jika jarak yang terbaca 2 cm
    LED Red menyala jika jarak yang terbaca 3 cm
    LED menyala semua dan berkedip kedip selama 1 detik jika jarak melebihi dari 3 cm 
  Jawab : <br>
  Untuk pengerjaan kita modifikasi seperti dibawah berikut : <br>
  ```
    2cm = blue

    4cm = green

    6cm = red

    Diatas 6cm, red green dan blue delay 1 detik 
```
Source code : <br>
LED Blue menyala jika jarak yang terbaca 2 cm
<image src= "13.jpeg">
hasil output di rangkaian
<image src= "12.jpeg">

LED Green menyala jika jarak yang terbaca 4 cm
<image src= "15.jpeg">
hasil output di rangkaian
<image src= "14.jpeg">

LED Red menyala jika jarak yang terbaca 6 cm
<image src= "17.jpeg">
hasil output di rangkaian
<image src= "16.jpeg">

Diatas 6cm, red green dan blue delay 1 detik
<image src= "18.jpeg">
https://drive.google.com/file/d/15wpE5d-itpSiQPJHHHfsDa78gos9W1lq/view?usp=sharing

2. Upload hasilnya berupa file video menggunakan youtube atau google drive dan sisipkan linknya pada laporan Anda.
Link Google Drive :
https://drive.google.com/drive/folders/12b6LiKXxmYn3OkHlbmUI8ZWvD_eIShB5?hl=id

Link Github Source Code :
https://github.com/DiltaFebiana/Kelompok3_IoTLDR_P7.git