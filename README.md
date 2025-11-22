# Reporte 4 ESP32 con sensor ultrasonico

Programación de un ESP32 con un sensor ultrasónico HC-SR04 y una pantalla LCD 16x2(I2C)
## Introducción
### Descripción
Utilizaremos l plataforma WOKWI para simular la adquisición de datos de distancia mediante un sensor ultrasónico HC-SR04 y la prorgramación del mismo en un microcontrolador ESP32, los datos se mostrarán en una pantalla LCD

### Material Necesario 
Para realizar esta practica necesitas lo siguiente

a. Plataforma WOKWI

b. Tarjeta ESP 32

c. Sensor ultrasónico HC-SR04

d. Pantalla LCD 16x2(I2C)

## Instrucciones
### Previo
1. Abrir la plataforma WOKWI.

### Preparación
2. Ir a la pestaña de sketch.ino y borrar el codigo e programación predeterminado
3. Abrir la terminal de programación y colocar la siguente programación:
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor

DHTesp dhtSensor;

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
  lcd.clear();
  lcd.setCursor(3, 0);
  lcd.print("Bienvenidos");
  lcd.setCursor(2, 1);
  lcd.print("al Modulo 5");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 1);
  lcd.print("David Mejia");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia:");
  lcd.print(d);
  lcd.setCursor(14, 0);
  lcd.print("cm");
 
  delay(1000);
}
```




4. Ir a la pestaña "Library manager" haer clic sobre el icon "+", buscar la libreria "HCSR04 ultrasonic sensor" y agregarla
![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/libreria%20sensor%20ultrasonico.png?raw=true)

5. De igual manera agregar la libreria "LiquidCrystal I2C" para la pantalla LCD

![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/Libreria%20Pantalla%20LCD%20Liquid%20cristal.png?raw=true)

7. Ir al esquema de simulacón, dar clic al icono "+ (add new part)"

![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/Add%20new%20part.png?raw=true)

6. Buscar el sensor HCSR04 y agregar

![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/Add%20new%20part%203.png?raw=true)

7. De igual manera buscar la pantalla LCD 16x2(I2C) y agregar
   
8. Colocar el sensor y la pantalla sobre el esquema de simulación y conectar como indica la figura de abajo

![]<img width="677" height="492" alt="image" src="https://github.com/user-attachments/assets/695d1f5e-4a1a-44d8-b554-aedfdf3528dd" />)

## Operación
9. Iniciar simulador dando clic en el icono "play"

![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/play.png?raw=true)

10. Visualizar los datos en el monitor serial.

## Resultados
Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.
![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/resultado%20sensor%20ultrasonico%203.png?raw=true)
![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/resultado%20sensor%20ultrasonico%202.png?raw=true)
![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/resultado%20sensor%20ultrasonico%201.png?raw=true)

## Créditos
Ralizado por el Ingeniero David Mejía
