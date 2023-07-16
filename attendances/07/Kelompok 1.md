# Anggota Kelompok

1. Ahmad Rafif Alaudin( 02 / 2041720230)
2. Raka Bagas Fitriansyah( 15 / 2041720187)
3. Thirsya Widya Sulaiman( 18 / 2041720233)

<br/>

# PRAKTIKUM PEKAN KE-8

<br/>

## Praktikum 1 - Mencari alamat I2C

Pada praktikum 1 kami mencari alamat lokasi dari I2C. Walaupun I2C defaultnya terdapat di 0x27 akan tetapi hal tersebut bisa berbeda tergantung dari manufacture atau vendor.

Hardware Preparation :

- NodeMCU x 1
- LCD 16x2 x 1
- I2C x 1
- Kabel dupont x 4
- Micro USB cable x 1
- Laptop x 1

Software Preparation :

- Visual studio code (PlatformIO)

Rangkaian :

<img src="Kelompok 1/prak1.JPG" width="500px">

Kode Program :

```c++
#include <Arduino.h>
#include <Wire.h>

void setup()
{
  Wire.begin();
  Serial.begin(115200);
  Serial.println("\nI2C Scanner");
}

void loop()
{
  byte error, address;
  int nDevices;
  Serial.println("Scanning...");
  nDevices = 0;
  for (address = 1; address < 127; address++)
  {
    Wire.beginTransmission(address);
    error = Wire.endTransmission();
    if (error == 0)
    {
      Serial.print("I2C ditemukan pada 0x");
      if (address < 16)
      {
        Serial.print("0");
      }
      Serial.println(address, HEX);
      nDevices++;
    }
    else if (error == 4)
    {
      Serial.print("Unknow error at address 0x");
      if (address < 16)
      {
        Serial.print("0");
      }
      Serial.println(address, HEX);
    }
  }
  if (nDevices == 0)
  {
    Serial.println("No I2C devices found\n");
  }
  else
  {
    Serial.println("done\n");
  }
  delay(3000);
}

```

<b>Verifikasi Hasil Praktikum 1 (Hasil) :</b>

<img src="Kelompok 1/praktikum 1.JPG" width="200px">

<b>Keterangan Hasil</b> :

Dari hasil praktikum alamat dari I2C diketahui / ditemukan berada pada 0x27.

Video :



https://user-images.githubusercontent.com/90122538/229746306-60999fb8-6e89-4bca-b42a-3b5fdba13154.mp4



</br>
</br>

## Praktikum 2 - Menampilkan data pada LCD

Pada praktikum 2 kami mencoba menampilkan sebuah text dengan menggunakan LCD yang memakai alamat dari I2C (sesuai pada praktikum 1).

Hardware Preparation :

- NodeMCU x 1
- LCD 16x2 x 1
- I2C x 1
- Kabel dupont x 4
- Micro USB cable x 1
- Laptop x 1

Software Preparation :

- Visual studio code (PlatformIO)

Kode Program :

```c++
#include <Arduino.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup()
{
  lcd.init(); // initialize the lcd
  lcd.backlight();
  lcd.clear();
  lcd.home();
}

void scrollText(int row, String message, int delayTime, int lcdColumns)
{
  for (int i = 0; i < lcdColumns; i++)
  {
    message = " " + message;
  }
  message = message + " ";
  for (int pos = 0; pos < message.length(); pos++)
  {
    lcd.setCursor(0, row);
    lcd.print(message.substring(pos, pos + lcdColumns));
    delay(delayTime);
  }
}

void loop()
{
  lcd.home();
   lcd.print("Polinema");
   scrollText(1, "Kelas IoT.", 250, 16);
}
```

<b>Verifikasi Hasil Praktikum 2 (Hasil :)</b>

Video :



https://user-images.githubusercontent.com/90122538/229746447-1faab5e2-3890-4a05-a93b-38cc01672b47.mp4



<b>Keterangan Hasil</b> :

Dari hasil praktikum kami berhasil dalam menampilkan sebuah text “POLINEMA KELAS IOT” dengan menggunakan LCD.

## Menampilkan data pada LCD - Wokwi

kode Program :

```c++
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);


void setup() {
  lcd.init(); // initialize the lcd
  lcd.backlight();
  lcd.clear();
  lcd.home();
}

void scrollText(int row, String message, int delayTime, int lcdColumns)
 {
   for (int i = 0; i < lcdColumns; i++)
   {
     message = " " + message;
   }
   message = message + " ";
   for (int pos = 0; pos < message.length(); pos++)
   {
     lcd.setCursor(0, row);
     lcd.print(message.substring(pos, pos + lcdColumns));
     delay(delayTime);
   }
 }

void loop() {
  lcd.home();
  lcd.print("Polinema");
  scrollText(1, "Kelas IoT.", 250, 16);
}


```

hasil :

<img src="Kelompok 1/prak2.JPG" width="500px">

<br/>
<br/>

## Pertanyaan

1. Jelaskan fungsi dari pemanggilan method lcd.backlight()?

<b>jawab:</b>

Pemanggilan method lcd.backlight() berfungsi untuk menyalakan backlight. Sebab jumper backlight() digunakan untuk memilih apakah LED backlight (LED lampu latar LCD) menyala atau padam (opsional).

2. Bagaimana caranya mengganti tingkat intensitas kecerahan dari LCD Anda?

<b>jawab:</b>

Cara untuk mengganti tingkat intensitas kecerahan dari LCD dengan memutar bagian LCD contrast menggunakan obeng + kecil.

3. Silakan modifikasi data yang ditampilkan pada LCD Anda?

<b>jawab:</b>

Pada nomor 3 ini kami melakukan modifikasi data yang ditampilkan pada LCD menjadi “Assalamualaikum” pada baris pertama dan “Ta'aruf yuk.” pada baris kedua seperti video dibawah ini.

kode program yang diganti :

```c++
void loop() {
  lcd.home();
  lcd.print("Assalamualaikum"); 
  scrollText(1, "ta'aruf yuk.", 250, 16);
}
```

video output :


https://user-images.githubusercontent.com/90122538/229746555-6fb4bcc9-96be-4afd-b3ff-a1e99509d70b.mp4




## KESIMPULAN

Dari praktikum pekan 8 langkah awal dalam menggunakan I2C LCD harus melakukan pencarian alamat lokasi dari I2C terlebih dahulu dengan cara seperti pada praktikum 1. Setelah mendapatkan alamat dari I2C, maka memakai alamat I2C tersebut untuk menampilkan text.
Komponen I2C LCD dapat digabungkan dengan komponen yang lain. Dalam tugas kami menggabungkan LED, dan DHT11 yang menghasilkan output suhu dan waktu pada LED dan perubahan warna nyala LED.

<br/>
<br/>

# TUGAS

Buatlah sebuah aplikasi yang sederhana menggunakan DHT11, LED RGB, dan LCD. Skenarionya adalah sebagai berikut

1. Buatlah ketiga komponen tersebut di dalam satu rangkaian menggunakan fritzing.

- Rangkaian Fritzing

<img src="Kelompok 1/Tugas LCD_bb.png" width="500px">

- Rangkaian Wokwi

<img src="Kelompok 1/tugasw.jpeg" width="500px">

2. Tampilkan suhu dalam bentuk Fahrenheit dan Celcius, suhu yang ditampilkan adalah suhu di ruangan sekitar Anda.

3. Ketika suhu normal LED berwarna biru akan berkedip-kedip, ketika suhu dingin LED berwarna hijau akan berkedip, dan LED berwarna merah akan berkedip ketika suhu tergolong tinggi.

4. Tampilkan waktu saat ini juga pada LCD.

<b>jawaban nomor 2 - 4 :</b>

## Menggunakan PlatformIO

kode program

```c++
#include <Arduino.h>
#include <LiquidCrystal_I2C.h>
#include <SimpleDHT.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

#define pinDHT 7 // SD3 pin signal sensor DHT
#define RED D5
#define GREEN D6
#define BLUE D4

byte temperature = 0;
byte humidity = 0;

SimpleDHT11 dht11(D7); // instan sensor dht11

void setup()
{
  Serial.begin(115200);
  pinMode(BLUE, OUTPUT);
  pinMode(RED, OUTPUT);
  pinMode(GREEN, OUTPUT);
  lcd.init(); // initialize the lcd
  lcd.backlight();
  lcd.clear();
  lcd.home();
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
  float fahrenheit = (celsius * 1.8) + 32;

  lcd.home();

  lcd.print(String(celsius, 2)); // mencetak suhu dengan 2 digit di belakang koma
  lcd.write(byte(0xDF));         // menampilkan simbol derajat dengan karakter ASCII khusus
  lcd.print("C ");
  lcd.print(String(fahrenheit, 2)); // mencetak suhu dalam Fahrenheit
  lcd.write(byte(0xDF));            // menampilkan simbol derajat dengan karakter ASCII khusus
  lcd.print("F");
  lcd.setCursor(0, 1); // set cursor to column 0, row 1
  lcd.print("04-04-2023 14:03");

  // algotitma LED
  // ketika suhu normal 29C
  if (celsius == 30)
  {
    for (int x = 0; x < 3; x++)
    {
      digitalWrite(BLUE, HIGH);
      delay(500);
      digitalWrite(BLUE, LOW);
      delay(500);
    }
  }
  // ketika suhu panas >=30C
  else if (celsius >= 31)
  {
    digitalWrite(RED, HIGH);
    delay(500);
    digitalWrite(RED, LOW);
    delay(500);
  }
  // ketika suhu dingin <=28C
  else if (celsius <= 29)
  {
    digitalWrite(GREEN, HIGH);
    delay(500);
    digitalWrite(GREEN, LOW);
    delay(500);
  }
}
```

output video :


https://user-images.githubusercontent.com/90122538/229746650-7aef3aba-76a7-4f31-b4ec-501bf18aadaf.mp4




Penjelasan Kode Program:

- pertama perlu menginstall library SimpleDHT dan LiquidCrystal_I2C
- lalu definisikan pin data untuk LED dan DHT, serta instansiasi variabel untuk mengambil data temperature
- pada `setup()` define pin LED sebagai output serta fungsi-fungsi yang digunakan untuk LCD
- buat fungsi `cekDHT()` yang digunakan untuk melakukan pengecekan terhadap sensor DHT apakah berfungsi atau tidak
- kemudian pada fungsi `loop()` panggil fungsi `cekDHT()`, lalu instansiasikan variabel celcius dan fahrenheit
- kemudian tampilkan celcius dan fahrenheit pada LCD menggunakan fungsi `lcd.print()`. variabel terlebih dahulu perlu dikonversi menjadi string agar dapat tertampil pada LCD
- kemudian tulis kode program pemillihan nyala LED. dimana suhu normal ada pada 29 celcius, suhu dingin kurang sama dengan dari 28 celcius, serta suhu panas di lebih dari sama dengan 30 celcius.

</br>

## Menggunakan Wokwi

kode program

```c++
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);


void setup() {
  lcd.init(); // initialize the lcd
  lcd.backlight();
  lcd.clear();
  lcd.home();
}

void scrollText(int row, String message, int delayTime, int lcdColumns)
 {
   for (int i = 0; i < lcdColumns; i++)
   {
     message = " " + message;
   }
   message = message + " ";
   for (int pos = 0; pos < message.length(); pos++)
   {
     lcd.setCursor(0, row);
     lcd.print(message.substring(pos, pos + lcdColumns));
     delay(delayTime);
   }
 }

void loop() {
  lcd.home();
   lcd.print("Polinema");
   scrollText(1, "Kelas IoT.", 250, 16);
}

```

Hasil Output :

<img src="Kelompok 1/tugaswo.JPG" width="200px">

</br>
</br>

5. Silakan hasilnya diupload ke google drive ataupun youtube, linknya sertakan dalam laporan Anda.

- Praktikum 1
[https://drive.google.com/file/d/1ZHjRKk1a-hgjX7HOMONyDRp4ash45Kj5/view?usp=sharing](https://drive.google.com/file/d/1ZHjRKk1a-hgjX7HOMONyDRp4ash45Kj5/view?usp=sharing)

- Praktikum 2
[https://drive.google.com/file/d/148cHMKmqAw8aZXbhzwU4vwazL6nkiaRx/view?usp=sharing](https://drive.google.com/file/d/148cHMKmqAw8aZXbhzwU4vwazL6nkiaRx/view?usp=sharing)

- Pertanyaan Praktikum 2
[https://drive.google.com/file/d/1rmCW_HyoYnMata_de_Mi71hrA5Zeew9w/view?usp=sharing](https://drive.google.com/file/d/1rmCW_HyoYnMata_de_Mi71hrA5Zeew9w/view?usp=sharing)

- TUGAS
[https://drive.google.com/file/d/1y4zAuOVFAs6Qc1OVyaZqdqxHyxrvcIf6/view?usp=sharing](https://drive.google.com/file/d/1y4zAuOVFAs6Qc1OVyaZqdqxHyxrvcIf6/view?usp=sharing)
