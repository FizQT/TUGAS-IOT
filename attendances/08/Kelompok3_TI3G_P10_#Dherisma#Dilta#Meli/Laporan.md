## PRAKTIKUM IOT PERTEMUAN 10 TI-3G
### Kelompok 3 TI-3G:
Nama anggota : <br>
1. Dherisma Hanindita Utami (07)
2. Dilta Febiana (08)
3. Meliusa Nora Hariyanti (13)

# SOCKET SERVER CLIENT
## Praktikum 1
        '''import socket
from threading import Thread


# Multithreaded Python server
class ClientThread(Thread):

    def _init_(self, ip, port):
        Thread._init_(self)
        self.ip = ip
        self.port = port
        print("Incoming connection from " + ip + ":" + str(port))

    def run(self):
        while True:
            try:
                data = conn.recv(2048)
                if len(data) == 0:
                    break

                print("length: " + str(len(data)))
                print("Server received data:", data)
                # MESSAGE = input("Input response:")
                MESSAGE = "OK"
                conn.send(MESSAGE.encode("utf8"))  # echo
            except Exception as e:
                print(e)
                break
                TCP_IP = "0.0.0.0"
                TCP_PORT = 2004 
                BUFFER_SIZE = 20 
                tcpServer = socket.socket(socket.AF_INET, socket.SOCK_STREAM) tcpServer.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
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

hasil

<image src= "1.jpeg">
<image src= "2.jpeg">
<image src= "3.jpeg">

outputan 

<image src= "4.jpeg">

## Praktikum 2
Code Program


    #include <Arduino.h>
    #include <ESP8266WiFi.h>

    #define LED D4

    const char *ssid = "iPhone Meliusa"; // nama SSID untuk koneksi Anda
    const char *password = "anuanuanu"; // password akses point WIFI Anda
    const uint16_t port = 8080; // diganti dengan port serve Anda
    const char *host = "182.1.117.172";//diganti dengan host server Anda, bisa ip ataupun domain

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
    
Output :
<image src= "5.jpeg">