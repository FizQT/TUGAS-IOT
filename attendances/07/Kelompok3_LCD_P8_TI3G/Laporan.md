## PRAKTIKUM IOT PERTEMUAN 8 TI-3G
### Kelompok 3 TI-3G:
Nama anggota : <br>
1. Dherisma Hanindita Utami (07)
2. Dilta Febiana (08)
3. Meliusa Nora Hariyanti (13)

### PRAKTIKUM 1 - Mencari alamat I2C
Kode Program Seperti Berikut :
```
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
Output program :

<image src= "1.jpg">

rangkaian alatnya :
<image src= "2.jpg">

### PRAKTIKUM 2 - Menampilkan data pada LCD
Source code :
```
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

void scrollText(int row, String message, const int delayTime, const int lcdColumns)
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
Hasil Output di rangkaian alat :
<image src= "3.jpg">

### PERTANYAAN 
1. Jelaskan fungsi dari pemanggilan method lcd.backlight()?
jawab : lcd.backlight() adalah metode yang digunakan untuk mengontrol lampu latar (backlight) pada modul LCD. Modul LCD biasanya dilengkapi dengan lampu latar yang memungkinkan karakter atau tampilan yang ditampilkan pada layar dapat dilihat dengan jelas bahkan dalam kondisi pencahayaan yang rendah.
Metode lcd.backlight() digunakan untuk menghidupkan atau mematikan lampu latar pada modul LCD. Metode ini menerima satu parameter, yaitu status yang dapat diisi dengan nilai 0 untuk mematikan lampu latar dan 1 untuk menghidupkan lampu latar.
2. Bagimana caranya mengganti tingkat intensitas kecerahan dari LCD Anda?
jawab : Untuk mengganti tingkat intensitas kecerahan (brightness) dari modul LCD, Anda dapat menggunakan metode lcd.set_backlight() yang tersedia pada beberapa library modul LCD, seperti adafruit_character_lcd, pylcdsys, atau library lainnya.
Metode lcd.set_backlight() menerima satu parameter yaitu brightness yang dapat diisi dengan nilai antara 0 hingga 1. 
3. Silakan modifikasi data yang ditampilkan pada LCD Anda?
jawab : 
<image src= "4.jpg">
<image src= "5.jpg">

### Menampilkan data pada LCD - WOKWI
```
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

void scrollText(int row, String message, const int delayTime, const int lcdColumns)
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
Output pada Wokwi

<image src= "6.jpg">

## TUGAS
Buatlah sebuah aplikasi yang sederhana menggunakan DHT11, LED RGB, dan LCD. Skenarionya adalah sebagai berikut

1. Buatlah ketiga komponen tersebut di dalam satu rangkaian menggunakan fritzing.
2. Tampilkan suhu dalam bentuk Fahrenheit dan Celcius, suhu yang ditampilkan adalah suhu di ruangan sekitar Anda
jawab :
```
#include <Arduino.h>
#include <SimpleDHT.h>

#define pinDHT 7 // SD3 pin signal sensor DHT

byte temperature = 0;
byte humidity = 0;

SimpleDHT11 dht11(D2); // instan sensor dht11

int nilaiSensor;
// Deklarasi pin untuk setiap LED
#define pinDHT 7 // SD3 pin signal sensor DHT

void setup()
{
  Serial.begin(115200);
  Serial.println("Tugas Kelompok 3");
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

  Serial.print("Sample OK: ");
  Serial.print((int)temperature);
  Serial.print(" *C, ");

  float fahrenheit = temperature * 1.8 + 32.0;

  Serial.print((int)fahrenheit);
  Serial.print(" *F");
  Serial.println();
  delay(1500);
}
```

Output :<br>
<image src= "7.jpg">

3. Ketika suhu normal LED berwarna biru akan berkedip-kedip, ketika suhu dingin LED berwarna hijau akan berkedip, dan LED berwarna merah akan berkedip ketika suhu tergolong tinggi.
4. Tampilkan waktu saat ini juga pada LCD.
5. Silakan hasilnya diupload ke google drive ataupun youtube, linknya sertakan dalam laporan Anda.