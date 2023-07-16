**PERTEMUAN 7**

Nama Kelompok : 
1. Ah Maulidi Rifki MD (01)
2. Dawam Ilhami Assidiqi (05)
3. Hafizh Izhar Darmansyah (11)
4. M. Fairuz Zakaria Firdaus (14)

**Praktikum**<br>

1. Praktikum 1 - Membaca data intensitas cahaya - WOKWI WEB<br>
Kode Program :
```
#define sensorLDR 34
int nilaiSensor;


void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  Serial.println("Contoh Penggunaan Sensor LDR");
  delay(3000);
}


void loop() {
  // put your main code here, to run repeatedly:
  nilaiSensor = analogRead(sensorLDR);
  Serial.print("Nilai Sensor : ");
  Serial.println(nilaiSensor);
  delay(1000);
}
```
Skema dan Hasil:<br>
<img src="Kelompok6/Skema Hasil.jpg" width="400px">
<br>

2. Praktikum 2 - Membaca data jarak benda - WOKWI WEB<br>
Kode Program :
```
#define triggerPin 32
#define echoPin 33

void setup() {
  // put your setup code here, to run once:
   Serial.begin (115200);
   pinMode(triggerPin, OUTPUT);
   pinMode(echoPin, INPUT);
   pinMode(BUILTIN_LED, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
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
<br>
Skema dan Hasil:<br>
<img src="Kelompok6/Skema Hasil 2.jpg" width="400px">
<br>

**TUGAS**<br>

Kode Program :<br>
```
#include <Arduino.h>
#include <SimpleDHT.h>

// esp LED
#define RED D1
#define BLUE D2

// LDR
#define sensorLDR A0
int nilaiSensor;

// DHT11
#define pinDHT 7
SimpleDHT11 dht11(D7);

byte temperature = 0;

void setup()
{
  Serial.begin(115200);
  pinMode(BLUE, OUTPUT);
  pinMode(RED, OUTPUT);
}

void cekDHT()
{
  // cek DHT11
  int err = SimpleDHTErrSuccess;

  if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
  {
    Serial.print("Pembacaan DHT11 gagal, err=");
    Serial.println(err);
    delay(1000);
    return;
  }
}

void loop()
{

  cekDHT();
  float celsius = (float)temperature;

  // mengambil data cahaya
  nilaiSensor = analogRead(sensorLDR);

  // print informasi sensor cahaya dan suhu
  Serial.print("Temp: ");
  Serial.print(celsius);
  Serial.println("°C");

  Serial.print("Nilai Sensor Cahaya : ");
  Serial.println(nilaiSensor);
  Serial.println("-------------------------");

  // - Ketika cahaya redup dan suhu kategori dingin maka LED warna biru akan berkedip-kedip.
  if (nilaiSensor >= 1000 && celsius <= 30)
  {
    for (int x = 0; x < 3; x++)
    {
      digitalWrite(BLUE, HIGH); // LED kondisi 1 nyala
      delay(1500);              // delay selama 150ms
      digitalWrite(BLUE, LOW);  // LED mati
      delay(1000);              // delay selama 100ms
    }
  }
  // - Ketika cahaya terang dan suhu tergolong tinggi, LED merah akan menyala.
  else if (nilaiSensor <= 1000 && celsius >= 30)
  {
    digitalWrite(RED, HIGH); // LED kondisi 2 dinyalakan
  }
  else
  {
    digitalWrite(RED, LOW);
    digitalWrite(BLUE, LOW);
  }
  delay(1000);
}
```

Hasil :<br>
<img src="Kelompok6/Skema Tugas.jpg" width="400px">