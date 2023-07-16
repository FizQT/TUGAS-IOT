# Anggota Kelompok

1. Ahmad Rafif Alaudin( 02 / 2041720230)
2. Raka Bagas Fitriansyah( 15 / 2041720187)
3. Thirsya Widya Sulaiman( 18 / 2041720233)

<br/>

# PRAKTIKUM PEKAN KE-10

<br/>

## Praktikum 1 - Instalasi Server Menggunakan Python

Pada praktikum ke-1 diawali dengan menjalankan socket server untuk siap menerima komunikasi dari socket client yang menggunakan python (server.py) dan menggunakan port yang open  atau sudah di konfigurasi sehingga bisa diakses tidak hanya dari lokal.

Kode Program :

```c++
import socket
from threading import Thread


# Multithreaded Python server
class ClientThread(Thread):

    def __init__(self, ip, port):
        Thread.__init__(self)
        self.ip = ip
        self.port = port
        print("Incoming connection from " + ip + ":" + str(port))

    def run(self):
        while True:
            try:
                data = conn.recv(2048)
                if len(data) == 0:
                    break
                 # Receive all data until the newline character
                data = b""
                while b"\n" not in data:
                    chunk = conn.recv(2048)
                    if not chunk:
                        break
                    data += chunk
                print("length: " + str(len(data)-2))
                print("Server received data:", data)
                # MESSAGE = input("Input response:")
                MESSAGE = "OK"
                conn.send(MESSAGE.encode("utf8"))  # echo
            except Exception as e:
                print(e)
                break


TCP_IP = "0.0.0.0"
TCP_PORT = 2004
BUFFER_SIZE = 1024

tcpServer = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcpServer.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
tcpServer.bind((TCP_IP, TCP_PORT))
threads = []

while True:
    tcpServer.listen(4)
    print("Server started on " + TCP_IP + " port " + str(TCP_PORT))
    (conn, (ip, port)) = tcpServer.accept()
    newthread = ClientThread(ip, port)
    newthread.start()
    threads.append(newthread)

for t in threads:
    t.join()


```

<b>Verifikasi Hasil Praktikum 1 (Hasil) :</b>

<img src="Kelompok 1/prak1.png" width="500px">

<b>Keterangan Hasil</b> : setelah menjalankan server kemudian melakukan telnet maka inputan string pada telnet dapat tertampil lagi pada server sekaligus bersama panjang stringnya.

</br>

Setelah berhasil menjalankan socket sever, selanjutnya perlu dibuat socket client yang berjalan di controller atau ESP8266 Amica atau Lolita dimana sudah terdapat modul wifi yang siap.

Untuk kode yang menyesuaikan dengan kebutuhan, kami mengubah menjadi sebagai berikut :

```c++
const char *ssid = "****";
const char *password = "****";
const uint16_t port = ****;
const char *host = "****";
```

Keterangan:

- `ssid` adalah ssid yang bisa digunakan untuk berkomunikasi, bisa tethering dengan handphone.
- `password` adalah password ssid yang digunakan.
- `port` adalah port socket sever aplikasi yang telah kita buat sebelumnya.
- `host` adalah host tempat socket server dijalankan, jika di local bisa menggunakan `localhost` atau `127.0.0.1`.

kode program :

```c++
#include <Arduino.h>
#include <ESP8266WiFi.h>

#define LED D4

const char *ssid = "Araspot";        // nama SSID untuk koneksi Anda
const char *password = "yondatau";   // password akses point WIFI Anda
const uint16_t port = 2004;          // diganti dengan port serve Anda
const char *host = "192.168.83.101"; // diganti dengan host server Anda, bisa ip ataupun domain

void connect_wifi()
{
  Serial.printf("Connecting to %s ", ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }
  Serial.println(" connected");
}

void connect_server()
{
  WiFiClient client;

  Serial.printf("\n[Connecting to %s ... ", host);
  if (client.connect(host, port))
  {
    Serial.println("connected]");

    Serial.println("[Sending a request]");
    client.print("Hai from ESP8266");

    Serial.println("[Response:]");
    String line = client.readStringUntil('\n');
    Serial.println(line);
    client.stop();
    Serial.println("\n[Disconnected]");
  }
  else
  {
    Serial.println("connection failed!]");
    client.stop();
  }
  delay(3000);
}

void setup()
{
  Serial.begin(115200);
  connect_wifi();
}

void loop()
{
  connect_server();
}
```

video hasil :



https://user-images.githubusercontent.com/90122538/236789570-20189250-6a8a-41a1-b910-cfaecc1d09ed.mp4



</br>
</br>

## Praktikum 2

Pada praktikum ke-2 menggunakan socket server pada praktikum ke-1 untuk menerima input dari keyboard sehingga dapat dimanfaatkan untuk memasukan perintah pada controller atau ESP8266 yang dimiliki dengan mengubah kode pada fungsi run.

Kode Program `server.py` :

```py
import socket
from threading import Thread
from time import sleep


# Multithreaded Python server
class ClientThread(Thread):

    def __init__(self, ip, port):
        Thread.__init__(self)
        self.ip = ip
        self.port = port
        print("Incoming connection from " + ip + ":" + str(port))

    def run(self):
        while True:
            try:
                MESSAGE = input("Input response:")
                conn.send(MESSAGE.encode("utf8"))  # echo
            except Exception as e:
                print(e)
                break
            sleep(0.25)


TCP_IP = "0.0.0.0"
TCP_PORT = 9001
BUFFER_SIZE = 20

tcpServer = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcpServer.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
tcpServer.bind((TCP_IP, TCP_PORT))
threads = []

while True:
    tcpServer.listen(4)
    print("Server started on " + TCP_IP + " port " + str(TCP_PORT))
    (conn, (ip, port)) = tcpServer.accept()
    newthread = ClientThread(ip, port)
    newthread.start()
    threads.append(newthread)

for t in threads:
    t.join()

```

Kode Program `main.cpp` :

```c++
#include <Arduino.h>
#include <ESP8266WiFi.h>

const char *ssid = "Araspot";        // nama SSID untuk koneksi Anda
const char *password = "yondatau";   // password akses point WIFI Anda
const uint16_t port = 9001;          // diganti dengan port serve Anda
const char *host = "192.168.83.101"; // diganti dengan host server Anda, bisa ip ataupun domain

WiFiClient client;

void connect_wifi()
{
  Serial.printf("Connecting to %s ", ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }
  Serial.println(" connected");
  delay(250);
}

void connect_server()
{
  while (!client.connect(host, port))
  {
    Serial.printf("\n[Connecting to %s ... ", host);
    delay(1000);
    return;
  }
  Serial.println("connected]");
  delay(1000);
}

void setup()
{
  Serial.begin(115200);
  Serial.println("Contoh penggunaan socket client");
  connect_wifi();
  connect_server();
}

void loop()
{
  if (client.connected())
  {
    Serial.print("[Response:]");
    String line = client.readStringUntil('\n');
    Serial.println(line);
    if (line.equalsIgnoreCase("led-on"))
    {
      pinMode(LED_BUILTIN, HIGH);
      delay(3000);
      pinMode(LED_BUILTIN, LOW);
    }
  }
  else
  {
    connect_server();
  }
  delay(250);
}
```

<b>Verifikasi Hasil Praktikum 2 (Hasil :)</b>

Video :



https://user-images.githubusercontent.com/90122538/236790029-d27dd39e-3d10-40db-8fd2-b91e3661a849.mp4



<b>Keterangan Hasil</b> :

Dari hasil praktikum kami berhasil menyalakan lampu LED ketika memasukkan inputan "led-on" pada server.

<br/>
<br/>

# TUGAS

Terdapat sebuah dusun di desa tertentu yang sudah menerapkan IoT, contoh penerapan tersebut di gang-gang ketika sudah beranjak malam lampu yang terdapat pada gang tersebut akan menyala. Pada dusun tersebut juga terdapat kebun rumah kaca, dimana suhu dan kelembaban sangat diperhatikan untuk menjaga produktivitas sayur-sayur di dalam kebun. Semua sensor yang terdapat pada dusun tersebut juga dapat dipantau langsung menggunakan LCD, selain itu secara terus menerus data sensor dikirimkan ke server secara periodik(misalkan setiap 10 detik) serta semua lampu yang terdapat pada gang-gang dapat dinyalakan melalui server, ketika posisi malam tiba server memerintahkan lampu untuk menyala jika belum menyala. Lampu yang digunakan bisa menggunakan LED. Dari kasus di atas, buat program untuk kebutuhan tersebut baik dari sisi controller (ESP8266) dan dari sisi server. Adapun kebutuhannya adalah sebagai berikut

1. Terdapat sensor LDR, DHT11, serta untuk aktuator LCD dan LED.
2. Semua data sensor secara periodik dikirimkan ke server, misalkan setiap 10 detik. Server cukup menampilkan data sensor di konsol, tidak perlu diolah atau disimpan.
3. Data sensor juga ditampilkan di LCD.
4. LED bisa dinyalakan oleh server pada waktu tertentu, perlu ada pengecekan apakah LED sudah nyala atau belum.
5. Selamat mencoba. ^_^

Seperti biasa untuk output dokumentasikan berupa link video google drive ataupun youtube, selanjutnya sisipkan link tersebut pada laporan Anda.

kode program `server.py` :

```py
import socket
from threading import Thread
from time import sleep


# Multithreaded Python server
class ClientThread(Thread):

    def __init__(self, ip, port):
        Thread.__init__(self)
        self.ip = ip
        self.port = port
        # print("Incoming connection from " + ip + ":" + str(port))
        data = conn.recv(2048)
        print("Server received data:", data)

    def run(self):
        while True:
            try:
                MESSAGE = input("Input response:")
                conn.send(MESSAGE.encode("utf8"))  # echo
            except Exception as e:
                print(e)
                break
            sleep(0.25)


TCP_IP = "0.0.0.0"
TCP_PORT = 9001
BUFFER_SIZE = 20

tcpServer = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcpServer.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
tcpServer.bind((TCP_IP, TCP_PORT))
threads = []

while True:
    tcpServer.listen(4)
    # print("Server started on " + TCP_IP + " port " + str(TCP_PORT))
    (conn, (ip, port)) = tcpServer.accept()
    newthread = ClientThread(ip, port)
    newthread.start()
    threads.append(newthread)

for t in threads:
    t.join()

```

kode program `main.cpp` :

```c++
#include <Arduino.h>
#include <ESP8266WiFi.h>
#include <LiquidCrystal_I2C.h>
#include <SimpleDHT.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

#define pinDHT 7 // SD3 pin signal sensor DHT

byte temperature = 0;
byte humidity = 0;

SimpleDHT11 dht11(D7); // instan sensor dht11

// LDR
#define sensorLDR A0
int nilaiSensor;

const char *ssid = "Araspot";        // nama SSID untuk koneksi Anda
const char *password = "yondatau";   // password akses point WIFI Anda
const uint16_t port = 9001;          // diganti dengan port serve Anda
const char *host = "192.168.83.101"; // diganti dengan host server Anda, bisa ip ataupun domain

WiFiClient client;

void connect_wifi()
{
  Serial.printf("Connecting to %s ", ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }
  Serial.println(" connected");
  delay(250);
}

void connect_server()
{

  while (!client.connect(host, port))
  {
    Serial.printf("\n[Connecting to %s ... ", host);
    delay(1000);
    return;
  }
  Serial.println("connected]");
  delay(1000);
}

void setup()
{
  Serial.begin(115200);
  lcd.init(); // initialize the lcd
  lcd.backlight();
  lcd.clear();
  lcd.home();

  connect_wifi();
  connect_server();
}

void cekDHT()
{
  // cek DHT11
  int err = SimpleDHTErrSuccess;

  if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
  {
    Serial.print("Pembacaan DHT11 gagal, err=");
    Serial.println(err);
    delay(1000);
    return;
  }
}

void loop()
{
  WiFiClient client;

  cekDHT();
  float celsius = (float)temperature;

  // mengambil data cahaya
  nilaiSensor = analogRead(sensorLDR);

  lcd.home();

  lcd.print("suhu  : ");
  lcd.print(String(celsius, 2)); // mencetak suhu dengan 2 digit di belakang koma
  lcd.write(byte(0xDF));         // menampilkan simbol derajat dengan karakter ASCII khusus
  lcd.print("C ");

  lcd.setCursor(0, 1); // set cursor to column 0, row 1
  lcd.print("cahaya : ");
  lcd.print(String(nilaiSensor)); // mencetak nlai LDR

  String dataServer = "suhu :" + String(celsius) + "C | Cahaya : " + String(nilaiSensor);

  if (client.connect(host, port))
  {
    client.print(dataServer);
    Serial.print("[Response:]");
    String line = client.readStringUntil('\n');
    Serial.println(line);

    int ledState = digitalRead(LED_BUILTIN);

    if (ledState == HIGH && line.equalsIgnoreCase("led-off"))
    {
      pinMode(LED_BUILTIN, LOW);
    }
    else if (ledState == LOW && line.equalsIgnoreCase("led-off"))
    {
      pinMode(LED_BUILTIN, LOW);
    }
    else if (ledState == HIGH && line.equalsIgnoreCase("led-on"))
    {
      pinMode(LED_BUILTIN, HIGH);
    }
    else if (ledState == LOW && line.equalsIgnoreCase("led-on"))
    {
      pinMode(LED_BUILTIN, HIGH);
    }
  }
  else
  {
    connect_server();
  }
  delay(10000);
}
```

Hasil Output :



https://user-images.githubusercontent.com/90122538/236792130-04ce4a1d-adf5-4109-b92f-784c4dbcee37.mp4



<b>video Dokumentasi : </b>

Video Tugas : [https://drive.google.com/file/d/1pK168VQIYS3Y05TZy-eag-90G8TN6hf_/view?usp=sharing](https://drive.google.com/file/d/1pK168VQIYS3Y05TZy-eag-90G8TN6hf_/view?usp=sharing)

video praktikum 1 : [https://drive.google.com/file/d/1_G3CRhp405uSMRmV02rvJ_KgshSH8t1Z/view?usp=sharing](https://drive.google.com/file/d/1_G3CRhp405uSMRmV02rvJ_KgshSH8t1Z/view?usp=sharing)

video Praktikum 2 : [https://drive.google.com/file/d/1vU2ZnDWMafkkYt7VXV_rCEYsrE5GEOEd/view?usp=sharing](https://drive.google.com/file/d/1vU2ZnDWMafkkYt7VXV_rCEYsrE5GEOEd/view?usp=sharing)
