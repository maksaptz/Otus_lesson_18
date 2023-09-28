# Vagrant-стенд c сетевой лабораторией

Описание домашнего задания:

## Цель и задачи домашнего задания:
Настроить хосты в соответсвии со схемой(см. network_map.png). 
Задание состоит из 2-х частей: теоретической и практической.


В теоретической части требуется: 
1) Найти свободные подсети;
2) Посчитать количество узлов в каждой подсети, включая свободные;
3) казать Broadcast-адрес для каждой подсети;
4) Проверить, нет ли ошибок при разбиении.


В практической части требуется: 
1) Соединить офисы в сеть согласно логической схеме и настроить роутинг;
2) Интернет-трафик со всех серверов должен ходить через inetRouter;
3) Все сервера должны видеть друг друга (должен проходить ping);
4) У всех новых серверов отключить дефолт на NAT (eth0), который vagrant поднимает для связи.


### Описание домашнего задания
Vagrntfile разворачивает следующие хосты:
1) inetRouter - маршрутизатор через который все хосты выходят в сеть.


Настройки:
- форвард пакетов ядро;
- сетевой экран и маскарад;
- маршруты в низлежащие сети.
2) centralRouter- центральный хост который соединяет все сети.


Настройки:
- форвард пакетов ядро;
- маршруты в низлежащие сети.
3) centralServer - сервер в сети centralRouter.


Настройки:
- маршрут по умолчанию.
4) office1Router - хост за которым находиться сеть 1 офиса.


Настройки:
- форвард пакетов ядро;
- маршрут в смежные сети.
5) office1Server - сервер в сети 1 офиса.


Настройки:
- маршрут по умолчанию.
6) office2Router - хост за которым находиться сеть 2 офиса.


  Настройки:
- форвард пакетов ядро;
- маршрут в смежные сети.
7) office2Server - сервер в сети 2 офиса.


Настройки:
- маршрут по умолчанию.

#### Ход выполнения
Для выполнения домашнего задания был настроен Vagrantfile который разворачивает хосты с готовыми сетевыми интерфейсами и запускает ansible для настройки машин.


Ansible использует 4 роли:
1) coreForward - включает на маршрутизаторах форвардинг пакетов в ядре;
2) nat - конфигурирует на inetRouter файрволл и маскарад;
3) routes - настраивает маршруты на всех хостах а также устанавливает traceroute на Ubuntu os
4) reboot - перезагружает хосты
