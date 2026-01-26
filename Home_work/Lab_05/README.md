
# Лабораторная работа. Доступ к сетевым устройствам по протоколу SSH
### Дано:
###	Топология
![](./images/lab_05_fig_01.png)
###	Таблица адресации
|Устройство  |Интерфейс  |IP-адрес     |Маска подсети|Шлюз по умолчанию|
|------------|-----------|-------------|-------------|-----------------|
|R1          |G0/0/1     | 192.168.1.1 |255.255.255.0|-
|S1          |VLAN 1     | 192.168.1.11|255.255.255.0|192.168.1.1      |
|PC-A        |NIC        | 192.168.1.3 |255.255.255.0|192.168.1.1      |
### Задание:
1. [Часть 1. Настройка основных параметров устройства.]()
   - [Шаг 1. Создайте сеть согласно топологии.]()
   - [Шаг 2. Выполните инициализацию и перезагрузку маршрутизатора и коммутатора.]()
   - [Шаг 3. Настройте маршрутизатор.]()
   - [Шаг 4.]()
   - [Шаг 5.]()
2. [Часть 2.]()
   - [Шаг 1.]()
   - [Шаг 2.]()
   - [Шаг 3.]()
   - [Шаг 4.]()
   - [Шаг 5.]()
   - [Шаг 6.]()
3. [Часть 3.]()
   - [Шаг 1.]()
   - [Шаг 2.]()
   - [Шаг 3.]()
4. [Часть 4.]()
   - [Шаг 1.]()
   - [Шаг 2.]()
5. [Вопросы для повторения](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D0%B2%D0%BE%D0%BF%D1%80%D0%BE%D1%81%D1%8B-%D0%B4%D0%BB%D1%8F-%D0%BF%D0%BE%D0%B2%D1%82%D0%BE%D1%80%D0%B5%D0%BD%D0%B8%D1%8F)
6. Файлы Cisco Packet Tracer
   - [Основной файл домашнего задания](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/pkt/lab_01.pkt)
   - [Файл Приложения А](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/pkt/lab_01_appendix_a.pkt)


## Часть 1. Настройка основных параметров устройства.
###  Шаг 1. Создайте сеть согласно топологии.
![](./images/lab_05_fig_02.png)
###  Шаг 2. Выполните инициализацию и перезагрузку маршрутизатора и коммутатора.
- Маршрутизатор
```
Router>enable
Router#erase startup-config 
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]y[OK]
Erase of nvram: complete
%SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
Router#delete vlan.dat
Delete filename [vlan.dat]?y
Delete flash:/y? [confirm]y%Error deleting flash:/y (No such file or directory)
Router#reload
Proceed with reload? [confirm]yInitializing Hardware ...
```
###  Шаг 3. Настройте маршрутизатор.
a.	Подключитесь к маршрутизатору с помощью консоли и активируйте привилегированный режим EXEC.
```

```
