# <b>LAPORAN PRAKTIKUM  
# Anggota Kelompok
1. Gustania Nirmala Meisi (10)
2. Rosis Hudaya Putra (16)
3. Safira Istifarini (17)<br>

# <b>PRAKTIKUM PERTEMUAN 15

## <b>Praktikum <br>
### <b>Konfigurasi Message Broker<br>
1. Download terlebih dahulu pada link berikut ```https://mosquitto.org/download/```.
2. Lakukan installasi sampai selesai
3. Agar perintah mosquitto bisa dikenali perlu didaftarkan (path) terlebih dahulu
4. Secara default folder installasi terdapat di C:\Program Files\mosquitto, sehingga kita perlu mendaftarkan folder tersebut pada path environment
5. Ketik kembali perintah mosquitto pada Windows PowerShell, seharusnya outputnya berbeda dari yang sebelumnya artinya message broker sudah berjalan.
### <b>Menambahkan Password MQTT<br>

1. Buatlah sebuah user jti dengan perintah di bawah ini. User jti hanya contoh, silakan diganti dengan yang lain jika diperlukan

```c 
ubuntu@ip-172-31-16-8:~$ sudo mosquitto_passwd -c /etc/mosquitto/passwd jti
Password:
Reenter password:
```

2. Buatlah file konfigurasi yang menginfokan bahwa untuk publish tidak dizinkan tanpa password. Ketik perintah di bawah ini

    ```sudo nano /etc/mosquitto/conf.d/jti.conf```

Akan muncul editor nano, selanjutnya tambahkan dua baris perintah berikut

```c
listener 8090
protocol websockets

listener 1883
#protocol websockets

per_listener_settings true
allow_anonymous false
password_file /etc/mosquitto/passwd
```

3. Tekan CTRL+O untuk menyimpan konfigurasi file dan CTRL+X untuk keluar dari editor nano.<br>
Untuk sistem operasi Windows, file konfigurasi terdapat di 

    ```C:\Program Files\mosquitto\mosquitto.conf.``` 

4. Silakan restart mosquitto untuk memberikan perubahan dan coba lakukan publish atau subscribe sebuah message, kira-kira perintahnya adalah sebagai berikut:<br>

    ```sudo systemctl restart mosquitto```<br>

    Untuk sistem operasi windows, silakan sesuaian konfigurasi seperti berikut ini, jika jalankan menggunakan perintah ```mosquitto -c .\mosquitto.conf.``` File konfigurasi bisa diletakkan di folder manapun.

```c
listener 8090
protocol websockets

listener 1883
protocol mqtt

per_listener_settings true
allow_anonymous false
password_file pwfile
```

## <b>Hasil <br>

<img src = "kelompok04\per1.jpeg" width="500px">

## <b>Pertanyaan <br>
1. Apakah fungsi dari baris perintah protocol websockets pada file konfig mosquitto?
2. Silakan ganti menjadi false pada per_listener_settings true, restart mosquitto. Apakah yang akan terjadi atau pengaruhnya apa?
3. Buatlah user yang lain, kemudian lakukan subscribe dan publish message!

## <b>Jawaban <br>

1. Baris perintah protocol websockets pada file konfigurasi Mosquitto digunakan untuk mengaktifkan atau menonaktifkan dukungan protokol WebSocket pada broker Mosquitto.<br><br>
Protokol WebSocket memungkinkan klien untuk berkomunikasi dengan broker menggunakan koneksi dua arah secara real-time melalui protokol HTTP yang sudah ada. Dengan mengaktifkan protokol websockets, klien dapat menggunakan koneksi websockets untuk berinteraksi dengan broker MQTT.

2. Jika mengubah nilai per_listener_settings menjadi false pada konfigurasi Mosquitto dan kemudian me-restart Mosquitto, maka pengaruhnya adalah fitur per-listener settings akan dinonaktifkan.<br><br>
Fitur per-listener settings memungkinkan untuk mengonfigurasi pengaturan yang berbeda untuk setiap pendengar (listener) yang ditetapkan pada broker Mosquitto. Dengan mengatur per_listener_settings menjadi false, semua pendengar akan menggunakan pengaturan yang sama.

3. <img src = "kelompok04\prak1.PNG" width="500px">

### <b>Menghubungkan Smart Device Aplikasi Web <br>
1. Tambahkan kode program pada Node-MCU, dibutuhkan DHT11. Kode programnya adalah sebagai berikut :
```C
#include <Arduino.h>
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
#include <SimpleDHT.h>

// hp
// const char *ssid = "od3ng";
// const char *password = "0d3n9bro";

// kampus
const char *ssid = "Smart Parking";            // sesuaikan dengan username wifi
const char *password = "5m4rT_P4rk!Ng";        // sesuaikan dengan password wifi
const char *mqtt_server = "broker.hivemq.com"; // isikan server broker

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

    client.publish("room/suhu", temperatureTemp); // agar lebih unix silakan tambahkan NIM ex: 0001/room/suhu
}
}
```
2. Edit file atau buat file index.html yang terdapat di /var/www/html/index.html menggunakan file seperti di bawah ini : 

```c
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JTI IoT</title>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/paho-mqtt/1.0.1/mqttws31.min.js" type="text/javascript"></script>
    <script type="text/javascript">
        var MQTTbroker = '****';//servernya disesuaikan
        var MQTTport = ****; //sesuaikan port websockets messsage broker,
        var MQTTsubTopic = '****'; //topiknya perlu disesuaikan
        var chart; // global variuable for chart
        var dataTopics = new Array();
        //mqtt broker
        var client = new Paho.MQTT.Client(MQTTbroker, MQTTport, "jti_" + parseInt(Math.random() * 100, 10));
        client.onMessageArrived = onMessageArrived;
        client.onConnectionLost = onConnectionLost;

        //mqtt connecton options including the mqtt broker subscriptions
        var options = {
            userName: "****",//silakan disikan username dan password yang didaftarkan mqtt
            password: "****",
            timeout: 3,
            useSSL: false,
            onSuccess: function() {
                console.log("mqtt connected");
                // Connection succeeded; subscribe to our topics
                client.subscribe(MQTTsubTopic, {
                    qos: 1
                });
            },
            onFailure: function(message) {
                console.log("Connection failed, ERROR: " + message.errorMessage);
                //window.setTimeout(location.reload(),20000); //wait 20seconds before trying to connect again.
            }
        };
        //can be used to reconnect on connection lost
        function onConnectionLost(responseObject) {
            console.log("connection lost: " + responseObject.errorMessage);
            //window.setTimeout(location.reload(),20000); //wait 20seconds before trying to connect again.
        };
        //what is done when a message arrives from the broker
        function onMessageArrived(message) {
            console.log(message.destinationName, '', message.payloadString);
            //check if it is a new topic, if not add it to the array
            if (dataTopics.indexOf(message.destinationName) < 0) {

                dataTopics.push(message.destinationName); //add new topic to array
                var y = dataTopics.indexOf(message.destinationName); //get the index no

                //create new data series for the chart
                var newseries = {
                    id: y,
                    name: message.destinationName,
                    data: []
                };
                chart.addSeries(newseries); //add the series
            };

            var y = dataTopics.indexOf(message.destinationName); //get the index no of the topic from the array
            var myEpoch = new Date().getTime(); //get current epoch time
            var thenum = message.payloadString.replace(/^\D+/g, ''); //remove any text spaces from the message
            var plotMqtt = [myEpoch, Number(thenum)]; //create the array
            if (isNumber(thenum)) { //check if it is a real number and not text
                console.log('is a propper number, will send to chart.')
                plot(plotMqtt, y); //send it to the plot function
            };
        };
        //check if a real number
        function isNumber(n) {
            return !isNaN(parseFloat(n)) && isFinite(n);
        };
        //function that is called once the document has loaded
        function init() {
            //i find i have to set this to false if i have trouble with timezones.
            Highcharts.setOptions({
                global: {
                    useUTC: false
                }
            });
            // Connect to MQTT broker
            client.connect(options);
        };
        //this adds the plots to the chart
        function plot(point, chartno) {
            console.log(point);

            var series = chart.series[0],
                shift = series.data.length > 20; // shift if the series is
            // longer than 20
            // add the point
            chart.series[chartno].addPoint(point, true, shift);
        };
        //settings for the chart
        $(document).ready(function() {
            chart = new Highcharts.Chart({
                chart: {
                    renderTo: 'container',
                    defaultSeriesType: 'spline'
                },
                title: {
                    text: 'Dashboard IoT JTI - Suhu Live Websockets'
                },
                subtitle: {
                    text: 'broker: ' + MQTTbroker + ' | port: ' + MQTTport + ' | topic : ' + MQTTsubTopic
                },
                xAxis: {
                    type: 'datetime',
                    tickPixelInterval: 150,
                    maxZoom: 20 * 1000
                },
                yAxis: {
                    minPadding: 0.2,
                    maxPadding: 0.2,
                    title: {
                        text: 'Value',
                        margin: 80
                    }
                },
                series: []
            });
        });
    </script>
    <script src="http://code.highcharts.com/stock/highstock.js"></script>
    <script src="http://code.highcharts.com/stock/modules/exporting.js"></script>
</head>

<body onload="init();">
    <!--Start the javascript ball rolling and connect to the mqtt broker-->
    <div id="container" style="height: 500px; min-width: 500px"></div><!-- this the placeholder for the chart-->
</body>

</html>
```
3. Upload kode tersebut ke server, bisa menggunakan WinSCP atau ketika sudah menggunakan repository berarti perlu push ke repo selanjutnya yang di server perlu dilakukan pull

## <b>Hasil <br>

<img src = "kelompok04\per1.jpeg" width="500px">

## <b>Pertanyaan<br>
1. Berapa lama sekali pengiriman data sensor DHT dari Node-MCU ke server broker? Silakan diubah menjadi lebih cepat!
2. Fungsi baris perintah dtostrf(temperature, 4, 2, temperatureTemp); digunakan untuk apa? Jelaskan!
3. Modifikasi bentuk chart pada halaman index.html dalam bentuk yang lain, misalkan chart bar ataupun gauge!

## <b>Jawaban<br>

1. <img src = "kelompok04\prak1.PNG" width="500px">

2. Fungsi `dtostrf(temperature, 4, 2, temperatureTemp)` digunakan untuk mengkonversi nilai bilangan floating-point (misalnya suhu) menjadi string dalam format yang ditentukan. Berikut adalah penjelasan dari parameter fungsi `dtostrf`:

- `temperature`: Nilai suhu (floating-point) yang akan dikonversi menjadi string.
- `4`: Jumlah digit yang ingin disertakan dalam hasil string. Angka ini termasuk digit desimal dan karakter null-terminating ('\0').
- `2`: Jumlah digit desimal yang ingin disertakan dalam hasil string.
- `temperatureTemp`: Nama variabel string yang akan menampung hasil konversi.

Jadi, dalam contoh tersebut, nilai suhu akan dikonversi menjadi string dengan 4 digit (termasuk digit desimal) dan 2 digit desimal setelah koma. Hasil konversi akan disimpan dalam variabel `temperatureTemp`. Dengan demikian, `temperatureTemp` akan berisi string yang merepresentasikan nilai suhu dengan format yang sesuai.

3. <img src = "kelompok04\prak1.PNG" width="500px">

## <b>Tugas<br>

Buatlah sebuah tampilan website yang fungsi utama adalah untuk menampilkan sensor cahaya, suhu, dan kelembaban. Kemudian Dapat juga menghidupkan masing-masing LED RGB, website tersebut harus telah teruplod di OCI(lampirkan alamatnya pada laporan praktikum) dan videokan hasilnya.

## <b>Hasil <br>

Video dokumentasi tugas [klik disini](https://drive.google.com/file/d/1QjFIUHo-r-LOkSajcPMNN1sXbPMuQtET/view?usp=sharing)




