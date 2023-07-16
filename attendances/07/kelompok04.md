# <b>LAPORAN PRAKTIKUM  
# Anggota Kelompok
1. Gustania Nirmala Meisi (10)
2. Rosis Hudaya Putra (16)
3. Safira Istifarini (17)<br>

# <b>Implementasi LCD I2C<b>

## <b>Teori Singkat
Berbagai jenis LCD bergantung dengan banyaknya karakter yang dapat ditampilkan, misalkan 16x2 ataupun 20x4. 16x2 artinya LCD tersebut mampu menampilkan sebanyak 32 karakter, dengan jumlah barisnya 2 dan jumlah kolomnya adalah 16. LCD merupakan sebuah jenis dari aktuator dan biasanya digunakan sebagai output atau tampilan dari sebuah nilai/data yang telah diolah dari sensor.

## <b>Praktikum 1 - Mencari alamat I2C
Untuk dapat menggunakan LCD yang menggunakan I2C, sebelumnya harus mencari terlebih dahulu lokasi dari I2C tersebut. I2C defaultnya terdapat di 0x27, akan tetapi hal tersebut bisa berbeda bergantung dari manufacture atau vendor. Buatlah kode di bawah ini untuk mendapatkan alamat I2C pada LCD.

Adapun langkah-langkahnya adalah sebagai berikut;

1. Buat project menggunakan visual studio code dengan PlatformIO dengan nama `IoT-08`
<img src = "kelompok04\nama_project.jpg" width="500px">

2. Tentukan board yang digunakan, dengan mengetik esp8266 kemudian pilih yang `Espressif ESP8266 EFSP-12E`
<img src = "kelompok04\esp.jpg" width="500px">

3. Untuk lokasi penyimpanan project disesuaikan dengan kebutuhan Anda.
4. Tunggu beberapa saat sampai dibuat struktur project oleh Visual Studio Code. Kemudian tambahkankan beberapa konfigurasi pada file platform.ini. Tambahkan kode `monitor_speed = 115200` untuk mengkonfigurasi serial console terkait baudrate.
<img src = "kelompok04\monitor_speed.jpg" width="500px">

5. Tambahkan potongan kode pada fungsi setup() seperti berikut ini

```cpp
 #include <Wire.h>
 void setup()
 {
 Wire.begin();
 Serial.begin(115200);
 Serial.println("\nI2C Scanner");
 }
 ```

 6. Pada fungsi loop() tambahkan juga kode seperti berikut

 ```cpp
   byte error, address;
   int nDevices;
   Serial.println("Scanning...");
   nDevices = 0;
   for(address = 1; address < 127; address++ ) {
     Wire.beginTransmission(address);
     error = Wire.endTransmission();
     if (error == 0) {
       Serial.print("I2C ditemukan pada 0x");
       if (address<16) {
         Serial.print("0");
       }
       Serial.println(address,HEX);
       nDevices++;
     }
     else if (error==4) {
       Serial.print("Unknow error at address 0x");
       if (address<16) {
         Serial.print("0");
       }
       Serial.println(address,HEX);
     }    
   }
   if (nDevices == 0) {
     Serial.println("No I2C devices found\n");
   }
   else {
     Serial.println("done\n");
   }
   delay(3000);
 ```

 7. Hasil dari percobaan
 <img src = "kelompok04\praktikum1.jpg" width="500px">

 8. Rangkaian WokWi
 <img src = "kelompok04\prak1.png" width="500px"><br>

 ## <b>Praktikum 2 - Menampilkan data pada LCD
 Pada praktikum ini kita akan mencoba menggunakan LCD untuk menampilkan sebuah text, hasil praktikum pertama akan kita gunakan pada praktikum ini. Silakan ikuti langkah-langkah berikut ini

1. Buat project menggunakan visual studio code dengan PlatformIO dengan nama `IoT-08`
<img src = "kelompok04\nama_project.jpg" width="500px">
<img src = "kelompok04\esp.jpg" width="500px">

2. Tambahkan library `LiquidCrystal_I2C` pada project Anda, untuk menambahkan library tersebut bisa melalui `platform.ini` atau menggunakan wizard/sistem menu pada PlatformIO seperti yang telah diajarkan pada praktikum yang sebelumnya.
<img src = "kelompok04\library.jpg" width="500px">

3. Tambahkan 2 baris kode sebelum fungsi `setup()` agar kita bisa memanfaatkan library yang telah kita tambahkan seperti di bawah ini
```cpp
 #include <LiquidCrystal_I2C.h>

 LiquidCrystal_I2C lcd(0x27, 16, 2);
```
4. Tambahkan kode pada fungsi `setup()` untuk memanggil berapa fungsi sebagai berikut
```cpp
   lcd.init(); // initialize the lcd
   lcd.backlight();
   lcd.clear();
   lcd.home();
```
5. Buatlah sebuah fungsi `scroolText(...)`, fungsi ini digunakan untuk melakukan scrolling text yang terdapat pada LCD agar lebih menarik.
```cpp
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
```
6. Tambahkan beberapa baris perintah pada fungsi `loop()`
```cpp
   lcd.home();
   lcd.print("Polinema");
   scrollText(1, "Kelas IoT.", 250, 16);
```
7. Hasil dari percobaan<br>
<img src = "kelompok04\praktikum2.jpeg" width="500px"><br>
Video dokumentasi hasil praktikum 2 [klik disini](https://drive.google.com/file/d/1IFhWSnD2Gh7hKtacud9M5WTjjlZhGRyR/view?usp=sharing)

8. Rangkaian WokWi<br>
Untuk dapat menggunakan wokwi, silakan disesuaikan untuk lokasi dari `SDA` dan `SCL`. Silakan menghubungkan `SDA` pada `pin 21`, sedangkan `SCL` pada `pin 22`. Jangan lupa menambahkan library `LiquidCrystal I2C`. <br>
<img src = "kelompok04\prak2.PNG" width="500px"><br>
<img src = "kelompok04\prak2hasil.PNG" width="500px"><br>

### <b>Pertanyaan dan Jawaban
1. Jelaskan fungsi dari pemanggilan method lcd.backlight()?<br>
Fungsi pemanggilan method lcd.backlight() adalah untuk mengontrol pencahayaan (backlight) pada LCD. Method ini biasanya digunakan pada saat pertama kali menginisialisasi layar LCD, agar layar dapat terlihat dengan jelas.<br>
Dalam pemrograman Arduino, lcd.backlight() digunakan untuk menghidupkan atau mematikan backlight pada layar LCD. Nilai parameter yang dimasukkan dalam method ini adalah nilai boolean true atau false, yang menunjukkan apakah backlight dihidupkan atau dimatikan.
2. Bagimana caranya mengganti tingkat intensitas kecerahan dari LCD Anda?<br>
Pada umumnya, kebanyakan modul LCD karakter tidak mendukung pengaturan tingkat kecerahan secara langsung melalui program. Namun, Anda bisa menggunakan potensiometer untuk mengatur kecerahan pada layar LCD dengan memutar potensiometer.
3. Silakan modifikasi data yang ditampilkan pada LCD Anda?<br>
Video dokumentasi jawaban pertanyaan praktikum 2 [klik disini](https://drive.google.com/file/d/1vS2YuFT_jl796q3_VPsKEokHWFfM9_nG/view?usp=share_link)
```cpp
void loop()
{
    lcd.home();
    lcd.print("Kelompok - 04");
    scrollText(1, "Gusta, Rosis, Safira", 250, 16);
}
```
<br>

 ## <b>Tugas</b><br>

Buatlah sebuah aplikasi yang sederhana menggunakan DHT11, LED RGB, dan LCD. Skenarionya adalah sebagai berikut

1. Buatlah ketiga komponen tersebut di dalam satu rangkaian menggunakan fritzing.
2. Tampilkan suhu dalam bentuk Fahrenheit dan Celcius, suhu yang ditampilkan adalah suhu di ruangan sekitar Anda.
3. Ketika suhu normal LED berwarna biru akan berkedip-kedip, ketika suhu dingin LED berwarna hijau akan berkedip, dan LED berwarna merah akan berkedip ketika suhu tergolong tinggi.
4. Tampilkan waktu saat ini juga pada LCD.
5. Silakan hasilnya diupload ke google drive ataupun youtube, linknya sertakan dalam laporan Anda.

 ## <b>Jawaban</b><br>

 1. Rancangan Wokwi<br>
 <img src = "kelompok04\tugas.PNG" width="500px"><br>

 2. Ketika suhu normal LED berwarna biru akan berkedip-kedip, ketika suhu dingin LED berwarna hijau akan berkedip, dan LED berwarna merah akan berkedip ketika suhu tergolong tinggi.<br>

    Suhu dingin : <br>
  <img src = "kelompok04\ijo.PNG" width="500px"><br>

    Suhu tinggi : <br>
<img src = "kelompok04\merah.PNG" width="500px"><br>
 
 3. Rancangan Kode Program<br>
 ```cpp
 #include <Arduino.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <SimpleDHT.h>
#define DEGREE_SYMBOL 0xDF

const int DHT_PIN = D3;
SimpleDHT11 dht(DHT_PIN);

const int BLUE_LED_PIN = D7;
const int GREEN_LED_PIN = D6;
const int RED_LED_PIN = D5;

LiquidCrystal_I2C lcd(0x27, 16, 2); // Alamat I2C untuk LCD

void setup()
{
    Serial.begin(115200);
    pinMode(BLUE_LED_PIN, OUTPUT);
    pinMode(GREEN_LED_PIN, OUTPUT);
    pinMode(RED_LED_PIN, OUTPUT);

    lcd.init();      // Inisialisasi LCD
    lcd.backlight(); // Hidupkan backlight
    lcd.setCursor(0, 0);
    lcd.print("");
}

void loop()
{
    byte temperature = 0;
    byte humidity = 0;
    int err = SimpleDHTErrSuccess;
    if ((err = dht.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
    {
        Serial.print("Gagal membaca dari sensor DHT11, kode error: ");
        Serial.println(err);
        return;
    }

    float temperatureF = temperature * 1.8 + 32;

    Serial.print(String(temperature, DEC) + "°C ");
    Serial.print(String(temperatureF, 1) + "°F ");

    lcd.setCursor(0, 0);
    lcd.print(String(temperature, DEC));
    lcd.write(DEGREE_SYMBOL);
    lcd.print("C ");
    lcd.print(String(temperatureF, 1));
    lcd.write(DEGREE_SYMBOL);
    lcd.print("F");

    lcd.setCursor(0, 1);
    lcd.print("04-04-2023 16.00");
    if (temperature >= 25)
    { // suhu tinggi, LED merah akan berkedip
        digitalWrite(BLUE_LED_PIN, LOW);
        digitalWrite(GREEN_LED_PIN, LOW);
        for (int i = 0; i < 5; i++)
        {
            digitalWrite(RED_LED_PIN, HIGH);
            delay(100);
            digitalWrite(RED_LED_PIN, LOW);
            delay(100);
        }
    }
    else if (temperature <= 20)
    { // suhu rendah, LED hijau akan berkedip
        digitalWrite(BLUE_LED_PIN, LOW);
        digitalWrite(RED_LED_PIN, LOW);
        for (int i = 0; i < 5; i++)
        {
            digitalWrite(GREEN_LED_PIN, HIGH);
            delay(100);
            digitalWrite(GREEN_LED_PIN, LOW);
            delay(100);
        }
    }
    else
    { // suhu normal, LED biru akan berkedip
        digitalWrite(GREEN_LED_PIN, LOW);
        digitalWrite(RED_LED_PIN, LOW);
        for (int i = 0; i < 5; i++)
        {
            digitalWrite(BLUE_LED_PIN, HIGH);
            delay(100);
            digitalWrite(BLUE_LED_PIN, LOW);
            delay(100);
        }
    }

    Serial.println("---");
    delay(1000);
}
 ```
 3. Video dokumentasi tugas [klik disini](https://drive.google.com/file/d/14zr-7tERx_NeYsxxI-VUZf6iCR2NkoXt/view?usp=sharing)
