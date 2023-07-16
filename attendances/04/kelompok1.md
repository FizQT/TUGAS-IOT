# Anggota Kelompok

1. Ahmad Rafif Alaudin(02)
2. Raka Bagas Fitriansyah(15)
3. Thirsya Widya Sulaiman(18)

<br/>

# PRAKTIKUM PEKAN KE-5

## Project 1: Running LED RGB

Pada project ketiga ini akan dilakukan percobaan untuk menyalakan lebih dari satu LED secara teratur dan berurutan (running lED), siapkan beberapa komponen yang dibutuhkan dan rangkailah komponen tersebut pada project board.

Hardware Preparation:

- NodeMCU x 1
- LED RGB x 1
- 220 ohm resistor x 3, optional
- Kabel Dupont (male to male)
- Micro USB cable x 1
- PC/laptop x 1
- Software Visual Studio Code

kode Program yang digunakan :

```c
#include <Arduino.h>

#define RED_LED D5 //led warna merah
#define GREEN_LED D6 //led warna hijau
#define BLUE_LED D7 //led warnah biru

void setup() {
  Serial.begin(115200);
  pinMode(RED_LED,OUTPUT);//atur pin-pin digital sebagai output
  pinMode(GREEN_LED,OUTPUT);
  pinMode(BLUE_LED,OUTPUT);
  Serial.println("Contoh Program LED RGB");
}

void rgbLED(){
  digitalWrite(RED_LED, HIGH); 
  digitalWrite(GREEN_LED, LOW); 
  digitalWrite(BLUE_LED, LOW); 
  Serial.println("LED Merah nyala"); 
  delay(1000); 

  digitalWrite(RED_LED, LOW); 
  digitalWrite(GREEN_LED, HIGH); 
  digitalWrite(BLUE_LED, LOW); 
  Serial.println("LED Hijau nyala"); 
  delay(1000); 

  digitalWrite(RED_LED, LOW); 
  digitalWrite(GREEN_LED, LOW); 
  digitalWrite(BLUE_LED, HIGH); 
  Serial.println("LED Biru nyala"); 
  delay(1000);
}

void loop() {
  rgbLED();
}
```

- pada praktikum kelompok kami LED RGB yang digunakan adalah berjenis catode(-) sehingga menggunakan port Ground.

- berikut adalah dokumentasi hasil dari praktikum 1 :

### Tanpa Resistor



https://user-images.githubusercontent.com/90122538/225061924-ca941ec0-2cd7-4ac1-8fca-8f27c8bb05b1.mp4



### Dengan Resistor



https://user-images.githubusercontent.com/90122538/225058014-fb358745-b73a-422e-90b5-6f63db0d8e14.mp4



<br/>

## Project 1 : Run Wokwi on Visual Studio Code

- Silakan masuk ke Wokwi - Buat projeact baru - Pilih boardnya ESP32

<img src="Kelompok 1/wokwi1.png" width="500px">

- Buatlah sebuah rangkain seperti pada gambar berikut

<img src="Kelompok 1/wokwi2.png" width="500px">

<br/>

1. Sedangkan untuk kode program modifikasi sedikit untuk mendeklarasikan GPIO sehingga menjadi seperti berikut

```c
#define RED_LED 21 //led warna merah
#define GREEN_LED 19 //led warna hijau
#define BLUE_LED 18 //led warnah biru
```

2. Download project tersebut pada sub menu `Download project ZIP` di Wokwi. Setelah didownload terdapat file `wokwi-project.txt`, `file project dengan ekstensi *.ino`, dan`diagram.json`.

<img src="Kelompok 1/wokwi3.png" width="500px">

3. Buatlah project pada Visual Studio Code, jangan lupa memiliki boardnya `DOIT ESP32 DEVKIT V1`, copy file `*.ino` ke dalam folder src serta diagram.json pada direktori project VS Code

4. Buatlah file `wokwi.toml` yang berisi informasi lokasi hasil compile atau file binary pada direktori project VS Code, yang berisi seperti berikut

```toml
[wokwi]
version = 1
elf = ".pio/build/esp32doit-devkit-v1/firmware.elf"
firmware = ".pio/build/esp32doit-devkit-v1/firmware.bin"
```

Sehingga untuk struktur direktori lengkap seperti berikut

<img src="Kelompok 1/wokwi4.png" width="250px">

5. Silakan dijalankan dengan menekan tombol F1 dan pilih `Wokwi: Start Simulator`.

6. Jika semua normal maka akan menampilkan seperti pada Dokumentasi berikut ini



https://user-images.githubusercontent.com/90122538/225058360-c83a7647-1cf0-469f-ba3a-a5429798cdfc.mp4



<br/>

## Project 2: SOS LED

Pada project ketiga ini akan dilakukan percobaan untuk menyalakan lebih dari satu LED secara teratur sesuai sandi morse SOS, untuk komponen yang dibutuhkan dan rangkaian masih menggunakan komponen pada projek yang sebelumnya.

- Kode Program yang dipakai :

```c
#include <Arduino.h>

#define RED_LED D5   //led warna merah
#define GREEN_LED D6 //led warna hijau
#define BLUE_LED D7  //led warnah biru

void setup()
{
  Serial.begin(115200);
  pinMode(RED_LED, OUTPUT); //atur pin-pin digital sebagai output

  Serial.println("Contoh Program LED SOS");
}

void loop()
{
  // 3 dits (3 titik atau huruf S)
  for (int x = 0; x < 3; x++)
  {
    digitalWrite(RED_LED, HIGH); // LED nyala
    delay(150);                  // delay selama 150ms
    digitalWrite(RED_LED, LOW); // LED mati
    delay(100);                  // delay selama 100ms
  }
  delay(100);

  // 3 dahs (3 garis atau huruf O)
  for (int x = 0; x < 3; x++)
  {
    digitalWrite(RED_LED, HIGH); // LED nyala
    delay(400);                  // delay selama 400ms
    digitalWrite(RED_LED, LOW); // LED mati
    delay(100);                  // delay selama 100ms
  }

  // 100ms delay to cause slight gap between letters
  delay(100);
  // 3 dits again (3 titik atau huruf S)
  for (int x = 0; x < 3; x++)
  {
    digitalWrite(RED_LED, HIGH); // LED nyala
    delay(150);                  // delay selama 150ms
    digitalWrite(RED_LED, LOW); // LED mati
    delay(100);                  // delay selama 100ms
  }

  // wait 5 seconds before repeating the SOS signal
  delay(5000);
}
```

- Dokumentasi Hasil Praktikum 2 :



https://user-images.githubusercontent.com/90122538/225062430-cc191e91-b154-4be3-9230-a9ad89565466.mp4



<br/>

## Kesimpulan Praktikum

- Pengertian LED : sebuah akuator berbahan semikonduktor yang mengeluarkan cahaya ketika diberikan tegangan maju.
- LED RGB dibagi menjadi 2 jenis, catode(-) dan anode(+).
- pada LED RGB baik catode maupun anode berada pada pin yang paling panjang. berikut adalah ilustrasinya :
<img src="Kelompok 1/kesimpulan1.png" width="300px">

- untuk mengetahui jenis LED RGB dapat menggunakan Amperemeter dengan mengidentifikasi sumbernya pada pin terpanjang. LED catode akan menyala ketika sumber adalah ground, sedangkan LED anode akan menyala ketika sumbernya adalah tegangan.
- untuk dapat menjalankan wokwi pada visual studio code, hal yang perlu dilakukan adalah:

1. mendownload project wokwi dalam bentuk ZIP.
2. ekstrak file zip.
3. membuat project platformIO pada VSCODE, pilih board sesuai dengan yang dipakai di wokwi.
4. pindahkah file dengan ekstensi `*.ino` pada folder src dan pindahkan file `diagram.json` pada direktori root project
5. buat file `wokwi.toml` pada direktori root project kemudian masukan path untuk `firmware` dan `elf` nya.
6. build project
7. tekan f1 kemudian pilih `Wokwi: Start Simulator`

## Kendala Praktikum

- BREADBOARD nya yang agak error (sulit untuk terhubung), sehingga perlu beberapa kali pindah posisi agar bisa terhubung.

<br/>

<br/>

# TUGAS PEKAN KE-5

- Kembangkan praktikum ke-2(SOS) sehingga ada 3 LED yang digunakan yaitu merah, hijau dan biru. LED hijau menggunakan LED RGB, sedangkan untuk LED biru dan LED merah menggunakan LED yang terdapat pada ESP8266. Buatlah skematik(gambar pengkabelannya) dan kode programnya!
- Sertakan juga dokumentasi link dalam bentuk video untuk masing-masing praktikum yang telah kelompok Anda lakukan.

## Skema

skema dibuat dengan menggunakan fritzing, dengan mengimport telebih dahulu komponen ESP2688.

<img src="Kelompok 1/skema.png" width="350px">

## Kode Program

kode program dijalankan dengan menggunakan Arduino IDE.

```c
#include <Arduino.h>

#define RED_LED D0   // LED merah
#define GREEN_LED_R D5  // LED hijau - merah
#define GREEN_LED_G D6  // LED hijau - hijau
#define GREEN_LED_B D7  // LED hijau - biru
#define BLUE_LED D4  // LED biru

void setup() {
  Serial.begin(115200);
  pinMode(RED_LED, OUTPUT);
  pinMode(GREEN_LED_R, OUTPUT);
  pinMode(GREEN_LED_G, OUTPUT);
  pinMode(GREEN_LED_B, OUTPUT);
  pinMode(BLUE_LED, OUTPUT);
  Serial.println("Contoh Program LED SOS");
}

void loop() {
  // 3 dits (3 titik atau huruf S)
  for (int x = 0; x < 3; x++) {
    digitalWrite(RED_LED, HIGH);
    delay(150);
    digitalWrite(RED_LED, LOW);
    delay(100);
  }
  delay(100);

  for (int x = 0; x < 3; x++) {
    // blink green LED in RGB format
    analogWrite(GREEN_LED_R, 0); // set red color to maximum
    analogWrite(GREEN_LED_G, 255);   // set green color to minimum
    analogWrite(GREEN_LED_B, 0);   // set blue color to minimum
    delay(400);
    analogWrite(GREEN_LED_R, 0);   // set red color to minimum
    analogWrite(GREEN_LED_G, 0);   // set green color to minimum
    analogWrite(GREEN_LED_B, 0);   // set blue color to minimum
    delay(100);
  }

  // 100ms delay to cause slight gap between letters
  delay(100);

  for (int x = 0; x < 3; x++) {
    digitalWrite(BLUE_LED, HIGH);
    delay(150);
    digitalWrite(BLUE_LED, LOW);
    delay(100);
  }

  delay(100);

  for (int x = 0; x < 3; x++) {
    digitalWrite(RED_LED, HIGH);
    delay(150);
    digitalWrite(RED_LED, LOW);
    delay(100);
  }

  // wait 5 seconds before repeating the SOS signal
delay(5000);
}
```

## Dokumentasi Hasil


https://user-images.githubusercontent.com/90122538/225059022-04894a1c-ff2e-409e-9e84-356b75f6d5e2.mp4



