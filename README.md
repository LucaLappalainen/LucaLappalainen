# IoT
## 14.9.2022
### projektisuunnitelma
#### Luca Lappalainen, Peetu Vainio ja Joel Utriainen
kokeiltiin arduinolla kaikenlaista  
-7 segment display  
-8x8 led matrix  
-lämpötila näkymään 7 segment displaylle (ei saatu toimimaan)  
-mikki  
-ultrasonic distance sensor ( ei saatu toimimaan) 


## 15.9.2022
Vaihettu Hostname raspberry pi käyttöjärjestelmään  
-Ohjeet: https://www.tomshardware.com/news/raspberry-pi-web-server,40174.html  
Tietokannan ja taulukon tekeminen:  

sudo mariadb =avaa tietokanta palvelun  
CREATE DATABASE SRYHMA; =Luo tietokannan  
USE SRYHMA =Avaa tietokannan  
CREATE TABLE Liike (id int AUTO_INCREMENT NOT NULL PRIMARY KEY, arvo boolean, aika datetime); =luo taulukon  
SELECT * FROM Liike; =Näyttää taulukon sisällön  
INSERT INTO Liike (arvo, aika) VALUES (true,now()); =Lisää annetut arvot taulukkoon  
SELECT * FROM Liike; =Näyttää taulukon sisällön  
INSERT INTO Liike (arvo, aika) VALUES (false,now()); =Lisää annetut arvot taulukkoon  
SELECT * FROM Liike; =Näyttää taulukon sisällön  
ctrl c =poistuu tietokanta palvelusta  

sudo mariadb  
CREATE DATABASE SRYHMA_Luca;  
USE SRYHMA_Luca  
CREATE TABLE Liike_Luca (id int AUTO_INCREMENT NOT NULL PRIMARY KEY, arvo boolean, aika datetime);  
SELECT * FROM Liike_Luca;  
INSERT INTO Liike_Luca (arvo, aika) VALUES (true,now());  
SELECT * FROM Liike_Luca;  
INSERT INTO Liike_Luca (arvo, aika) VALUES (false,now());  
SELECT * FROM Liike_Luca;  


## 16.9.2022
Testailtu Ardunoa raspberryn kanssa  

lataa arduino IDE Raspiin  
Terminal:  
-Sudo apt install arduino =Lataa arduinon  
-Sudo adduser käyttäjänimi dialout  
pyserial_kirjasto  
-pip install pyserial / sudo pip3 install pyserial  
apt list --installed -> python3-serial  

Testataan toimiiko Arduino IDE oikein:  
-Simppeli koodi (Serial)  
-Arduino UNO  
-Com-port  
^
/dev/ttyACM0  
/dev/ttyUSB0  

Laitettu Arduino ja Python koodit raspiin  
Arduino:  

void setup() {  
  // put your setup code here, to run once:  
Serial.begin(9600);  
}  

void loop() {  
  // put your main code here, to run repeatedly:  
Serial.println("Heippa");  
delay(100);  
}  

Python:  

#!/usr/bin/env python3  
#kirjasto  
import serial  

if __name__ == '__main__':  
    #serialin kommunikaatioon alustamisseen kutsutaan muutamilla parametreillä  
    ser = serial.Serial('/dev/ttyACM0', 9600, timeout=1)  
    ser.reset_input_buffer()  

    while True:  
        if ser.in_waiting > 0:  
            line = ser.readline().decode('utf-8').rstrip()  
            print(line)  

Välkkyvä LED valo, joka on yhdistetty ardunosta serialiin  
-Ohjeet: https://forum.arduino.cc/t/blinking-an-led-from-a-raspberry-pi-gpio-signal/695120  

Testattiin Servo moottoria (ei saatu toimimaan)  


## 21.9.2022
Tutustuttiin eri KTinker komentoihin pythonilla ja aloitettiin suomenlipun koodin tekemistä  
#### Esimerkkikoodi
import tkinter as tk = tunnistaa- tkinterin tk:na ja sitä rataa loputkin = koodit window = tk. Tk() lb=tk.Label(text="real python")= Tekstiksi tulee se, mitä suluissa lukee entry = tk.Entry()  
name=entry.get() = nimeksi tulee se, minkä kirjoitat = name lb.pack() = mahdollistaa lb:n käytön entry.pack()= mahdollistaa entryn käytön  
window.mainloop()  

## 22.9.2022
#### Tehtävä 1
A)Miten tietokantapalvelimella?  
SHOW DATABASES;  
B)Miten tietokantataulukko on muodostettu?  
DESCRIBE tbl_name  
#### Tehtävä 2
Loopissa ei kovakoodattua sisältöä, 3kpl esimerkkejä sql stringin muokkaamisesta %, format() ja f-string  
 import time  
 import datetime  
 import mariadb  
 import PRi.GPIO as GPIO  
 
 InputPin = 23  
 
 GPIO.setmode(GPIO.SCM)  
 GPIO.setup(InputPin, GPIO.IN  
 
 conn = mariadb.connect(user="root", password="Jopee31v", host="localhost", database="SRYHMA")  
 cur = conn.cursor()  
 waitloop = 5  
 print(datetime. datetime. now(1)  
 
 try:  
  while True:  
    sql5tr = "INSERT INTO Liike (arvo, aika) VALUES (5, now())"  
    sql5trPercentage = "INSERT INTO Liike (arvo, aika) VALUES (%s, %s)" %(GPIO.input(InputPin), datetime.datetime.now())  
    sql5trFormat = "INSERT INTO Liike (arvo, aika) VALUES ({},{})" .format(GPIO.input(InputPin),datetime.datetime.now())  
    sql5trF = f"INSERT INTO Liike (arvo, aika) VALUES ({GPIO.input(InputPin)}, now())  
   
    print("A: ", sql5tr)  
    print("B: ", sql5trPercentage)  
    print("C: ", sql5trFormat)  
    print("D: ", sql5trF)  
   
    time.sleep(waitloop)  
    cur.execute(sqlStrF)  
    conn.commit()  
except:  
  print("ei toimi")  
  time.sleep(waitloop)  
  window.mainloop()  
#### Tehtävä 3
DHT11 harjoitus  

## 23.9.2022
Suunniteltiin käyttöliittymää ja tehtiin sille graafinen ohjelmisto, saatiin myös projekti valmiiksi, joka aloitettiin 21-päivä, ja missä frame koodien avulla saatiin aikaiseksi suomenlippu  
#### Koodi
import tkinter as tk  

window = tk.Tk() = luo tyhjän ruudun  

frame123 = tk.Frame(master=window, width=50, height=50, bg="blue") = tekee framen ja sen korkeuden, leveyden ja värin  
frame123.pack(side=tk.RIGHT) = mahdollistaa framen käytön ja asettelee sen ruutuunsa  
frame134 = tk.Frame(master=window, width=50, height=50, bg="blue")  
frame134.pack(side=tk.RIGHT)  
frame145 = tk.Frame(master=window, width=50, height=50, bg="blue")  
frame145.pack(side=tk.LEFT)  
frame156 = tk.Frame(master=window, width=50, height=50, bg="blue")  
frame156.pack(side=tk.RIGHT)  
frame167 = tk.Frame(master=window, width=50, height=50, bg="blue")  
frame167.pack()  
frame177 = tk.Frame(master=window, width=50, height=50, bg="blue")  
frame177.pack()  
frame1 = tk.Frame(master=window, width=50, height=50, bg="blue")  
frame1.pack()  


## 28.9.2022
Tehtiin html:llää

## 29.9.2022
-käytiin läpi mitä kieliä ollaan tähän asti käytetty  
-koodattiin php:tä  
-Tehtiin PIR liikeanturi toimivaksi  
-Tehtiin index.html sivu  
-Tehtiin meille jokaiselle omat php sivut  
-Linkitettiin meidän php sivut html sivuun  
-saatiin omista tietokannoista taulukot toimimaan php sivuille  

## 3. - 14.10.2022
video projekti tai lukio-opintoja
