# <b>LAPORAN PRAKTIKUM  
# Anggota Kelompok
1. Gustania Nirmala Meisi (10)
2. Rosis Hudaya Putra (16)
3. Safira Istifarini (17)<br>

# <b>PRAKTIKUM PERTEMUAN 10

## <b>Praktikum 1 <br>
Membuat sebuah server TCP/IP sederhana yang dapat menerima koneksi dari beberapa klien secara simultan. Server ini menggunakan pendekatan multithreading, di mana setiap koneksi klien baru akan diurus oleh sebuah thread baru.<br>
Kode Program :<br>
```cpp
import socket
from threading import Thread


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
TCP_PORT = 5000
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
Verifikasi hasil percobaan:<br>
<img src = "kelompok04\1.jpg" width="200">
<img src = "kelompok04\2.jpg" width="150"><br>
Setelah berhasil menjalankan socket sever, selanjutnya perlu dibuat socket client yang berjalan di controller atau ESP8266 Amica<br>
Kode Program : <br>

```cpp
#include <Arduino.h>
#include <ESP8266WiFi.h>

#define LED D4

const char *ssid = "****"; // nama SSID untuk koneksi Anda
const char *password = "****"; // password akses point WIFI Anda
const uint16_t port = ****; // diganti dengan port serve Anda
const char *host = "****";//diganti dengan host server Anda, bisa ip ataupun domain

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

Hasil Praktikum 1:<br>
<img src = "kelompok04\prak1.jpg" width="500px">
<img src = "kelompok04\prak12.jpg" width="500px">

Keterangan:

`ssid` adalah ssid yang bisa digunakan untuk berkomunikasi, bisa tethering dengan handphone.

`password` adalah password ssid yang digunakan.

`port` adalah port socket sever aplikasi yang telah kita buat sebelumnya.

`host` adalah host tempat socket server dijalankan, jika di local bisa menggunakan localhost atau 127.0.0.1.
```cpp
const char *ssid = "****";
const char *password = "****";
const uint16_t port = ****;
const char *host = "****";
```
## <b>Praktikum 2
Menggunakan kode socket server yang sebelumnya, ubahlah kode pada fungsi `run` menjadi seperti di bawah ini.
```cpp
def run(self):
        while True:
            try:
                MESSAGE = input("Input response:")
                conn.send(MESSAGE.encode("utf8"))  # echo
            except Exception as e:
                print(e)
                break
            sleep(0.25)
```
Dengan mengubah program tersebut, socket server yang akan kita buat mampu menerima input dari keyboard sehingga dapat dimanfaatkan untuk memasukan perintah pada controller atau ESP8266 yang kita miliki.<br>
Kode Program `main.cpp`
```cpp
#include <Arduino.h>
#include <ESP8266WiFi.h>

#define LED D4

const char *ssid = "Galaxy A514696"; // nama SSID untuk koneksi Anda
const char *password = "nyambung";   // password akses point WIFI Anda
const uint16_t port = 5000;          // diganti dengan port serve Anda
const char *host = "192.168.22.45";  // diganti dengan host server Anda, bisa ip ataupun domain

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
Hasil praktikum 2 :<br>
<img src = "kelompok04\prak2.jpg" width="500px">

## <b>Tugas Praktikum
Terdapat sebuah dusun di desa tertentu yang sudah menerapkan IoT, contoh penerapan tersebut di gang-gang ketika sudah beranjak malam lampu yang terdapat pada gang tersebut akan menyala. Pada dusun tersebut juga terdapat kebun rumah kaca, dimana suhu dan kelembaban sangat diperhatikan untuk menjaga produktivitas sayur-sayur di dalam kebun. Semua sensor yang terdapat pada dusun tersebut juga dapat dipantau langsung menggunakan LCD, selain itu secara terus menerus data sensor dikirimkan ke server secara periodik(misalkan setiap 10 detik) serta semua lampu yang terdapat pada gang-gang dapat dinyalakan melalui server, ketika posisi malam tiba server memerintahkan lampu untuk menyala jika belum menyala. Lampu yang digunakan bisa menggunakan LED. Dari kasus di atas, buat program untuk kebutuhan tersebut baik dari sisi controller (ESP8266) dan dari sisi server. Adapun kebutuhannya adalah sebagai berikut

1. Terdapat sensor LDR, DHT11, serta untuk aktuator LCD dan LED.
2. Semua data sensor secara periodik dikirimkan ke server, misalkan setiap 10 detik. Server cukup menampilkan data sensor di konsol, tidak perlu diolah atau disimpan.
3. Data sensor juga ditampilkan di LCD.
4. LED bisa dinyalakan oleh server pada waktu tertentu, perlu ada pengecekan apakah LED sudah nyala atau belum.
5. Selamat mencoba. ^_^<br>

Kode Program :
```cpp
#include <Arduino.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <SimpleDHT.h>
#include <ESP8266WiFi.h>

const char *SSID = "Galaxy A514696";       // SSID WiFi
const char *PASSWORD = "nyambung";         // Password WiFi
const char *SERVER_IP = "192.168.158.149"; // Alamat IP server
const int SERVER_PORT = 5000;              // Port server

const int DHT_PIN = D3;
SimpleDHT11 dht(DHT_PIN);

const int BLUE_LED_PIN = D7;
const int GREEN_LED_PIN = D6;
const int RED_LED_PIN = D5;

const int SENSOR_LDR = A0;

LiquidCrystal_I2C lcd(0x27, 16, 2);

WiFiClient client;

void setup()
{
  Serial.begin(115200);
  pinMode(BLUE_LED_PIN, OUTPUT);
  pinMode(GREEN_LED_PIN, OUTPUT);
  pinMode(RED_LED_PIN, OUTPUT);

  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("");

  WiFi.begin(SSID, PASSWORD);
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }
  Serial.println("Connected to WiFi");
}

void loop()
{
  lcd.clear();
  byte temperature = 0;
  byte humidity = 0;
  int err = SimpleDHTErrSuccess;
  if ((err = dht.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
  {
    Serial.print("Gagal membaca dari sensor DHT11, kode error: ");
    Serial.println(err);
    return;
  }

  Serial.print(String(temperature, DEC) + "°C ");
  Serial.print(String(humidity, DEC) + "% ");

  int value = 0;
  value = analogRead(SENSOR_LDR);

  Serial.println(value);

  lcd.setCursor(0, 0);
  lcd.print("Suhu ");
  lcd.print(String(temperature, DEC));
  lcd.write(byte(0xDF));
  lcd.print("C ");
  lcd.print(value);

  lcd.setCursor(0, 1);
  lcd.print("Kelembapan ");
  lcd.print(String(humidity, DEC));
  lcd.write(byte(0x25));

  if (value > 1020)
  {
    digitalWrite(RED_LED_PIN, LOW);
    digitalWrite(GREEN_LED_PIN, LOW);
    digitalWrite(BLUE_LED_PIN, HIGH);
    delay(500);
    digitalWrite(RED_LED_PIN, LOW);
    digitalWrite(GREEN_LED_PIN, HIGH);
    digitalWrite(BLUE_LED_PIN, LOW);
    delay(500);
    digitalWrite(RED_LED_PIN, HIGH);
    digitalWrite(GREEN_LED_PIN, LOW);
    digitalWrite(BLUE_LED_PIN, LOW);
    delay(500);
  }
  else
  {
    digitalWrite(RED_LED_PIN, LOW);
    digitalWrite(GREEN_LED_PIN, LOW);
    digitalWrite(BLUE_LED_PIN, LOW);
  }

  Serial.println("---");

  // Kirim data sensor ke server
  String message = "Suhu " + String(temperature) + "C " + String(value) + " |Kelembapan " + String(humidity) + "%";
  if (client.connect(SERVER_IP, SERVER_PORT))
  {
    client.println(message);
    Serial.println("Data sensor terkirim ke server");
  }
  else
  {
    Serial.println("Gagal terhubung ke server");
  }
  delay(10000);
}
```
Hasil Tugas:<br>
<img src = "kelompok04\tugas1.jpg" width="500px">
<img src = "kelompok04\tugas12.jpg" width="500px"><br>

Video dokumentasi tugas [klik disini](https://drive.google.com/file/d/1QDIYYqw3QXKPc1FqqhypkpjHZEHEIdg0/view?usp=sharing)