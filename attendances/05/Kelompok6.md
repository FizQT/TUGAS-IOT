**PERTEMUAN 5**

Nama Kelompok : 
1. Ah Maulidi Rifki MD (01)
2. Dawam Ilhami Assidiqi (05)
3. Hafizh Izhar Darmansyah (11)
4. M. Fairuz Zakaria Firdaus (14)

**Praktikum**

1. Project 1: Running LED RGB
Kode Program :
```#include <Arduino.h>

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

## Dokumentasi Hasil
https://github.com/FizQT/testestes/assets/93257683/b3e082a7-c954-4dc0-9a50-85d22918a3bc


2. Project 2: SOS LED
Kode Program :
```
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

## Dokumentasi Hasil
https://github.com/FizQT/testestes/assets/93257683/dd801330-3f70-4c1d-8c93-328cfad56da3


**TUGAS**
Kode Program
```
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
https://github.com/FizQT/testestes/assets/93257683/dd801330-3f70-4c1d-8c93-328cfad56da3