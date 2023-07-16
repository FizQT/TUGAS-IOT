# Anggota Kelompok

1. Ahmad Rafif Alaudin( 02 / 2041720230)
2. Raka Bagas Fitriansyah( 15 / 2041720187)
3. Thirsya Widya Sulaiman( 18 / 2041720233)

<br/>

# PRAKTIKUM PEKAN KE-11

<br/>

## Praktikum 1 - Instalasi Node-RED

1. Memastikan Node.js dan npm terinstall (versi direkomendasikan node.js: v18.15.0 atau di atasnya dan npm 9.5.0 atau di atasnya), tetapi dengan menggunakan versi node.js dan npm dibawah yang direkomendasikan tidak terdapat masalah.

<img src="Kelompok 1/install1.png" width="500px">

2. Mengetikkan perintah `npm install -g --unsafe-perm node-red`

<img src="Kelompok 1/install2.png" width="500px">

3. Menjalankan node-RED dengan mengetikkan `node-red`

<img src="Kelompok 1/install3.png" width="500px">

4. Mengakses alamat sehingga akan muncul tampilan node-RED Alamat yang diakses sebagai berikut

<img src="Kelompok 1/install4.png" width="500px">

5. Hasil dari mengakses alamat berhasil dilakukan, sehingga muncul tampilan node-RED

<img src="Kelompok 1/install5.png" width="600px">

</br>
</br>

## Praktikum 2 - Menambahkan Keamanan pada Node-RED

Menambahkan keamanan pada Node-RED digunakan untuk membatasi setiap user ketika akan mengakses Node-RED, contohnya dengan cara memberikan user password ataupun mengganti protokol https pada halaman Node-RED, berikut ini cara yang dilakukan untuk menambahkan user dan password pada Node-RED yang telah kita install.

1. Membuka file settings.js yang terletak pada `.node-red/settings.js`

<img src="Kelompok 1/security1.png" width="500px">

<br/>

2. Mengedit file settings.js menjadi seperti gambar dibawah ini :

<img src="Kelompok 1/security2.png" width="500px">

Pada node-RED hanya dapat menggunakan 2 role saja yaitu admin (full access) dan user (read / tidak bisa digunakan untuk menambahkan library atau pallete ataupun mengkonfigurasi node-read ).

- Untuk membuat password menggunakan perintah bawaan dari node-red yaitu `node-red admin hash-pw`.

  <img src="Kelompok 1/security3.png" width="500px">

3. Menjalankan kembali node-RED dengan mengetikkan `node-red`, sehingga menghasilkan tampilan sebagai berikut

<img src="Kelompok 1/security4.png" width="500px">

<br/>

#### Pertanyaan

1. Gantilah port bawaan Node-RED dan buktikan bahwa Node-RED bisa diakses dari public network?

bukti gambar ketika menggunakan port 1998 dan IP laptop Rafif dan diakses dari laptop Raka Bagas,

- pada laptop Rafif

<img src="Kelompok 1/securityp1-rf.png" width="500px">

- pada laptop Raka Bagas

<img src="Kelompok 1/securityp1-raka.jpeg" width="500px">

<br/>

2. Buktikan dengan tangkapan layar perbedaan antar permisi untuk user read dan full access?

bukti gambar :

- user read tidak dapat melakukan perubahan apapun pada project, terbukti akan muncul pop up ketika mengklik deploy :

<img src="Kelompok 1/securityp2-user.png" width="650px">

- sedangkan user full akses dapat melakukan perubahan pada project, terbukti dapat melalukan deploy :

<img src="Kelompok 1/securityp2-admin.png" width="650px">

<br/>
<br/>

## Praktikum 3 - Sample Node-RED

1. Drag sebuah pallete node `inject` pada kategori `network` ke worksheet perhatikan gambar berikut ini

<img src="Kelompok 1/sample1.png" width="500px">

2. Selanjutnya double klik node `inject` yang terdapat pada worksheet sehingga menampilkan jendela properties seperti berikut

<img src="Kelompok 1/sample2.png" width="500px">

3. Tambahkan juga node `http request` pada worksheet, sesuaikan properties pada nilai `URL` dan `name`. Isikan `URL` dengan `https://raw.githubusercontent.com/prust/wikipedia-movie-data/master/movies.json` dan sedangkan `name` diisi dengan `movie request`. Untuk lebih jelasnya dapat dilihat pada gambar berikut ini

<img src="Kelompok 1/sample3.png" width="500px">

4. Hubungkan node make request (`inject`) dan movie request (`http request`) dengan cara klik dan drag antar ujung node, hasilnya dapat dilihat pada gambar berikut ini

<img src="Kelompok 1/sample4.png" width="500px">

5. Tambahkan node debug yang terdapat pada kategori `common`, jangan lupa diubah name dengan nama msg. Terakhir hubungkan node tersebut dengan node `movie request`. Hasil akhirnya adalah sebagai berikut

<img src="Kelompok 1/sample5.png" width="500px">

6. Langkah terakhir, silahkan klik tombol `Deploy` yang terletak di pojok kanan atas sampai muncul popup `successfully deployed`. Jika sudah, klik `make request` dan amati hasilnya pada bagian `debug` (klik icon kutu) di jendela sebelah kanan. Untuk lebih jelasnya dapat dilihat pada gambar di bawah ini

<img src="Kelompok 1/sample6.png" width="400px">

<br/>

#### Pertanyaan

1. Tambahkan kembali node function dan node debug, yang masing-masing fungsinya adalah untuk memfilter dimana movie yang akan tampil hanya movie dengan tahun > 2000 dan untuk menampilkan data filter tersebut.

2. Flow dan output pada debug dapat dilihat seperti berikut ini

<img src="Kelompok 1/sample-p1.png" width="500px">

- Kodingan untuk Node Function :

<img src="Kelompok 1/sample-p2.png" width="500px">

- Hasil :

<img src="Kelompok 1/sample-p3.png" width="300px">

<br/>
<br/>
<br/>

# TUGAS

Buatlah sebuah flow yang digunakan untuk menentukan sebuah kondisi temperatur dingin, normal, dan panas. Terdapat 3 node inject masing-masing sebagai berikut;

1. Ketika inject pertama diklik akan muncul di panel debug menampilkan dingin, lewatkan nilai 5 pada node inject pertama.
2. Ketika inject kedua diklik akan muncul di panel debug menampilkan normal, lewatkan nilai 25 pada node inject kedua.
3. Ketika inject ketiga diklik akan muncul di panel debug menampilkan panas, lewatkan nilai 50 pada node inject ketiga.

### Jawaban

1. Ketika inject pertama diklik akan muncul di panel debug menampilkan dingin, lewatkan nilai 5 pada node inject pertama.

<img src="Kelompok 1/tugas1.png" width="500px">

2. Ketika inject kedua diklik akan muncul di panel debug menampilkan normal, lewatkan nilai 25 pada node inject kedua

<img src="Kelompok 1/tugas2.png" width="500px">

3. Ketika inject ketiga diklik akan muncul di panel debug menampilkan panas, lewatkan nilai 50 pada node inject ketiga.

<img src="Kelompok 1/tugas3.png" width="500px">

4. Kodingan Node Function Conditional

<img src="Kelompok 1/tugas4.png" width="500px">

5. Hasil :

<img src="Kelompok 1/tugas5.png" width="300px">
