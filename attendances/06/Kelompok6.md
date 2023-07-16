**PERTEMUAN 6**

Nama Kelompok : 
1. Ah Maulidi Rifki MD (01)
2. Dawam Ilhami Assidiqi (05)
3. Hafizh Izhar Darmansyah (11)
4. M. Fairuz Zakaria Firdaus (14)

**Praktikum**<br>
Kode Program :
```
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

<img src="Kelompok6/DHT11.jpeg" width="400px">

**KESIMPULAN**<br>

-	Kesimpulan yang didapat setelah melakukan praktikum kelompok kami telah mengetahui cara kerja sensor DHT11. 
-	Cara kerja DHT11, DHT11 adalah sebuah sensor yang mana memiliki sebuah sensor suhu resistansi. Ketika suhu berubah, resistansi sensor suhu juga berubah, sehingga arus listrik yang mengalir melalui sensor juga berubah. Nilai suhu kemudian dapat dihitung berdasarkan perubahan resistansi yang terjadi.
-	Dan DHT11 juga memiliki sebuah sensor kelembapan kapastitif, yang mengukur perubahan kapasitansi pada elemen kapasitor di dalam sensor. Kapasitansi ini dipengaruhi oleh jumlah uap air dalam lingkungan sekitar sensor. Semakin banyak uap air, semakin tinggi kapasitansi dan semakin rendah resistansi yang terukur. Nilai kelembaban kemudian dapat dihitung berdasarkan perubahan kapasitansi yang terjadi.
-	Sensor DHT11 mengirimkan sinyal digital ke mikrokontroler, berupa data suhu dan kelembaban dalam bentuk sinyal pulsa dengan lebar pulsa yang bervariasi sesuai dengan nilai suhu dan kelembaban yang terukur. Sinyal pulsa ini kemudian diterjemahkan oleh mikrokontroler untuk mendapatkan nilai suhu dan kelembaban yang akurat.
-	Kelompok kami juga telah mengetahui cara kerja analogRead. analogRead() adalah fungsi pada platform mikrokontroler Arduino yang digunakan untuk membaca nilai tegangan analog dari suatu pin input pada mikrokontroler.
-	Cara kerja analogRead menggunakan converter analog ke digital (ADC) untuk mengubah nilai tegangan analog menjadi nilai digital yang dapat diolah oleh mikrokontroler. Jadi Ketika fungsi analogRead() dipanggil pada program Arduino, mikrokontroler memilih pin input yang akan dibaca dan mengukur tegangan analog pada pin tersebut.
-	Dalam penggunaan analogRead(), juga perlu diperhatikan bahwa tegangan input harus sesuai dengan rentang tegangan yang dapat diukur oleh ADC pada Arduino, yaitu 0 hingga 5 volt. Juga, nilai yang diter

**TUGAS**<br>

1.	Modifikasi baris kode pada bagian praktikum sehingga muncul data suhu dalam satuan Kelvin dan Reaumur!
```
#include <Arduino.h>
#include <SimpleDHT.h>

#define pinDHT 5 // SD3 pin signal sensor DHT

byte temperature = 0;
byte humidity = 0;

SimpleDHT11 dht11(D5); //instan sensor dht11

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

    // Convert temperature to Kelvin
    float temperatureK = (float)temperature + 273.15;
    Serial.print(" Kelvin, ");

    // …
    delay(1500);
}

void setup()
{
    pinMode(RED_PIN, OUTPUT);
    pinMode(GREEN_PIN, OUTPUT);
    pinMode(BLUE_PIN, OUTPUT);

    
    Serial.begin(115200);
    Serial.println("Simple DHT");
    delay(1000);
}

void loop()
{
    KelembabanSuhu();
}
```
2. Skema <br>
<img src="Kelompok6/Skema Tugas.jpg" width="400px">

3. Hasil<br>
Link video :
https://drive.google.com/file/d/1h03_YnQT-We-b8mYA2plPnZ0U-gtxVMA/view?usp=sharing