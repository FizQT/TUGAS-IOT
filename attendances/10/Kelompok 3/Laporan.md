## PRAKTIKUM IOT PERTEMUAN 13 TI-3G
### Kelompok 3 TI-3G:
Nama anggota : <br>
1. Dherisma Hanindita Utami (07)
2. Dilta Febiana (08)
3. Meliusa Nora Hariyanti (13)

## Manajemen Iot Dashboard
Hasil Praktikum
<image src= "prak1.png">
<image src= "prak2.png">

### Jawaban Pertanyaan 
modifikasi flow di atas sehingga ketika node switch digeser tidak menghasilkan nilai true atau false, tetapi ketika digeser nilainya adalah nyala atau mati. 

Jawab : 
<image src= "1.png">
<image src= "2.png">
<image src= "3.png">
<image src= "4.png">

### TUGAS
1. Tab Home memiliki group Lobby, Ruang Kajur, dan Ruang Dosen.
Group Lobby terdapat 2 node inject, 2 function, gauge, dan chart.
Group Ruang Kajur terdapat 2 node inject, 2 function, gauge, dan chart.
Group Ruang Dosen terdapat 2 node inject, 2 function, gauge, dan chart.
Jika diperhatikan node gauge dan chart bisa otomatis berjalan, hal tersebut diaktifkan saja pada bagian otomatis pada node inject.

    Sedangkan nilai yang selalu muncul acak itu menggunakan node funcion, 

        Math.floor(Math.random()*101)

    Jumlah line antara node chart pada Lobby, Ruang Kajur, dan Ruang Dosen berbeda bisa dilakukan dengan cara mengubah Setup Outputs pada function.

    Jawab : 

    Desain Node-red

     <image src= "17.jpg">
     
    home inject
    <image src= "5.jpeg">

    home function
    <image src= "19.jpg">

    <image src= "20.jpg">

    <image src= "8.jpeg">
   
   Output :

    <image src= "18.jpg">

2. Tab Room Control terdiri dari group Lampu dan AC.
Group Lampu memiliki 3 switch, 3 function, dan 3 text.
Group AC memiliki 3 slider dan 3 text.
function digunakan untuk parsing boolean ke string, "nyala atau mati".

    Jawab : 

    Desain Node-red Lampu
    <image src= "desain2.jpeg">
    
    <image src= "9.jpeg">
    <image src= "10.jpeg">
    <image src= "11.jpeg">

    Desain Node-red AC
    <image src= "desain3.jpeg">

    <image src= "12.jpeg">
    <image src= "13.jpeg">
 
    Output :
    <image src= "output2.jpeg">

3. Tab About hanya terdiri dari text biasa.

    Desain Node-red Text :

    <image src= "desain4.jpeg">

    <image src= "14.jpeg">

    Output :
     <image src= "output3.jpeg">

Tampilan Tab pada Node-red
    <image src= "15.jpeg">


