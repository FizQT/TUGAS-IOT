# Anggota Kelompok
1. Dherisma Hanindita Utami (07)
2. Dilta Febiana (08)
3. Meliusa Nora Hariyanti (14)
 
# Pertanyaan
1. Apa yang telah kelompok Anda lakukan pada pertemuan kali ini?
    : Kelompok kami telah melakukan installasi dan konfigurasi aplikai arduino IDE dan mencoba menjalankan atau verify potongan kode program untuk mengecek error apa tidak serta menyambungkan port USB Node MCU dengan ESP8266 ke laptop. Lalu kami juga menginstall fritzing untuk mendesain yang digunakan oleh desainer, seniman, dan para penghobi elektronika untung perancangan berbagai peralatan elektronika.
    <!-- Bisa berisi potongan kode program atau output program, jelaskan maksud dari kode tersebut. Bisa berupa gambar, jika terdapat gambar silakan membuat folder yang berbeda dengan kelompok yang lain. -->
2. Apa ada kendala pada pertemuan kali ini, jika ada sebutkan!
    : Tidak ada kendala dalam praktikum saat ini
    
    <!-- Silakan sebutkan kendala, misalkan; terjadi error pada langkah, kemudian solusinya apa.  -->
3. Apa yang bisa kelompok Anda simpulkan pada pertemuan kali ini!
    :Dalam praktikum saat ini kami dapat melakukan instalasi dan konfigurasi software dan hardware, dapat menggunakan Arduino IDE, VS Code dan fritzing, kami juga dapat merangkai MCU dengan bebera sensor, dan akulator dan LCD dan kami dapat membuat kode sederhana MCU dan Writing

    <!-- Kesimpulan kelompok Anda! -->
4. Silakan mengerjakan tugas yang terdapat di jobsheet!


## TUGAS
1. Dari aktifitas hari ini, apakah yang telah kelompok Anda lakukan. sebutkan jika terjadi kendala dari aktifitas tersebut 
    : Kelompok kami telah melakukan installasi dan konfigurasi aplikai arduino IDE dan mencoba menjalankan atau verify potongan kode program untuk mengecek error apa tidak serta menyambungkan port USB Node MCU dengan ESP8266 ke laptop. Lalu kami juga menginstall fritzing untuk mendesain yang digunakan oleh desainer, seniman, dan para penghobi elektronika untung perancangan berbagai peralatan elektronika
    Tidak ada kendala yang terjadi pada praktikum saat ini
2. Buatlah sebuah skematik sederhana dari salah satu sensor atau aktuator yang telah kelompok Anda beli, boleh menggunakan Fritzing atau Wokwi.
    : 
```void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  Serial.println("Hello, ESP32!");
}

void loop() {
  // put your main code here, to run repeatedly:
  delay(10); // this speeds up the simulation
}
```

<br> <image src= "img_kelompok3/Kelompok3_Dherisma_Dilta_Meli.jpeg">


3. Buatlah kode sederhana untuk menyalakan LED merah bawaan node MCU seperti pada gambar di bawah ini


```void setup() {
  pinMode(LED_BUILTIN, OUTPUT); 
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // menyalakan LED merah
  delay(1000);                       // menunggu selama 1 detik
  digitalWrite(LED_BUILTIN, LOW);    // mematikan LED merah
  delay(1000);
}
```

<image src= "img_kelompok3/Kelompok3_Dherisma_Dilta_Meli_.jpeg">