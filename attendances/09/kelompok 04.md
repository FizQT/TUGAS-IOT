# <b>LAPORAN PRAKTIKUM  
# Anggota Kelompok
1. Gustania Nirmala Meisi (10)
2. Rosis Hudaya Putra (16)
3. Safira Istifarini (17)<br>

# <b>PRAKTIKUM PERTEMUAN 11

## <b>Praktikum 1 <br>
Install Node-RED di local<br>
1. Pastikan sudah terinstall Node.js dan npm
2. Versi yang direkomendasikan node.js: v18.15.0 atau di atasnya
3. Versi npm9.5.0 atau di atasnya
4. Ketik perintah<br>

```cpp
npm install -g --unsafe-perm node-red
```

Menambahkan Keamanan pada Node-Red<br>
1. Silakan edit file ```settings.js```, file tersebut merupakan file konfigurasi Node-RED. Biasanya terletak pada home direktori installasi Node-RED. File tersebut terletak di ```.node-red/settings.js``` <br>

```cpp
ubuntu@ip-172-31-21-64:~$ pwd
   /home/ubuntu
   ubuntu@ip-172-31-21-64:~$ ls -al
   total 36
   drwxr-xr-x 6 ubuntu ubuntu 4096 Apr 10 14:38 .
   drwxr-xr-x 3 root   root   4096 Apr 10 14:00 ..
   -rw-r--r-- 1 ubuntu ubuntu  220 Feb 25  2020 .bash_logout
   -rw-r--r-- 1 ubuntu ubuntu 3771 Feb 25  2020 .bashrc
   drwx------ 2 ubuntu ubuntu 4096 Apr 10 14:01 .cache
   drwxrwxr-x 3 ubuntu ubuntu 4096 Apr 10 14:38 .local
   drwxrwxr-x 4 ubuntu ubuntu 4096 Apr 10 14:45 .node-red
   -rw-r--r-- 1 ubuntu ubuntu  807 Feb 25  2020 .profile
   drwx------ 2 ubuntu ubuntu 4096 Apr 10 14:00 .ssh
   -rw-r--r-- 1 ubuntu ubuntu    0 Apr 10 14:08 .sudo_as_admin_successful
   ubuntu@ip-172-31-21-64:~$ ls -al .node-red/settings.js
   -rw-r--r-- 1 ubuntu ubuntu 15473 Apr 10 14:41 .node-red/settings.js
   ```
   2. Buka file ```settings.js``` menggunakan editor misalkan menggunakan nano dengan perintah ```nano .node-red/settings.js``` atau langsung bisa menggunakan SFTP kemudian buka comment baris berikut ini, setelah dibuka seperti berikut : 

```cpp
   // Securing Node-RED
    // -----------------
    // To password protect the Node-RED editor and admin API, the following
    // property can be used. See http://nodered.org/docs/security.html for details.

    adminAuth: {
        type: "credentials",
        users: [{
            username: "admin",
            password: "$2b$08$WcJwycUos6FqbUKZsIfGzOqHC4kJQ0GHY7Oz.mR7zaasPtBHuk2gm",
            permissions: "*"
        },{
        username: "odeng",
        password: "$2a$08$5LFz5nVwzCyX/r6rHb4KpuvG16pUwPYHTA/OxBqwTqdNB9a6K/rru",
        permissions: "read"
    }]
    },
```
3. Isikan username, password, dan permisi dari setiap user. Hanya terdapat 2 rule yang dapat digunakan yaitu full akses dan read. Yang membedakan 2 rule tersebut adalah read tidak bisa digunakan untuk menambahkan library atau pallete ataupun mengkonfigurasi node-read. Untuk membuat password silakan menggunakan perintah bawaan dari node-red seperti berikut : 

```cpp
    ubuntu@ip-172-31-21-64:~$ node-red admin hash-pw
    Password:
````
### <b>Pertanyaan <br>
1. Gantilah port bawaan Node-RED dan buktikan bahwa Node-RED bisa diakses dari public network?<br>

2. Buktikan dengan tangkapan layar perbedaan antar permisi untuk user read dan full access?<br>

### <b>Jawaban <br>
1. Mengganti port bawaan Node-RED <br>

<img src = "kelompok04\port1.jpeg" width="500px"> <br>


<img src = "kelompok04\port2.jpeg" width="500px"> <br>
2. Tangkapan layar untuk perbedaan antara kedua role : <br>
A. Permission user read <br>
<img src = "kelompok04\read.PNG" width="500px">
B. Permission user full accesss <br>
<img src = "kelompok04\full_access.PNG" width="500px"> <br>

## <b>Praktikum 2 <br>

Sample Node-Red<br>
Pada praktikum yang ini ditunjukkan menggunakan Node-RED untuk request sebuah end point dan menampilkan response dalam sebuah mode debug. Silakan mengikuti langkah-langkah di bawah ini

1. Drag sebuah pallete node inject pada kategori network ke worksheet
2. Selanjutnya double klik node inject yang terdapat pada worksheet sehingga menampilkan jendela properties. Ubah name menjadi make request dan hapus properti msg.payload serta msg.topic menggunakan icon cross, jika sudah jangan lupa klik tombol Done.
3. Tambahkan juga node http request pada worksheet, sesuaikan properties pada nilai URL dan name. Isikan URL dengan https://raw.githubusercontent.com/prust/wikipedia-movie-data/master/movies.json 
<br> dan sedangkan name diisi dengan movie request.
4. Hubungkan node make reqeust (inject) dan movie request (http request) dengan cara klik dan drag antar ujung node.
5. Tambahkan node debug yang terdapat pada kategori common, jangan lupa diubah name dengan nama msg. Terakhir hubungkan node tersebut dengan node movie request.
6. Langkah terakhir, silakan klik tombol Deploy yang terletak di pojok kanan atas sampai muncul popup successfully deployed. Jika sudah, klik make request dan amati hasilnya pada bagian debug (klik icon kutu) di jendela sebelah kanan.
7. Hasilnya :<br>
<img src = "kelompok04\tugas1.PNG" width="500px">

### <b>Pertanyaan <br>
1. Tambahkan kembali node function dan node debug, yang masing-masing fungsinya adalah untuk memfilter dimana movie yang akan tampil hanya movie dengan tahun > 2000 dan untuk menampilkan data filter tersebut.<br>

2. Flow dan output pada debug dapat dilihat seperti berikut ini<br>

### <b>Jawaban <br>
1. Kode Program <br>
```cpp
try {
    // konversi data menjadi JSON string yang valid
    const jsonString = JSON.stringify(msg.payload);

    // parsing JSON string
    const parsedData = JSON.parse(jsonString);

    // filtering data JSON
    const filteredData = parsedData.filter((movie) => {
        return movie.year > 2000;
    });

    msg.payload = filteredData;
    return msg;
} catch (error) {
    node.error(error);
}
```
2. Flow dan outputnya, sebagai berikut : 
<img src = "kelompok04\flow.jpeg" width="500px"> <br>

## <b>Tugas<br>

Buatlah sebuah flow yang digunakan untuk menentukan sebuah kondisi temperatur dingin, normal, dan panas. Terdapat 3 node inject masing-masing sebagai berikut :

1. Ketika inject pertama diklik akan muncul di panel debug menampilkan dingin, lewatkan nilai 5 pada node inject pertama.
2. Ketika inject kedua diklik akan muncul di panel debug menampilkan normal, lewatkan nilai 25 pada node inject kedua.
3. Ketika inject ketiga diklik akan muncul di panel debug menampilkan panas, lewatkan nilai 50 pada node inject ketiga.

### <b>Jawaban <br>
<img src = "kelompok04\tugas.jpeg" width="500px"> <br>

