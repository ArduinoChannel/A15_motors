# A15_motors
библиотека для работы с H-мостовыми драйверами моторов!

## подключение, объекты
```cpp
#include <A15_motors.h>

A15_motors motors(rf, rb, lf, lb);  //для "релейного" управления моторами
A15_motors_PWM motors(enable, rf, rb, lf, lb);  //для плавного управления моторами
A15_relay relay(in);  //для реле
```
## функции
```cpp
/*---функции A15Motors и A15Motors_PWM---*/
setSpeed(speed);               //настройка скорости, 0 - 255
manualGo(rf1, rb1, lf1, lb1);  //вручную
go(direction);                 //резкий старт по константам
brake();                       //тормозим
setSmooth(smooth);             //настройка плавности
smoothGo(directionSmooth);     //плавный старт по константам
smoothBrake(directionSmooth);  //плавное торможение
/*---функции A15Relay---*/
work(period);                  //инвертирует состояние пина с заданным интервалом
stop();                        //останавливает работу
```
## константы
```cpp
FW  //вперёд
BW  //назад
R   //"танковый разворот" вправо
L   //"танковый разворот" влево
RF  //вперёд и вправо
LF  //вперёд и влево
RB  //назад и вправо
LB  //назад и влево
```
## пример
```cpp
#include <A15_motors.h>

A15_motors motors(6, 9, 10, 11);

void setup(){
  motors.setSpeed(180);
  motors.setSmooth(5);
}

void loop(){
  for(int i = 0; i < 4; i++){
    motors.smoothGo(FW);
    motors.smoothBrake(FW);
    motors.smoothGo(L);
    motors.smoothBrake(L);
  }
}
```
