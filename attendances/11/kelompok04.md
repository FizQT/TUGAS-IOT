# <b>LAPORAN PRAKTIKUM  
# Anggota Kelompok
1. Gustania Nirmala Meisi (10)
2. Rosis Hudaya Putra (16)
3. Safira Istifarini (17)<br>

# <b>PRAKTIKUM PERTEMUAN 14

## <b>Praktikum 1 <br>
1. Silakan seret node inject ke worksheet, kemudian ubahlah nilai properties
2. Seret juga node function ke worksheet
3. Jangan lupa seret juga node mqtt out pada kategori network, tambahkan server broker agar bisa publish data dengan cara klik icon pensil.
4. Tambahkan node mqtt in ke worksheet
5. Tambahkan node terakhir yaitu node debug, sementara untuk kongifigurasinya tidak perlu disesuaikan. 
6. Verifikasi Hasil Percobaan
<img src = "kelompok04\prak1.PNG" width="500px">

## <b>Pertanyaan 1 <br>

1. Pada node inject, pada properties Repeat dengan nilai interval. Apakah fungsinya?<br>
2. Apakah yang dimaksud dengan baris kode msg.payload=Math.floor(Math.random()*100);?<br>
3. Bagian node mqtt out, apakah fungsi Qos dengan nilai 2?<br>

## <b>Jawaban 1 <br>

1. Pada node "inject", properti "Repeat" dengan nilai "interval" digunakan untuk mengatur interval waktu di antara pengiriman pesan yang diinjeksi.<br>
2. Baris kode ```msg.payload=Math.floor(Math.random()*100);``` digunakan untuk menghasilkan sebuah angka acak antara 0 dan 100, kemudian angka tersebut ditetapkan sebagai nilai untuk properti "payload" pada objek pesan ("msg"). 
3. Pada node "mqtt out", properti "Qos" (Quality of Service) dengan nilai 2 mengacu pada tingkat kualitas layanan yang digunakan saat mengirim pesan melalui protokol MQTT (Message Queuing Telemetry Transport). Nilai Qos 2 menunjukkan bahwa pesan dikirim dengan jaminan pengiriman paling akurat (Exact Once).

## <b>Praktikum 2 <br>
1. Silakan buat flow baru dengan cara klik tombol plus(+), tambahkan terlebih dahulu node mqtt in ke worksheet 
2. Buatlah dashboard dengan tab Site dengan title Node-RED Dashboard
3. Tambahkan node chart dan sesuaikan konfigurasinya 
4. 

Verifikasi Hasil Percobaan<br>
<img src = "kelompok04\prak2.jpeg" width="500px"><br>
<img src = "kelompok04\prak3.jpeg" width="500px">


## <b>Pertanyaan 2 <br>

1. Modifikasi program di ESP8266 di atas agar bisa melakukan subscribe dengan topik room/lamp?<br>
2. Tambahkan kode di atas agar bisa publish nilai kelembaban dengan topik room/humadity?<br>
3. Tambah node chart agar dapat menampilkan nilai kelembaban, node chart masih dalam satu group yaitu Room pada dashboard Node-RED.<br>

## <b>Jawaban 2 <br>

Hasilnya : 

1. ```cpp
   client.publish("kelompok4/lamp", temperatureTemp);
   ```
2. <br><img src = "kelompok04\prak4.jpeg" width="500px">


## <b>Tugas <br>

Masih lanjutan dengan tugas, tambahkan sensor LDR dan LED RGB pada ESP8266. Ketentuannya adalah sebagai berikut : 

1. Tab Home terdiri dari group Control, Monitoring, dan Cahaya.<br>
   - Group Control memiliki 3 node switch dan 3 text statis, fungsi dari group ini adalah untuk menghidupkan dan mematikan led RGB.<br>
   - Group Monitoring 2 node chart untuk menampilkan suhu dan kelembaban.<br>
   - Group Cahaya terdiri dari text dan gauge, text untuk menampilkan kategori terang, redup, dan gelap. Sedangkan node gauge untuk menampilkan nilai sensor LDR.<br>
2. Tab Contact Pada tab ini digunakan untuk menampilkan data kelas, NIM, dan Nama. Silakan diisi dengan nama Anda masing-masing.<br>

## <b>Hasil <br>

Video dokumentasi tugas [klik disini](https://drive.google.com/file/d/1QjFIUHo-r-LOkSajcPMNN1sXbPMuQtET/view?usp=sharing)