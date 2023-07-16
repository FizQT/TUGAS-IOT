## PRAKTIKUM IOT PERTEMUAN 11 TI-3G
### Kelompok 3 TI-3G:
Nama anggota : <br>
1. Dherisma Hanindita Utami (07)
2. Dilta Febiana (08)
3. Meliusa Nora Hariyanti (13)

## Installasi IoT Platform

Karena kelompok kami telah menginstall node.js maka langsung ke langkah seperti dibawah berikut:

    npm install -g --unsafe-perm node-red
<image src= "1.png">

lalu setelah itu melakukan installasi NODE-RED

    node-red

<image src= "2.png">

maka copy paste link url pada output setelah install tersebut yaitu :

    http://127.0.0.1:1880/
maka akan muncul halaman node-red
<image src= "3.png">

## 3. Menambahkan Keamanan pada Node-Red

Silakan edit file settings.js, file tersebut merupakan file konfigurasi Node-RED. Biasanya terletak pada home direktori installasi Node-RED. File tersebut terletak di 

    .node-red/settings.js
lalu buka file tersebut di Visual Studio Code 

<image src= "4.png">

Isikan username, password, dan permisi dari setiap user. Hanya terdapat 2 rule yang dapat digunakan yaitu full akses dan read. Yang membedakan 2 rule tersebut adalah read tidak bisa digunakan untuk menambahkan library atau pallete ataupun mengkonfigurasi node-read. Untuk membuat password silakan menggunakan perintah bawaan dari node-red seperti berikut :

    node-red admin hash-pw
<image src= "5.png">

setelah itu save di VS Code dan restart node-red
lalu login sesuai password yang telah diubah :

<image src= "6.jpeg">
tampilan setelah login 
<image src= "7.jpeg">

### Pertanyaan
1. Gantilah port bawaan Node-RED dan buktikan bahwa Node-RED bisa diakses dari public network? <br>
jawab : ganti port pada settings.js dengan port bebas disini kami menggunakan port 2002 
<image src= "8.jpeg">

2. Buktikan dengan tangkapan layar perbedaan antar permisi untuk user read dan full access?
<image src= "9.jpeg">

## 3 . Sample Node-Red
1. Drag sebuah pallete node inject pada kategori network ke worksheet, perhatikan gambar berikut ini
<image src= "10.png">
2. Selanjutnya double klik node inject yang terdapat pada worksheet sehingga menampilkan jendela properties seperti berikut.

    Ubah name menjadi make request dan hapus properti msg.payload serta msg.topic menggunakan icon cross, jika sudah jangan lupa klik tombol Done
<image src= "11.png">
3. Tambahkan juga node http request pada worksheet, sesuaikan properties pada nilai URL dan name. Isikan URL dengan https://raw.githubusercontent.com/prust/wikipedia-movie-data/master/movies.json dan sedangkan name diisi dengan movie request. Untuk lebih jelasnya dapat dilihat pada gambar berikut ini.
<image src= "13.png">
<image src= "12.png">

4. Hubungkan node make reqeust (inject) dan movie request (http request) dengan cara klik dan drag antar ujung node, hasilnya dapat dilihat pada gambar berikut ini.
<image src= "14.png">

5. Tambahkan node debug yang terdapat pada kategori common, jangan lupa diubah name dengan nama msg. Terakhir hubungkan node tersebut dengan node movie request. Hasil akhirnya adalah sebagai berikut
<image src= "15.png">
<image src= "16.png">

6. Langkah terakhir, silakan klik tombol Deploy yang terletak di pojok kanan atas sampai muncul popup successfully deployed. Jika sudah, klik make request dan amati hasilnya pada bagian debug (klik icon kutu) di jendela sebelah kanan. Untuk lebih jelasnya dapat dilihat pada gambar di bawah ini
<image src= "17.png">
<image src= "18.png">
<image src= "19.jpg">
<image src= "20.jpg">
<image src= "21.png">

## Pertanyaaan
1. Tambahkan kembali node function dan node debug, yang masing-masing fungsinya adalah untuk memfilter dimana movie yang akan tampil hanya movie dengan tahun > 2000 dan untuk menampilkan data filter tersebut.
<image src= "22.jpeg">
<image src= "23.jpeg">

2. Flow dan output pada debug dapat dilihat seperti berikut ini
<image src= "24.jpeg">

## TUGAS
Buatlah sebuah flow yang digunakan untuk menentukan sebuah kondisi temperatur dingin, normal, dan panas. Terdapat 3 node inject masing-masing sebagai berikut;

1. Ketika inject pertama diklik akan muncul di panel debug menampilkan dingin, lewatkan nilai 5 pada node inject pertama.

2. Ketika inject kedua diklik akan muncul di panel debug menampilkan normal, lewatkan nilai 25 pada node inject kedua.

3. Ketika inject ketiga diklik akan muncul di panel debug menampilkan panas, lewatkan nilai 50 pada node inject ketiga.

Perhatian keluaran pada panel debug di bawah ini, itu output yang diharapkan.

    jawaban :

desain 
<image src= "tugas1.jpeg">

di dalam node switch atau kondisinya
<image src= "tugas2.jpeg">

<image src= "tugas3.jpeg">
