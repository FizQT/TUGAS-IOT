# Anggota Kelompok

1. Ahmad Rafif Alaudin( 02 / 2041720230)
2. Raka Bagas Fitriansyah( 15 / 2041720187)
3. Thirsya Widya Sulaiman( 18 / 2041720233)

# PRAKTIKUM PEKAN KE-6

## Teori Singkat Sensor Suhu dan Kelembaban

Salah satu sensor diantara sensor-sensor yang lain adalah sensor suhu dan kelembaban. Sensor ini digunakan untuk mengambil data suhu pada lingkungan tertentu beserta tingkat kelembabannya. Salah satu sensor tersebut yang banyak digunakan adalah DHT11 karena secara biaya sangat minim serta mudah digunakan.
Jenis sensor lain yang memiliki fungsi yang sama adalah DHT22, yang membedakan dari tipe ini adalah keakuratan dalam mengambil data suhu dan kelembaban dan juga lama atau jeda dalam pengambilan sampling. DHT22 mengambil sampling setiap 2 detik, sedangkan DHT11 setiap 1 detik. Tentunya DHT22 lebih baik dibandingkan dengan versi terdahulunya, DHT11.

## Spesifikasi Sensor DHT 11

<table>
    <tr>
        <td>Nama</td>
        <td>Nilai</td>
    </tr>
    <tr>
        <td>Tegangan</td>
        <td>3, 5 V - 5,5 V </td>
    </tr>
    <tr>
        <td>Arus</td>
        <td>0,3 mA</td>
    </tr>
    <tr>
        <td>Jangkauan Suhu</td>
        <td>0 - 50 Celcius</td>
    </tr>
    <tr>
        <td>Jangkauan Kelembaban</td>
        <td>20% - 90%</td>
    </tr>
    <tr>
        <td>Akurasi Pengukuran</td>
        <td>+- 2 Celcius</td>
    </tr>
</table>

## Praktikum Project Wokwi

Pada project ini membuat sebuah rangkaian dengan menggunakan Wokwi. Rangkaian yang dibuat meliputi ESP32, Sensor DHT22 dan penyesuaian GPIO ketika program tersebut dijalankan. Ketika dijalankan akan menampilkan nilai Temp dan Humidity.

Hasil rangkaian

<img src="Kelompok 1/Rangkaian Wokwi.jpeg" width="500px">

Kode program yang digunakan :

```c++
#include "DHTesp.h"

const int DHT_PIN = 15;

DHTesp dhtSensor;

void setup() {
  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
}

void loop() {
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 2) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  delay(1000);
}

```

penjelasan code program

```c++
#include "DHTesp.h" 
```

Menggunakan Include DHTesp.h dari library wokwi untuk menggunakan library Sensor DHT

```c++
const int DHT_PIN = 15;
```

Mendefinisikan variabel integer bernama DHT_PIN yang mendefinisikan pin board nomer 15

```c++
DHTesp dhtSensor;
```

objek dhtSensor untuk membaca suhu dan kelembaban dari sensor

```c++
void setup() {
  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
}
```

dibagian setup berisikan Serial begin monitor 115200 dan inisialisasi sensor DHT22.

```c++
void loop() {
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 2) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  delay(1000);
}
```

Membuat TempAndHumidity data dengan berisi objek dhtSensor. Membuat serial yang berisikan temperature dan kelembapan.

Hasil ketika dijalankan :

<img src="Kelompok 1/Hasil Wokwi.jpeg" width="500px">

</br>

## Praktikum - Membaca data suhu dan kelembaban udara di NodeMCU

Pada praktikum ini melakukan percobaan untuk menangkap data suhu dan kelembaban udara dengan sensor DHT11. Source code untuk membaca suhu dan kelembaban udara menggunakan Visual Studio Code. Susunan rangkaiannya sebagai berikut

Hardware Preparation :

- NodeMCU x 1
- Sensor DHT11 x 1
- Kabel dupont
- Micro USB cable x 1
- Laptop x 1

Software Preparation :

- Visual Studio Code

Kode program :

```c++
#include <Arduino.h>
#include <SimpleDHT.h>


#define pinDHT 7 // SD3 pin signal sensor DHT


byte temperature = 0;
byte humidity = 0;


SimpleDHT11 dht11(D7); //instan sensor dht11


void KelembabanSuhu()
{
    int err = SimpleDHTErrSuccess;


    if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
    {
        Serial.print("Pembacaan DHT11 gagal, err=");
        Serial.println(err);
        delay(1000);
        return;
    }


    Serial.print("Sample OK: ");
    Serial.print((int)temperature);


    Serial.print(" *C, ");
    Serial.print((int)humidity);
    Serial.println(" H");


    delay(1500);
}


void setup()
{
    Serial.begin(115200);
    Serial.println("Simple DHT");
    delay(1000);
}


void loop()
{
    KelembabanSuhu();
}

```

Link Dokumentasi Project [klik disini](https://drive.google.com/file/d/1WD_lH3BvYTfR7i3X9tg8Wf1EzkTyCscK/view?usp=sharing)

## Kesimpulan Praktikum

Berdasarkan praktikum yang telah dilakukan, maka DHT11 merupakan sensor yang digunakan mendeteksi suhu dan kelembaban. Pada bagian suhu bisa dilihat dari output pada console, kemudian selain suhu juga dapat mendeteksi panas bisa dilihat pada index di console.

## TUGAS

1. Modifikasi baris kode pada bagian praktikum sehingga muncul data suhu dalam satuan Kelvin dan Reamur!

kode yang dimodifikasi pada fungsi kelembabanSuhu():

```c++
void KelembabanSuhu()
{
  int err = SimpleDHTErrSuccess;

  if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
  {
    Serial.print("Pembacaan DHT11 gagal, err=");
    Serial.println(err);
    delay(1000);
    return;
  }

  float celsius = (float)temperature;
  float fahrenheit = (celsius * 1.8) + 32;
  float reamur = celsius * 0.8;
  

  Serial.print("Sample OK: ");
  Serial.print("Suhu (C): ");
  Serial.print(celsius);
  Serial.print(" | Suhu (F): ");
  Serial.print(fahrenheit);
  Serial.print(" | Suhu (R): ");
  Serial.print(reamur);
  Serial.print("| H : ");
  Serial.println((int)humidity);

  delay(1500);
}
```

Video dokumentasi tugas nomor 1 [klik disini](https://drive.google.com/file/d/1cpCGdQoNXpYXWGqCLra6Rzpuj7M51dXy/view?usp=sharing)

2. Buatlah simulasi sebuah alat pembaca suhu dan kelembaban udara di tengah kota dengan memanfaatkan lampu LED sebagai indikator dengan disertai keterangan data suhu dan kelembaban yang ditampilkan pada serial monitor!

kode program :

```c++
#include <Arduino.h>
#include <SimpleDHT.h>

#define pinDHT 7 // SD3 pin signal sensor DHT

#define RED_LED D1   // led warna merah
#define GREEN_LED D2 // led warna hijau
#define BLUE_LED D3  // led warnah biru

byte temperature = 0;
byte humidity = 0;

SimpleDHT11 dht11(D7); // instan sensor dht11

void KelembabanSuhu()
{
  int err = SimpleDHTErrSuccess;

  if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
  {
    Serial.print("Pembacaan DHT11 gagal, err=");
    Serial.println(err);
    delay(1000);
    return;
  }

  float celsius = (float)temperature;
  float fahrenheit = (celsius * 1.8) + 32;
  float reamur = celsius * 0.8;
  String keterangan = "";

  // Dingin = 0 - 16 celcius | green
  // Normal = 17- 30 celcius | blue
  // Panas = 31 - 50 celcius | Red
  if (celsius >= 0 && celsius <= 16)
  {
    keterangan = " Dingin ";
    digitalWrite(RED_LED, LOW);
    digitalWrite(GREEN_LED, HIGH);
    digitalWrite(BLUE_LED, LOW);
  }
  else if (celsius > 16 && celsius <= 30)
  {
    keterangan = " Normal ";
    digitalWrite(RED_LED, LOW);
    digitalWrite(GREEN_LED, LOW);
    digitalWrite(BLUE_LED, HIGH);
  }
  else if (celsius > 30)
  {
    keterangan = " Panas ";
    digitalWrite(RED_LED, HIGH);
    digitalWrite(GREEN_LED, LOW);
    digitalWrite(BLUE_LED, LOW);
  }

  Serial.print("Suhu Sekarang : ");
  Serial.print(keterangan);
  Serial.print("Suhu (C): ");
  Serial.print(celsius);
  Serial.print(" | Suhu (F): ");
  Serial.print(fahrenheit);
  Serial.print(" | Suhu (R): ");
  Serial.print(reamur);
  Serial.print("| H : ");
  Serial.println((int)humidity);

  delay(1500);
}

void setup()
{
  Serial.begin(115200);
  Serial.println("Simple DHT");
  delay(1000);

  // atur pin-pin digital sebagai output
  pinMode(RED_LED, OUTPUT);
  pinMode(GREEN_LED, OUTPUT);
  pinMode(BLUE_LED, OUTPUT);
}

void loop()
{
  KelembabanSuhu();
}
```

Video dokumentasi hasil tugas [klik disini](https://drive.google.com/file/d/1n6AUCx9s_PjRXKEHgV9RzR-EXo3h-EdQ/view?usp=sharing)

3. Gambarkan skematik dari simulasi yang Anda buat.

<img src="Kelompok 1/DHT11_bb.png" width="500px">

4. Hasil dari simulasi tersebut silakan upload di youtube atau google drive dan urlnya disisipkan pada laporan Anda.

Link video hasil tugas: [https://drive.google.com/file/d/1n6AUCx9s_PjRXKEHgV9RzR-EXo3h-EdQ/view?usp=sharing](https://drive.google.com/file/d/1n6AUCx9s_PjRXKEHgV9RzR-EXo3h-EdQ/view?usp=sharing)
