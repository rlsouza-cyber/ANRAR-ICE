#include "WiFi.h"                   //Biblioteca WiFi
#include <HTTPClient.h>             //Biblioteca para conexão com a pagina da internet
#include <Adafruit_BMP280.h>        //Biblioteca do sensor BMP280
​
#define LED 2
#define SSid "PRISANTANA2307-4G"    //Nome da rede WiFi
#define Senha "946281448pr"         //Senha de acesso ao serviço WiFi
​
const char* serverName = "https://www.arduinomaker.com.br/iot001/add.php"; //Endereço do webservice
float temperatura = 0;
float pressao = 0;
int altitude = 0;
unsigned long tmpRefreshSensor = 0;
int intervaloSensor = 20000;
​
Adafruit_BMP280 bmp; // I2C
​
void setup() {
  Serial.begin(9600);
​
  pinMode(LED, OUTPUT);
  digitalWrite(LED, LOW);
​
  if (!bmp.begin(0x76)) {
    Serial.println(F("Não foi encontrado o sensor BMP280"));
    while (1) delay(10);
  }
 
  setupWiFi();
​
  //teste();
}
​
void loop() {
  sensor();
  delay(2000);
}
