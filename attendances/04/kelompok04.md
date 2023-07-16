# LAPORAN PRAKTIKUM  
# Anggota Kelompok
1. Gustania Nirmala Meisi (10)
2. Rosis Hudaya Putra (16)
3. Safira Istifarini (17)<br>
## <b>Project Running LED RGB<b>
<br>

1. Silakan masuk ke Wokwi - Buat projeact baru - Pilih boardnya ESP32 

2. Rancangan Project Pada Wokwi 
 <br>
 <img src = "kelompok04\rancangan.jpeg"><br>

3. Kode Program  
```c
	#define RED_LED 21 //led warna merah 

#define GREEN_LED 19 //led warna hijau 

#define BLUE_LED 18 //led warnah biru 
 

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
<br>

4. Jika semua normal maka akan menampilkan seperti pada gambar berikut ini 
<br>
<img src = "kelompok04\LED-RGB.png">
<br>

5. Selanjutnya tuliskan kode program berikut pada Visual Studio Code <br>

```c
#include <Arduino.h> 

#define RED_LED D5 //led warna merah#define GREEN_LED D6 //led warna hijau 

#define BLUE_LED D7 //led warnah biru 
 
		void setup() { 

Serial.begin(115200); 

pinMode(RED_LED,OUTPUT);//atur pin-pin digital sebagai 	output 

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
<br>

Hasil : 

Video dokumentasi [klik disini](https://drive.google.com/file/d/12TufTwgGLgVcNdFyhvGa0y52HzSa0EHr/view?usp=sharing)
<br> 

### <b>SOS LED<b> <br><br>

1. Rancangan Project Pada Wokwi 
<br>
<img src="kelompok04\rancangan.jpeg"> 
<br>

2. Kode Program 
<br>

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
<br>
Hasil :
<br><br>
<video width="320" autoplay loop muted>
  <source src="kelompok04\SOS.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
<br>

## <b>KESIMPULAN <b>

Kesimpulan pada praktikum ini adalah kami mampu mengimplementasi Coding Running LED pada Visual Studio Code menggunakan PlatformIO, sebelum menjalankan kode program tersebut kami melakukan simulasi LED pada Wokwi terlebih dahulu agar tidak mengalami kesalahan dalam menyalakan LED. Karena dengan menjalankan kode program dan berhasil menyalakan lampu LED sesuai perintah maka kami mampu membedakan LED Anode dan Cathode <br><br>
## <b>TUGAS <b>

### <b>Soal <b>

1. Kembangkan praktikum ke-2(SOS) sehingga ada 3 LED yang digunakan yaitu merah, hijau dan biru. LED hijau menggunakan LED RGB, sedangkan untuk LED biru dan LED merah menggunakan LED yang terdapat pada ESP8266. Buatlah skematik(gambar pengkabelannya) dan kode programnya! 

2. Kumpulkan laporan dan tugas di LMS 

3. Sertakan juga dokumentasi link dalam bentuk video untuk masing-masing praktikum yang telah kelompok Anda lakukan. 

### <b>Jawaban <b>

1. Rancangan Wokwi <br><br>
<img src = "kelompok04\Tugas.jpeg">
<br>

2. Kode Program Tugas 
```c
#include <Arduino.h> 

#define GREEN_LED_R D5 // LED hijau – merah 

#define GREEN_LED_G D6 // LED hijau – hijau 

#define GREEN_LED_B D7 // LED hijau – biru 
 

void setup() 

{ 

 		Serial.begin(115200); 

pinMode(RED_LED, OUTPUT); 

  		pinMode(GREEN_LED_R, OUTPUT); 

  		pinMode(GREEN_LED_G, OUTPUT); 

  		pinMode(GREEN_LED_B, OUTPUT); 

  		pinMode(BLUE_LED, OUTPUT); 

  	Serial.println("Contoh Program LED SOS"); 

} 

void loop() 

{ 

  	// 3 dits (3 titik atau huruf S) 

  		for (int x = 0; x < 3; x++) 

  	{ 

    	digitalWrite(RED_LED, HIGH); 

    		delay(150); 

    	digitalWrite(RED_LED, LOW); 

    		delay(100); 

  	} 

  		delay(100); 

 

  	for (int x = 0; x < 3; x++) 

  	{ 

    	// blink green LED in RGB format 

    		analogWrite(GREEN_LED_R, 0);   // set red color to maximum 

    		analogWrite(GREEN_LED_G, 255); // set green color to minimum 

    		analogWrite(GREEN_LED_B, 0);   // set blue color to minimum 

    			delay(400); 

    		analogWrite(GREEN_LED_R, 0); // set red color to minimum 

    		analogWrite(GREEN_LED_G, 0); // set green color to minimum 

    		analogWrite(GREEN_LED_B, 0); // set blue color to minimum 

    			delay(100); 

  	} 

  	// 100ms delay to cause slight gap between letters 

  		delay(100); 
 

  	for (int x = 0; x < 3; x++) 

  	{ 

    		digitalWrite(BLUE_LED, HIGH); 

    			delay(150); 

    		digitalWrite(BLUE_LED, LOW); 

    			delay(100); 

  	} 

  		delay(100); 

  	for (int x = 0; x < 3; x++) 

  	{ 

    		digitalWrite(RED_LED, HIGH); 

    			delay(150); 

    		digitalWrite(RED_LED, LOW); 

    			delay(100); 

  	} 
 

  	// wait 5 seconds before repeating the SOS signal 

  	delay(3000); 

} 
```
<br>
Hasil :

Video dokumentasi Tugas [klik disini](https://drive.google.com/file/d/1ovgnk7X9tQAg2hkVSl2lvrxn0etdTEkI/view?usp=sharing)
 