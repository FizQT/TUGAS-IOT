# Anggota Kelompok

1. Ahmad Rafif Alaudin( 02 / 2041720230)
2. Raka Bagas Fitriansyah( 15 / 2041720187)
3. Thirsya Widya Sulaiman( 18 / 2041720233)

<br/>

# PRAKTIKUM PEKAN KE-14

<br/>

## Praktikum 1 - MQTT Node-RED

Walaupun beberapa protokol yang dapat disupport oleh Node-RED, akan tetapi pada kesempatan kali ini protokol yang digunakan MQTT. Untuk menggunakan protokol MQTT, pada Node-RED dashboard ketika melakukan installasi sudah termasuk di dalamnya. Ikut langkah-langkah di bawah ini untuk mulai praktikum

1. Silakan seret `node inject` ke worksheet, kemudian ubahlah nilai properties seperti pada gambar berikut

<img src="Kelompok 1/prak1_1.png" width="500px">

2. Seret juga `node function` ke worksheet, sesuaikan propertiesnya seperti pada gambar berikut

<img src="Kelompok 1/prak1_2.png" width="500px">

3. Jangan lupa seret juga node mqtt out pada kategori network, tambahkan server broker agar bisa publish data dengan cara klik icon pensil. Konfigurasinya adalah sebagai berikut adalah sebagai berikut

<img src="Kelompok 1/prak1_3.png" width="500px">

>Pada bagian `Name` isikan `Mqtt Server AWS`, `Server` diisikan `broker.hivemq.com` dan port isikan `1883`.
>Untuk `node mqtt out` kira-kira seperti berikut

<img src="Kelompok 1/prak1_4.png" width="500px">

Perhatian gambar berikut untuk flow lengkapnya, setelah semua node dihubungkan.

<img src="Kelompok 1/prak1_5.png" width="500px">

4. Tambahkan `node mqtt in` ke worksheet, sesuaikan konfigurasi sebagai berikut

<img src="Kelompok 1/prak1_6.png" width="500px">

Pada bagian `Server, Topic dan Qos` disamakan dengan `node mqtt out` sedangkan `Name` silakan isikan dengan `sample subscriber`.

5. Tambahkan node terakhir yaitu `node debug`, sementara untuk kongifigurasinya tidak perlu disesuaikan. Huv bungkan kedua node tersebut sehingga menjadi sebagai berikut

</br>

Pertanyaan

1. Pada node inject, pada properties Repeat dengan nilai interval. Apakah fungsinya?

Jawab :
fungsinya adalah akan melakukan mengulangi inject secara otomatis dengan interval 3 second, atau akan melakukan inject setiap 3 detik.

2. Apakah yang dimaksud dengan baris kode msg.payload=Math.floor(Math.random()*100);?

Jawab :
baris kode diatas digunakan untuk mendapat pembulatan nilai random antara 0 - 100

3. Bagian node mqtt out, apakah fungsi Qos dengan nilai 2?

Jawab :
untuk memastikan topic yang dikirim telah diterima oleh client yang subscribe.

</br>

## Praktikum 2 - Membuat Dashboard Node-RED

Pada praktikum yang kedua akan dibuat sebuah tampilan seolah-olah menyalakan lampu dari internet, ikutilah langkah-langkah sebagai berikut :

1. erlebih dahulu pilih menu dashboard, yang terdapat di pojok kanan bawah. dashbaord ini adalah untuk mengkonfigurasi website yang akan kita buat misalkan dari sistem menu/hirarki menu ataupun title website.

<img src="Kelompok 1/prak1_1.png" width="500px">

<br/>

2. Pada bagian Tabs & Links klik tombol tab, lalu terbentuk yaitu Tab 1 klik tombol edit sehingga akan muncul jendela Edit

<img src="Kelompok 1/prak1_1.png" width="500px">

3. Tambahkan Group pada Tab Home tersebut dengan klik tombol group. Selanjutnya klik edit pada group yang baru ditambahkan

<img src="Kelompok 1/prak1_1.png" width="500px">

<br/>

4. Mengulangi langkah sebelumnya untuk membuat grup Output

<img src="Kelompok 1/prak1_1.png" width="500px">

5. Drag ke worksheet/flow node switch kemudian double klik

<img src="Kelompok 1/prak1_1.png" width="500px">

6. Ulangi langkah sebelumnya, tetapi yang ditambahkan adalah node text

<img src="Kelompok 1/prak1_1.png" width="500px">

7. Hubungkan node switch dan node text.

<img src="Kelompok 1/prak1_1.png" width="500px">

8. Hasilnya sebagai berikut dengan

<img src="Kelompok 1/prak1_1.png" width="500px">

<br>

#### Pertanyaan

1. Modifikasi program di ESP8266 di atas agar bisa melakukan subscribe dengan topik room/lamp?

Jawab :<br/>
<img src="Kelompok 1/prak2_p11.png" width="500px"><br/>
<img src="Kelompok 1/prak2_p12.png" width="500px"><br/>
2. Tambahkan kode di atas agar bisa publish nilai kelembaban dengan topik room/humadity?

Jawab :

```c++
#include <Arduino.h>
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
#include <SimpleDHT.h>

// hp
// const char *ssid = "od3ng";
// const char *password = "0d3n9bro";

// kampus
const char *ssid = "Araspot";                   // sesuaikan dengan username wifi
const char *password = "yondatau";              // sesuaikan dengan password wifi
const char *mqtt_server = "test.mosquitto.org"; // isikan server broker

WiFiClient espClient;
PubSubClient client(espClient);

SimpleDHT11 dht11(D7);

long now = millis();
long lastMeasure = 0;
String macAddr = "";

void setup_wifi()
{
  delay(10);
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.print("WiFi connected - ESP IP address: ");
  Serial.println(WiFi.localIP());
  macAddr = WiFi.macAddress();
  Serial.println(macAddr);
}

void reconnect()
{
  while (!client.connected())
  {
    Serial.print("Attempting MQTT connection...");
    if (client.connect(macAddr.c_str()))
    {
      Serial.println("connected");
    }
    else
    {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      delay(5000);
    }
  }
}

void setup()
{
  Serial.begin(115200);
  Serial.println("Mqtt Node-RED");
  setup_wifi();
  client.setServer(mqtt_server, 1883);
}

void loop()
{
  if (!client.connected())
  {
    reconnect();
  }
  if (!client.loop())
  {
    client.connect(macAddr.c_str());
  }
  now = millis();
  if (now - lastMeasure > 5000)
  {
    lastMeasure = now;
    int err = SimpleDHTErrSuccess;

    byte temperature = 0;
    byte humidity = 0;
    if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
    {
      Serial.print("Pembacaan DHT11 gagal, err=");
      Serial.println(err);
      delay(1000);
      return;
    }
    static char temperatureTemp[7];
    dtostrf(temperature, 4, 2, temperatureTemp);
    Serial.println(temperatureTemp);

    static char humidityTemp[7];
    dtostrf(humidity, 4, 2, humidityTemp);
    Serial.println(humidityTemp);

    client.publish("2041720230/room/lamp", temperatureTemp);  // agar lebih unix silakan tambahkan NIM ex: 0001/room/suhu
    client.publish("2041720230/room/humidity", humidityTemp); // agar lebih unix silakan tambahkan NIM ex: 0001/room/suhu
  }
}
```

3. Tambah node chart agar dapat menampilkan nilai kelembaban, node chart masih dalam satu group yaitu Room pada dashboard Node-RED.

Jawab : <br/>
<img src="Kelompok 1/prak2_p2.png" width="500px">

<br/>
<br/>
<br/>

# TUGAS

Buatlah sebuah dashboard website untuk memonitoring dan control pada sebuah ruang lobby, ruang kajur, dan ruang dosen. Masing-masing ruang dengan detail node yang dibutuhkan pada node dashboard sebagai berikut;

1. Tab Home terdiri dari group Control, Monitoring, dan Cahaya.

- Group Control memiliki 3 node switch dan 3 text statis, fungsi dari group ini adalah untuk menghidupkan dan mematikan led RGB.
- Group Monitoring 2 node chart untuk menampilkan suhu dan kelembaban.
- Group Cahaya terdiri dari text dan gauge, text untuk menampilkan kategori terang, redup, dan gelap. Sedangkan node gauge untuk menampilkan nilai sensor LDR.

2. Tab Contact Pada tab ini digunakan untuk menampilkan data kelas, NIM, dan Nama. Silakan diisi dengan nama Anda masing-masing.

### Jawaban

Kode Program :

```c++

#include <Arduino.h>
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
#include <SimpleDHT.h>

const char *ssid = "Araspot";                 
const char *password = "yondatau";            
const char *mqtt_server = "broker.hivemq.com"; 

const int redPin = D5;  
const int greenPin = D6; 
const int bluePin = D2;  

bool isRedOn = false;  
bool isGreenOn = false;
bool isBlueOn = false; 

WiFiClient espClient;
PubSubClient client(espClient);

SimpleDHT11 dht11(D7);

long now = millis();
long lastMeasure = 0;
String macAddr = "";

#define sensorLDR A0

int nilaiSensor;

void setup_wifi()
{
  delay(10);
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.print("WiFi connected - ESP IP address: ");
  Serial.println(WiFi.localIP());
  macAddr = WiFi.macAddress();
  Serial.println(macAddr);
}

void reconnect()
{
  while (!client.connected())
  {
    Serial.print("Attempting MQTT connection...");
    if (client.connect(macAddr.c_str()))
    {
      Serial.println("connected");
      client.subscribe("2041720230/room/led");
    }
    else
    {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      delay(5000);
    }
  }
}

void handleLedControl(char *payload, int length)
{

  String message = "";
  for (int i = 0; i < length; i++)
  {
    message += (char)payload[i];
  }

  if (message.equals("red_on"))
  {
    digitalWrite(redPin, HIGH);
    isRedOn = true;
  }
  else if (message.equals("red_off"))
  {
    digitalWrite(redPin, LOW);
    isRedOn = false;
  }
  else if (message.equals("green_on"))
  {
    digitalWrite(greenPin, HIGH);
    isGreenOn = true;
  }
  else if (message.equals("green_off"))
  {
    digitalWrite(greenPin, LOW);
    isGreenOn = false;
  }
  else if (message.equals("blue_on"))
  {
    digitalWrite(bluePin, HIGH);
    isBlueOn = true;
  }
  else if (message.equals("blue_off"))
  {
    digitalWrite(bluePin, LOW);
    isBlueOn = false;
  }
}

void callback(char *topic, byte *payload, int length)
{

  if (String(topic) == "2041720230/room/led")
  {
    handleLedControl((char *)payload, length);
  }
}

void setup()
{
  Serial.begin(115200);
  Serial.println("Mqtt Node-RED");
  setup_wifi();
  client.setServer(mqtt_server, 1883);

  client.setCallback(callback);

  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  digitalWrite(redPin, LOW);
  digitalWrite(greenPin, LOW);
  digitalWrite(bluePin, LOW);
}

void loop()
{
  if (!client.connected())
  {
    reconnect();
  }
  if (!client.loop())
  {
    client.connect(macAddr.c_str());
  }
  now = millis();
  if (now - lastMeasure > 5000)
  {
    lastMeasure = now;
    int err = SimpleDHTErrSuccess;

    byte temperature = 0;
    byte humidity = 0;
    if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess)
    {
      Serial.print("Pembacaan DHT11 gagal, err=");
      Serial.println(err);
      delay(1000);
      return;
    }

    static char temperatureTemp[7];
    dtostrf(temperature, 4, 2, temperatureTemp);
    Serial.println(temperatureTemp);

    static char humidityTemp[7];
    dtostrf(humidity, 4, 2, humidityTemp);
    Serial.println(humidityTemp);

    nilaiSensor = analogRead(sensorLDR);

    static char nurTemp[7];
    dtostrf(nilaiSensor, 4, 2, nurTemp);
    Serial.println(nurTemp);

    client.publish("2041720230/room/temp", temperatureTemp);  
    client.publish("2041720230/room/humidity", humidityTemp);
    client.publish("2041720230/room/nur", nurTemp);           
  }
}

```

Dokumentasi Hasil : 


