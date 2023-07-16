# Anggota Kelompok

1. Ahmad Rafif Alaudin(02)
2. Raka Bagas Fitriansyah(15)
3. Thirsya Widya Sulaiman(18)

# Pertanyaan

1. Apa yang telah kelompok Anda lakukan pada pertemuan kali ini?

    <!-- Bisa berisi potongan kode program atau output program, jelaskan maksud dari kode tersebut. Bisa berupa gambar, jika terdapat gambar silakan membuat folder yang berbeda dengan kelompok yang lain. -->
2. Apa ada kendala pada pertemuan kali ini, jika ada sebutkan!

    <!-- Silakan sebutkan kendala, misalkan; terjadi error pada langkah, kemudian solusinya apa.  -->
3. Apa yang bisa kelompok Anda simpulkan pada pertemuan kali ini!

    <!-- Kesimpulan kelompok Anda! -->
4. Silakan mengerjakan tugas yang terdapat di jobsheet!

<br>

# Jawaban

## 1. Apa yang telah kelompok Anda lakukan pada pertemuan kali ini?

### Arduino IDE

Pada praktikum ini kelompok kami melakukan instalasi Arduino IDE. Disini kami menginstal Arduino IDE versi 2.0.4. Selanjutnya melakukan konfigurasi dengan memasukkan link yang telah tersedia di jobsheet pada file > Preferences. Langkah selanjutnya mencari esp8266 dan dilakukan instalasi. Selanjutnya memilih NodeMCU 1.0 (ESP-12E Module) pada Board Manager. Lalu memasukkan kabel data USB dari NodeMCU ke laptop dan tampil PORT COM6 pada device manager.

<img src="Kelompok 1/arduino1.png" style="width: 700px">

Membuka Arduino IDE dan memastikan boardnya NodeMCU 1.0 (ESP-12E Module) dan menyesuaikan port nya yaitu COM6. Lalu menjalankan aplikasi, dimana outputnya sebagai berikut

<img src="Kelompok 1/arduino2.png" style="width: 700px">

### Fritzing Designer

Pada praktikum kali ini kelompok kami juga melakukan instalasi Fritzing Designer. Untuk versi yang di install adalah versi Fritzing 0.9.3b (64-bit). Bentuk file yang didownload adalah bentuk zip. Untuk itu setelah di download file perlu diekstrak terlebih dahulu. Setelah diekstrak dilakukan proses instalasi programnya. Setelah berhasil maka akan menampilkan tampilan sebagai berikut,

<img src="Kelompok 1/fritzing0.png" style="width: 700px">

Untuk dapat membuat desain, klik menu file kemudian klik new

<img src="Kelompok 1/fritzing2.png">

Setelah itu akan terbuka file design baru, untuk dapat menambahkan item komponen yang ingin ditambahkan dapat dilakukan dengan cara drag and drop dari menu yang ada di sebelah kanan.

<img src="Kelompok 1/fritzing3.png" style="width: 700px">

Jika komponen yang diinginkan tidak tersedia, kita dapat mengimport nya dengan file berekstensi `.fzpz`. Klik icon yang berada di sebelah kanan search bar, kemudian klik import.

<img src="Kelompok 1/fritzing4.png">

Setelah itu pilih file yang ingin di import dalam direktori lokal kita.

<img src="Kelompok 1/fritzing5.png" style="width: 700px">

Setelah itu komponen yang kita inginkan dapat digunakan dengan menggunakan cara drag and drop

<img src="Kelompok 1/fritzing6.png" style="width: 700px">

### Platform IO

a. Buka aplikasi extensions dan install di VSCode

<img src="Kelompok 1/PlatformIO_1.jpeg">

b. Menunggu konfigurasi

<img src="Kelompok 1/PlatformIO_2.jpeg">

c. PlatformIO dapat terbuka

<img src="Kelompok 1/PlatformIO_3.jpeg">

### Wokwi

Buka aplikasi extensions wokwi di vs code untuk di install

<img src="Kelompok 1/Wikwok_1.jpeg">

Silakan lakukan installasi extension tersebut, kemudian masukkan Licence key dengan menekan tombol F1 dan pilih Wokwi: Manually Enter Licence Key.

<img src="Kelompok 1/Wikwok_2.jpeg">

Jika berhasil memasukkan lisensi , maka mencoba contoh koding untuk dicoba di wokwi

<img src="Kelompok 1/Wikwok_3.jpeg">

<br>

## 2. Apa ada kendala pada pertemuan kali ini, jika ada sebutkan

### Arduino IDE

Kendala yang kelompok kami alami pada saat melakukan instalasi Arduino IDE yaitu saat melakukan instalasi menggunakan versi 1.8.12 terdapat peringatan update. Solusi untuk mengatasi hal tersebut kami melakukan uninstall Arduino IDE 1.8.12 dan melakukan instalasi lagi dengan Arduino versi 2.0.4.  

### Fritzing Designer

Kendala yang kami alami pada saat melakukan instalasi Fritzing designer adalah aplikasinya yang berbayar, solusi dari permasalahan tersebut adalah mencari alternatif aplikasi yang gratis

<img src="Kelompok 1/fritzing1.png" style="width: 500px">

### PlatformIO

Kendala melakukan instalasi dikarenakan memori disk C sudah penuh dan melakukan pengosongan pada disk C.

### Wokwi

Terjadi error pada percobaan kode dikarenakan harus melakukan instalasi platformIO dan melakukan konfigurasi pada platformIO.

<br>

## 3. Apa yang bisa kelompok Anda simpulkan pada pertemuan kali ini

### Arduino IDE

Kesimpulan yang kami dapatkan pada Arduino IDE yaitu dapat melakukan compile dan run program setelah memasukkan USB dari NodeMCU dan mendapatkan PORT dan terhubung di device manager. Oleh karena itu, NodeMCU yang dihubungkan akan melakukan sesuai dengan code program.  

### Fritzing design

Kesimpulan yang kami dapatkan dalam tahap instalasi Fritzing design adalah bahwa tools ini merupakan tools yang dijalankan secara offline dan digunakan untuk mendesign skema. Jika terdapat komponen yang tidak tersedia di library fritzing design, kita dapat melakukan import komponen dengan ekstensi `.fzpz`.

### PlatformIO

Kesimpulan yang kami dapatkan dalam menggunakan platformIO adalah kemudahan fitur yang disediakan dan mudah diinstal di vscode. PlatformIO sendiri memiliki banyak pilihan dalam penggunaanya.  

### Wokwi

Kesimpulan yang kami dapatkan adalah terdapat untuk penulisan kode dengan simulasi hardware yang dapat disambungkan sebelum melakukan perancangan secara langsung.

### Kesimpulan lain

Kesimpulan yang kami dapatkan adalah dalam melakukan praktikum dan tugas, penggunaan software sangat penting untuk melakukan penulisan kode dan melakukan simulasi untuk melihat apakah kode yang digunakan sudah dilakukan dengan benar atau tidak.

<br>

## 4. Silakan mengerjakan tugas yang terdapat di jobsheet

1. Buatlah sebuah skematik sederhana dari salah satu sensor atau aktuator yang telah kelompok Anda beli, boleh menggunakan Fritzing atau Wokwi.

<b>Jawaban :</b>

<img src="Kelompok 1/tugas1.png">

Gambar diatas merupakan gambar skematik sederhana dari ESP32 + DHT22 Sensor. DHT22 Sensor adalah sensor yang dapat mengukur suhu dan juga kelembaban.  

2. Buatlah kode sederhana untuk menyalakan LED merah bawaan node MCU seperti pada gambar di bawah ini  :

Kodingan :

```C++
void setup() {
  Serial.begin(115200); // Inisialisasi komunikasi serial
  pinMode(LED_BUILTIN, OUTPUT); // Mengatur pin LED_BUILTIN sebagai OUTPUT
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH); // Menyalakan LED
  Serial.println("Lampu menyala!"); // Menampilkan pesan pada Serial Monitor
  delay(1000); // Menunggu 1 detik
  digitalWrite(LED_BUILTIN, LOW); // Mematikan LED
  Serial.println("Lampu padam!"); // Menampilkan pesan pada Serial Monitor
  delay(1000); // Menunggu 1 detik
}
```

Hasil :

<video width="320" autoplay loop muted>
  <source src="Kelompok 1/tugas2.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<https://user-images.githubusercontent.com/90122538/221874256-1e07dbc9-6dc1-4191-a728-6f67fca586e9.mp4>
