# <b>LAPORAN PRAKTIKUM  
# Anggota Kelompok
1. Gustania Nirmala Meisi (10)
2. Rosis Hudaya Putra (16)
3. Safira Istifarini (17)<br>

# <b>PRAKTIKUM PERTEMUAN 13

## <b>Praktikum 1 <br>
Install Dashboard Node-RED <br>
1. Silakan akses Node-RED via browser, http://127.0.0.1:1880/ ( Menyesuaikan alamat port Node-Red masing masing)
2. Klik button yang terdapat di pojok kanan atas dan cari menu Manage pallete lalu klik
3. Setelah muncul jendela User Settings, pilih tab install dan ketik dashboard sehingga akan muncul modul-modul yang bisa kita install dan klik tombol install
4. Setelah muncul pop notifikasi proses install, silakan pilih atau klik tombol install
5. Lalu cek dengan melihat pada Node-RED via browser
6. Hasilnya :<br>

<img src = "kelompok04\prak1.PNG" width="500px">

## <b>Praktikum 2 <br>
Membuat Dashboard Node-RED <br>
1. Pilih menu dashboard, yang terdapat di pojok kanan bawah. dashboard ini adalah untuk mengkonfigurasi website yang akan kita buat misalkan dari sistem menu/hirarki menu ataupun title website.
2. Pada bagian Tabs & Links klik tombol tab sehingga akan ditambahkan tab baru di bawahnya, pada tab baru yang terbentuk yaitu Tab 1 klik tombol edit sehingga akan muncul jendela Edit dashboard tab node
3. Pada bagian Tabs & Links klik tombol tab sehingga akan ditambahkan tab baru di bawahnya, pada tab baru yang terbentuk yaitu Tab 1 klik tombol edit sehingga akan muncul jendela Edit dashboard tab node<br>
Pada bagian Name isikan Home dan Icon diganti dengan fa-home dan klik tombol Update untuk mengakhiri.
4. Selanjutnya tambahkan Group pada Tab Home tersebut dengan klik tombol group. Selanjutnya klik edit pada group yang baru ditambahkan sehingga akan muncul jendela Edit dashboard tab node kembali. 
5. Ulangi langkah sebelumnya
6. Drag ke worksheet/flow node switch kemudian double klik sehingga akan menampilkan jendela seperti di bawah, sesuaikan bagian seperti Group, Label, dan Name
7. Ulangi langkah sebelumnya, tetapi yang ditambahkan adalah node text, sesuaikan property
8. Hubungkan node switch dan node text, hasil akhirnya adalah sebagai berikut. Kemudian silakan lakukan deploy dengan klik tombol Deploy. Untuk melihat tampilannya silakan akses Node-RED, ```http://127.0.0.1:1880//ui```
9. Hasilnya : 

<img src = "kelompok04\prak2.jpeg" width="500px">

### <b>Pertanyaan <br>

1. Silakan modifikasi flow di atas sehingga ketika node switch digeser tidak menghasilkan nilai true atau false, tetapi ketika digeser nilainya adalah nyala atau mati. 

### <b>Jawaban <br>

<img src = "kelompok04\prak3.jpeg" width="500px">

## <b>Tugas<br>

Buatlah sebuah dashboard website untuk memonitoring dan control pada sebuah ruang lobby, ruang kajur, dan ruang dosen. Masing-masing ruang dengan detail node yang dibutuhkan pada node dashboard sebagai berikut;

1. Tab Home memiliki group Lobby, Ruang Kajur, dan Ruang Dosen.<br>

- Group Lobby terdapat 2 node inject, 2 function, gauge, dan chart.<br>
- Group Ruang Kajur terdapat 2 node inject, 2 function, gauge, dan chart.<br>
- Group Ruang Dosen terdapat 2 node inject, 2 function, gauge, dan chart.<br>
- Jika diperhatikan node gauge dan chart bisa otomatis berjalan, hal tersebut diaktifkan saja pada bagian otomatis pada node inject.<br>

Sedangkan nilai yang selalu muncul acak itu menggunakan node funcion, Math.floor(Math.random()*101)<br>

Jumlah line antara node chart pada Lobby, Ruang Kajur, dan Ruang Dosen berbeda bisa dilakukan dengan cara mengubah Setup Outputs pada function.<br>

2. Tab Room Control terdiri dari group Lampu dan AC.<br>

- Group Lampu memiliki 3 switch, 3 function, dan 3 text.
Group AC memiliki 3 slider dan 3 text.<br>

- function digunakan untuk parsing boolean ke string, "nyala atau mati"<br>

Tab About hanya terdiri dari text biasa.<br>

### <b>Jawaban <br>

<img src = "kelompok04\Capture.PNG" width="500px"> <br>

<img src = "kelompok04\1.PNG" width="500px"> <br>

Video dokumentasi tugas [klik disini](https://drive.google.com/file/d/1QjFIUHo-r-LOkSajcPMNN1sXbPMuQtET/view?usp=sharing)