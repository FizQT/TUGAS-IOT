# Anggota Kelompok
1. Gustania Nirmala Meisi (10)
2. Rosis Hudaya Putra (16)
3. Safira Istifarini (17)

# Pertanyaan dan Jawaban
1.	Apa yang telah kelompok Anda lakukan pada pertemuan kali ini?
Bisa berisi potongan kode program atau output program, jelaskan maksud dari kode tersebut. Bisa berupa gambar, jika gambar silakan membuat folder<br>
Jawaban<br>
a.	Instalasi Arduino IDE
<br>
<img src = "kelompok04\arduino.png">
<img src = "kelompok04\arduino1.png">
<br>
b. Instalasi PlatformIO
<br>
<img src = "kelompok04\platformio.png">
<img src = "kelompok04\platformio1.jpeg">
<br>
c. Instalasi Fritzing
<br>
<img src="kelompok04\fritzing.jpeg">
<img src="kelompok04\fritzing1.jpeg">
<br>
d. Instalasi Wokwi
<br>
<img src="kelompok04\wokwi.jpeg">
<img src="kelompok04\wokwi1.jpeg">

<br>
2.	Apa ada kendala pada pertemuan kali ini, jika ada sebutkan!
Silakan sebutkan kendala, misalkan; terjadi error pada langkah, kemudian solusinya apa. <br>
Jawaban :<br>
Pada pertemuan kali ini, kelompok kami tidak mengalami kendala namun hanya mengalami terlalu melakukan instalasi IDE yang digunakan karena terkendala jaringan

<br>
3.	Apa yang bisa kelompok Anda simpulkan pada pertemuan kali ini! Kesimpulan kelompok Anda!
<br> 

* Mampu melakukan Instalasi & Konfigurasi software & Hardware pendukung
* Mampu menggunakan Arduino IDE, VS code platform io, dan Fritzing
* Dapat merangkai MCU dengan salah satu sensor
* Mampu membuat kode sederhana MCU dan Writing

<br>
4.	Silakan mengerjakan tugas yang terdapat di jobsheet!

Tugas

1. Buatlah sebuah skematik sederhana dari salah satu sensor atau aktuator yang telah kelompok Anda beli, boleh menggunakan Fritzing atau Wokwi.<br>
<img src = "kelompok04\skematik.jpeg">
2. Buatlah kode sederhana untuk menyalakan LED merah bawaan node MCU seperti pada gambar di bawah ini
```c
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);  // Mengatur pin built-in LED sebagai output
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // Menyalakan LED merah
  delay(1000);  // Menunggu selama 1 detik
  digitalWrite(LED_BUILTIN, LOW);  // Mematikan LED merah
  delay(1000);  // Menunggu selama 1 detik
}
```
<img src="kelompok04\simulasi.jpeg">
