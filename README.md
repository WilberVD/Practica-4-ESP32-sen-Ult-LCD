# Practica #4 SENSOR ULTRASONICO CON LCD
Este repositorio muestra como podemos programar una ESP32 con el sensor Ultrasonico y una pantalla LCD.

## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```Ultrasonico```) para medir la distancia de un entorno; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- HC-SR04 Ultrasonic Distance Sensor
- LCD 16x2 (I2C)


## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).
![](https://github.com/WilberVD/PRACTICA-DHT/blob/main/woki.jpg)


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms
 
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " +String(d) + "cm  ");
  lcd.print("Wokwi Online IoT");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("ING.Wilber ");
  lcd.setCursor(0, 1);
  lcd.print("Industrial");
  delay(2000);
  lcd.clear();

}


```
2. Instalar la libreria  **DHT sensor library for ESPx** y **LiquidCrystal I2C** como se muestra en la siguente imagen.

![](https://github.com/WilberVD/PRACTICA-3-DHT11-CON-LCD/blob/main/libreria.jpg)

3. Hacer la conexion del **Ultrasonico** con la **ESP32** y la **Lcd**  como se muestra en la siguente imagen.

![](https://github.com/WilberVD/Practica-4-ESP32-sen-Ult-LCD/blob/main/4.2.jpg)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la temperatura y humedad dando *doble click* al sensor **Ultrasonico** 

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.

![](https://github.com/WilberVD/Practica-4-ESP32-sen-Ult-LCD/blob/main/4.3.jpg)


# Créditos

Desarrollado por Wilber Valladares Diaz

- [GitHub](WilberVD (github.com))
