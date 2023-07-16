# Anggota Kelompok

1. Ahmad Rafif Alaudin( 02 / 2041720230)
2. Raka Bagas Fitriansyah( 15 / 2041720187)
3. Thirsya Widya Sulaiman( 18 / 2041720233)

<br/>

# PRAKTIKUM PEKAN KE-7

<br/>

## Praktikum 1 - Membaca data intensitas cahaya

Pada praktikum 1 kami melakukan percobaan untuk menangkap data intensitas cahaya. Menggunakan sensor LDR.

Hardware Preparation :

- NodeMCU x 1
- Sensor LDR dengan bracket dan IC Comparator x 1
- Kabel dupont x 3
- Micro USB cable x 1
- Laptop x 1

Software Preparation :

- Visual studio code (PlatformIO)

Rangkaian :

<img src="Kelompok 1/ldr1.png" width="500px">

Kode Program :

```c++
#include <Arduino.h>
#define sensorLDR A0
int nilaiSensor;


void setup() {
  Serial.begin(115200);
  Serial.println("Contoh Penggunaan Sensor LDR");
  delay(3000);
}
void loop() {
  nilaiSensor = analogRead(sensorLDR);
  Serial.print("Nilai Sensor : ");
  Serial.println(nilaiSensor);
  delay(1000);
}

```

Hasil :

<img src="Kelompok 1/prak1.jpeg" width="200px">

<b>Keterangan Hasil</b> : Dari praktikum 1 menghasilkan nilai sensor yang jika banyak cahaya mengenai sensor LDR maka nilai resistansinya akan menurun, dan sebaliknya jika semakin sedikit cahaya yang mengenai LDR maka nilai akan semakin besar. Normalnya nilai yang ditampilkan 0-1024.

Video :



https://user-images.githubusercontent.com/90122538/228459866-3b152783-8af8-4cfb-b511-0daa8b5d1d39.mp4



### Contoh Menggunakan Wokwi (Sensor LDR)

kode program :

```c++
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

Hasil :

<img src="Kelompok 1/wokwiprak1.png" width="500px">

<br/>
<br/>

## Praktikum 2 - Membaca data jarak benda

Pada praktikum 2 kami melakukan percobaan untuk menerapkan atau mengimplementasikan pembacaan sensor ultrasonic untuk kemudian ditampilkan pada serial monitor yang ada pada PlatformIO.

Hardware Preparation :

- NodeMCU x 1
- Sensor Ultrasonik HC-SR04 x 1
- Kabel dupont x 4
- Micro USB cable x 1
- Laptop x 1

Software Preparation :

- Visual studio code (PlatformIO)

Rangkaian :

<img src="Kelompok 1/hc1.png" width="500px">

Kode Program :

```c++
#define triggerPin D6
#define echoPin D5


void setup() {
   Serial.begin (115200);
   pinMode(triggerPin, OUTPUT);
   pinMode(echoPin, INPUT);
   pinMode(BUILTIN_LED, OUTPUT);
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

<b>Keterangan Hasil</b> : Dari praktikum 2 menghasilkan nilai sensor yang didapat dari sensor yang mendeteksi suatu benda dengan jarak tertentu dalam satuan cm.

Video :



https://user-images.githubusercontent.com/90122538/228460013-a6850e6d-75ef-4289-a83e-d82dfb7b9ba2.mp4



### Contoh Menggunakan Wokwi (Sensor Ultrasonik)

kode Program :

```c++
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

hasil :

<img src="Kelompok 1/wokwiprak2.png" width="500px">

<br/>
<br/>

## KESIMPULAN

- Sensor LDR digunakan sebagai sensor cahaya, dimana jika semakin banyak cahaya yang mengenainya, maka akan semakin menurun nilai resistansinya. Sebaliknya jika semakin sedikit cahaya yang mengenai sensor (gelap), maka nilai hambatannya akan menjadi semakin besar sehingga arus listrik yang mengalir akan terhambat. Sensor LDR dihubungkan ke pin analog A0 dari NodeMCU. Pin A0 menghasilkan nilai luaran analog dengan rentang antara 0 sampai 1023.

- Sensor Ultrasonic digunakan untuk mendeteksi suatu benda dengan jarak tertentu berdasarkan perhitungan dari pantulan suatu gelombang ultrasonik sehingga jarak suatu benda dapat diketahui. Pada sensor ultrasonik memiliki pin Trigger, dimana pin ini berfungsi sebagai pengirim sinyal dan pin Echo yang berfungsi sebagai penerima sinyal yang didapat dari pantulan benda.

<br/>
<br/>

# TUGAS

1. Buatlah sebuah rangkaian untuk LED, sensor cahaya dan sensor suhu menggunakan fritzing, kemudian buatlah program dengan skenario sebagai berikut.

### Bagian 1

- Ketika cahaya redup dan suhu kategori dingin maka LED warna biru akan berkedip-kedip.
- Ketika cahaya terang dan suhu tergolong tinggi, LED merah akan menyala.
Buatlah rangkaian dan kode programnya dimana:

Gambar Rangkaian :

<img src="Kelompok 1/tugas1_bb.png" width="500px">

Kode Program :

```c++
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

Hasil :



https://user-images.githubusercontent.com/90122538/228460157-3355ce1c-037e-400d-98c0-793384c023b4.mp4



### Bagian 2

- Terdapat tambahan 1 LED RGB,
- LED Blue menyala jika jarak yang terbaca 1 cm
- LED Green menyala jika jarak yang terbaca 2 cm
- LED Red menyala jika jarak yang terbaca 3 cm
- LED menyala semua dan berkedip kedip selama 1 detik jika jarak melebihi dari 3 cm

Gambar Rangkaian :

<img src="Kelompok 1/tugas2_bb.png" width="500px">

Kode Program :

```c++
#include <Arduino.h>

// esp LED
#define RED D1
#define GREEN D2
#define BLUE D3

// ultrasonic
#define triggerPin D6
#define echoPin D5

void setup()
{
  Serial.begin(115200);
  pinMode(triggerPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(BLUE, OUTPUT);
  pinMode(GREEN, OUTPUT);
  pinMode(RED, OUTPUT);
}

void loop()
{
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

  if (jarak == 11)
  {
    digitalWrite(BLUE, HIGH);
  }
  else if (jarak == 12)
  {
    digitalWrite(GREEN, HIGH);
  }
  else if (jarak == 13)
  {
    digitalWrite(RED, HIGH);
  }
  else if (jarak > 13)
  {
    for (int x = 0; x < 3; x++)
    {
      digitalWrite(RED, HIGH);
      digitalWrite(GREEN, HIGH);
      digitalWrite(BLUE, HIGH);
      delay(1000);
      digitalWrite(RED, LOW);
      digitalWrite(GREEN, LOW);
      digitalWrite(BLUE, LOW);
      delay(1000);
    }
  }
  delay(500);
}
```

Hasil :


https://user-images.githubusercontent.com/90122538/228460764-ef129d38-2582-44de-afcb-8da6fc6e85d5.mp4



2. Upload hasilnya berupa file video menggunakan youtube atau google drive dan sisipkan linknya pada laporan Anda.

- Link Video Tugas Bagian 1 : 

[https://drive.google.com/file/d/1pv_ataU8T-7d8nxFh9ZW-8xSFdr3Mu5A/view?usp=sharing](https://drive.google.com/file/d/1pv_ataU8T-7d8nxFh9ZW-8xSFdr3Mu5A/view?usp=sharing)

- Link Video Tugas Bagian 2 : 

[https://drive.google.com/file/d/1zlq4CFEHOzt_g2tyqMK3NYBu7t2M734j/view?usp=sharing](https://drive.google.com/file/d/1zlq4CFEHOzt_g2tyqMK3NYBu7t2M734j/view?usp=sharing)
