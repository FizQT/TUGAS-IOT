**PERTEMUAN 3**

Nama Kelompok : 
1. Ah Maulidi Rifki MD (01)
2. Dawam Ilhami Assidiqi (05)
3. Hafizh Izhar Darmansyah (11)
4. M. Fairuz Zakaria Firdaus (14)

**PRAKTIKUM**

1. Install Arduino IDE
<img src="Kelompok6/Install Arduino.png" width="400px">

2. Install Fritzing Designer
<img src="Kelompok6/Install Fritzing.png" width="400px">

3. Install Platform IO - Visual Studio Code
<img src="Kelompok6/Install PlatformIO.png" width="400px">

4. Install Wokwi - Visual Studio Code
<img src="Kelompok6/Install Wokwi.png" width="400px">

5. Install Wokwi Website - Visual Studio Code
<img src="Kelompok6/Install Wokwi Website.png" width="400px">


**TUGAS**

1. Dari aktifitas hari ini, apakah yang telah kelompok Anda lakukan. sebutkan jika terjadi kendala dari aktifitas tersebut
Jawab : Melakukan instalasi Arduino dan konfigurasi beberapa aplikasi yang dibutuhkan

2.	Buatlah sebuah skematik sederhana dari salah satu sensor atau aktuator yang telah kelompok Anda beli, boleh menggunakan Fritzing atau Wokwi.
Jawab : 
<img src="Kelompok6/Install Wokwi Website.png" width="400px">

3.	Buatlah kode sederhana untuk menyalakan LED merah bawaan node MCU seperti pada gambar di bawah ini 
    Jawab : 
    ```void setup() {
    // put your setup code here, to run once:
    pinMode(LED_BUILTIN, OUTPUT);
    }

    void loop() {
    // put your main code here, to run repeatedly:
    digitalWrite(LED_BUILTIN, HIGH);   // menyalakan LED merah
    delay(1000);                       // menunggu selama 1 detik
    digitalWrite(LED_BUILTIN, LOW);    // mematikan LED merah
    }```
<img src="Kelompok6/Node MCU.jpeg" width="400px">