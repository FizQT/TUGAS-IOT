# Anggota Kelompok

1. Ahmad Rafif Alaudin( 02 / 2041720230)
2. Raka Bagas Fitriansyah( 15 / 2041720187)
3. Thirsya Widya Sulaiman( 18 / 2041720233)

<br/>

# PRAKTIKUM PEKAN KE-13

<br/>

## Praktikum 1 - Install Dashboard Node-RED

Kami melakukan install node-RED dengan menggunakan menu Manage pallete pada Node-RED.

Langkah-Langkah sebagai berikut :

1. Mengakses  node-RED via browser

2. Klik button yang terdapat di pojok kanan atas dan cari menu Manage pallete

<img src="Kelompok 1/1.png" width="200px">

3. Pilih tab install dan ketik dashboard sehingga akan muncul modul-modul yang bisa di install dan klik tombol install.

<img src="Kelompok 1/2.png" width="500px">

4. Setelah muncul pop up notifikasi proses install seperti gambar di bawah ini, silakan pilih atau klik tombol install.

<img src="Kelompok 1/3.png" width="500px">

5. Komponen-komponen dashboard pada pallete sudah bertambah.

<img src="Kelompok 1/4.png" width="200px">

</br>
</br>

## Praktikum 2 - Membuat Dashboard Node-RED

Pada praktikum yang kedua akan dibuat sebuah tampilan seolah-olah menyalakan lampu dari internet, ikutilah langkah-langkah sebagai berikut :

1. erlebih dahulu pilih menu dashboard, yang terdapat di pojok kanan bawah. dashbaord ini adalah untuk mengkonfigurasi website yang akan kita buat misalkan dari sistem menu/hirarki menu ataupun title website.

<img src="Kelompok 1/5.png" width="500px">

<br/>

2. Pada bagian Tabs & Links klik tombol tab, lalu terbentuk yaitu Tab 1 klik tombol edit sehingga akan muncul jendela Edit

<img src="Kelompok 1/6.png" width="500px">

3. Tambahkan Group pada Tab Home tersebut dengan klik tombol group. Selanjutnya klik edit pada group yang baru ditambahkan

<img src="Kelompok 1/7.png" width="500px">

<br/>

4. Mengulangi langkah sebelumnya untuk membuat grup Output

<img src="Kelompok 1/9.png" width="200px">

5. Drag ke worksheet/flow node switch kemudian double klik

<img src="Kelompok 1/10.png" width="500px">

6. Ulangi langkah sebelumnya, tetapi yang ditambahkan adalah node text

<img src="Kelompok 1/11.png" width="500px">

7. Hubungkan node switch dan node text.

<img src="Kelompok 1/12.png" width="500px">

8. Hasilnya sebagai berikut dengan

<img src="Kelompok 1/13.png" width="500px">

<br>

#### Pertanyaan

1. Silakan modifikasi flow di atas sehingga ketika node switch digeser tidak menghasilkan nilai true atau false, tetapi ketika digeser nilainya adalah nyala atau mati. Perhatikan gambar berikut ini.

Jawab :

<img src="Kelompok 1/14.png" width="500px">

<img src="Kelompok 1/15.png" width="500px">

<img src="Kelompok 1/16.png" width="500px">

<br/>
<br/>
<br/>

# TUGAS

Buatlah sebuah dashboard website untuk memonitoring dan control pada sebuah ruang lobby, ruang kajur, dan ruang dosen. Masing-masing ruang dengan detail node yang dibutuhkan pada node dashboard sebagai berikut;

1. Tab Home memiliki group Lobby, Ruang Kajur, dan Ruang Dosen.

- Group Lobby terdapat 2 node inject, 2 function, gauge, dan chart.
- Group Ruang Kajur terdapat 2 node inject, 2 function, gauge, dan chart.
- Group Ruang Dosen terdapat 2 node inject, 2 function, gauge, dan chart.

>Jika diperhatikan node gauge dan chart bisa otomatis berjalan, hal tersebut diaktifkan saja pada bagian otomatis pada node inject.

> Sedangkan nilai yang selalu muncul acak itu menggunakan node funcion, Math.floor(Math.random()*101)

> Jumlah line antara node chart pada Lobby, Ruang Kajur, dan Ruang Dosen berbeda bisa dilakukan dengan cara mengubah `Setup Outputs` pada function.

2. Tab Room Control terdiri dari group Lampu dan AC.

- Group Lampu memiliki 3 switch, 3 function, dan 3 text.
- Group AC memiliki 3 slider dan 3 text.

>function digunakan untuk parsing boolean ke string, "nyala atau mati".

3. Tab About hanya terdiri dari text biasa.

### Jawaban

Berikut adalah dokumantasi hasil pengerjaan tugas pertemuan 13 :


https://github.com/AhmadRafif22/2023-iot-report-TI3G/assets/90122538/f65bf83b-2fe9-4bd9-823e-6b09dcac981b



