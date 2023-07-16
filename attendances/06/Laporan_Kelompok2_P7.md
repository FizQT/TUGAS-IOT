## LAPORAN PRAKTIKUM MINGGU KE 6 <br> 
### KELOMPOK 2 : <br> 
1. Aida Millati Mardiana (03)
2. Daffa Aqila R (04)
3. Faiza Kurnia Putri (09) <br>

## Praktikum 1 - Membaca data intensitas cahaya 
Rangkaian yang digunakan : 
<img src="images/pict 1.jpeg">
<img src="images/pict 2.jpeg">
Link kode program praktikum 1 : https://github.com/AidaMillatiMardiana/IOT_KEL2_P7_1.git <br>
Hasil : 
<img src="images/pict 3.jpeg">

## Contoh menggunakan wokwi 
<img src="images/pict 4.jpeg">
Kode Program : <br>
<img src="images/pict 6.jpeg">
Hasil : 
<img src="images/pict 5.jpeg">

## Praktikum 2 - Membaca data jarak benda
Rangkaian yang digunakan :  
<img src="images/pict 7.jpeg">
Link kode program praktikum 2 : https://github.com/AidaMillatiMardiana/IOT_KEL2_P7_2.git <br>
Hasil : 
<img src="images/pict 8.jpeg">

## Contoh menggunakan wokwi 
<img src="images/pict 9.jpeg">
kode program : 
<img src="images/pict 11.jpeg">
Hasil : 
<img src="images/pict 10.jpeg">

## Tugas 
``` //Penggunaan sensor suhu LM35
#include "DHTesp.h"
const int DHT_PIN = 15;
DHTesp dhtSensor;
float suhu = 0;

//Penggunaan sensor cahaya LDR
#define cahayaPin 14
int cahaya = 0;

//Penggunaan sensor ultrasonik HC-SR04
#define trigPin 32
#define echoPin 33

//Penggunaan LED bawaan NodeMCU32
#define ledPin 2

//Penggunaan LED RGB tambahan
#define redPin 25
#define greenPin 26
#define bluePin 27

void setup()
{
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  Serial.begin(9600);
}

void loop()
{
  //Membaca nilai sensor suhu LM35
  TempAndHumidity data = dhtSensor.getTempAndHumidity();
  suhu = data.temperature;

  //Membaca nilai sensor cahaya LDR
  cahaya = analogRead(cahayaPin);

  //Membaca jarak dengan sensor ultrasonik HC-SR04
  long duration, jarak;
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  jarak = duration * 0.034 / 2;

  //Membuat kondisi untuk LED kuning
  if(cahaya < 1000 && suhu < 25 && jarak == 1){
    digitalWrite(bluePin, HIGH);
    delay(200);
    digitalWrite(bluePin, LOW);
    delay(200);
  }else{
    digitalWrite(redPin, HIGH);
  }

  //Membuat kondisi untuk LED RGB tambahan
  if(jarak == 1){ //Lampu kuning
    digitalWrite(greenPin, LOW);
    digitalWrite(redPin, LOW);
    digitalWrite(bluePin, HIGH);
  }
  else if(jarak == 2){ // Lampu magenta
    digitalWrite(bluePin, LOW);
    digitalWrite(redPin, LOW);
    digitalWrite(greenPin, HIGH);
  }
  else if(jarak == 3 || jarak == 4){ // Lampu biru muda
    digitalWrite(bluePin, LOW);
    digitalWrite(greenPin, LOW);
    digitalWrite(redPin, HIGH);
  }
  else{
    digitalWrite(redPin, LOW);
    digitalWrite(greenPin, LOW);
    digitalWrite(bluePin, LOW);
  }

//Membuat kondisi untuk LED berkedip jika jarak melebihi 3
if(jarak > 4){
digitalWrite(ledPin, HIGH);
delay(500);
digitalWrite(ledPin, LOW);
delay(500);
}

//Menampilkan nilai sensor suhu pada monitor serial
Serial.print("Suhu: ");
Serial.println(suhu);

//Menampilkan nilai sensor cahaya pada monitor serial
Serial.print("Cahaya: ");
Serial.println(cahaya);

//Menampilkan jarak dengan sensor ultrasonik pada monitor serial
Serial.print("Jarak: ");
Serial.println(jarak);

delay(1000);
}
```
Hasil : 
<img src="images/pict 12.jpeg">

