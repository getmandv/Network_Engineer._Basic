# Лабораторная работа - Реализация DHCPv4.
### Дано:
### Топология:
![](./images/lab_08_fig_01.png)
### 1.Таблица адресации:
|Устройство|Интерфейс  |IP-адрес    |Маска подсети  |Шлюз по умолчанию|
|----------|-----------|------------|---------------|-----------------|
|R1        |G0/0/0     |10.0.0.1    |255.255.255.252|-                |
|R1        |G0/0/1     |-           |-              |-                |
|R1        |G0/0/1.100 |192.168.1.1 |255.255.255.192|-                |
|R1        |G0/0/1.200 |192.168.1.65|255.255.255.224|-                |
|R1        |G0/0/1.1000|-           |-              |-                |
|R2        |G0/0       |1.0.0.2     |255.255.255.252|-                |
|R2        |G0/0/1     |192.168.1.97|255.255.255.240|                 |
|S1        |VLAN 200   |192.168.1.66|255.255.255.224|192.168.1.65     |
|S2        |VLAN 1     |            |               |                 |
|PC-A      |NIC        |DHCP        |DHCP           |DHCP             |
|PC-B      |NIC        |DHCP        |DHCP           |DHCP             |
### 2. Таблица VLAN:
|VLAN|Имя         |Назначенный интерфейс      |
|----|------------|---------------------------|
|1   |Нет         |S2: F0/18                  |
|100 |Клиенты     |S1: F0/6                   |
|200 |Управление  |S1: VLAN 200               |
|999 |Parking_Lot |S1: F0/1-4, F0/7-24, G0/1-2|
|1000|Собственная |-                          |
### Задание:
1. [Часть 1. Создание сети и настройка основных параметров устройства.]()
2. [Часть 2. Настройка и проверка двух серверов DHCPv4 на R1.]()
3. [Часть 3. Настройка и проверка DHCP-ретрансляции на R2.]()
4. Файлы Cisco Packet Tracer
   - [Основной файл домашнего задания](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_07/pkt/lab_07.pkt)
## Часть 1. Часть 1.	Создание сети и настройка основных параметров устройства.
###  Шаг 1.	Создание схемы адресации.
Подсеть сети 192.168.1.0/24 в соответствии со следующими требованиями:
- a.	Одна подсеть «Подсеть A», поддерживающая 58 хостов (клиентская VLAN на R1).

Подсеть A: *192.168.1.0 255.255.255.192*

Запишите первый IP-адрес в таблице адресации для R1 G0/0/1.100: *192.168.1.1*
- b.	Одна подсеть «Подсеть B», поддерживающая 28 хостов (управляющая VLAN на R1).

Подсеть B: *192.168.1.64 255.255.255.224*

Запишите первый IP-адрес в таблице адресации для R1 G0/0/1.200: *192.168.1.65*

Запишите второй IP-адрес в таблице адресов для S1 VLAN 200: *192.168.1.66*

Введите соответствующий шлюз по умолчанию: 192.168.1.65
- c.	Одна подсеть «Подсеть C», поддерживающая 12 узлов (клиентская сеть на R2).

Подсеть C: *192.168.1.96 255.255.255.240*

Запишите первый IP-адрес в таблице адресации для R2 G0/0/1: *192.168.1.97*
### Шаг 2.	Создайте сеть согласно топологии.
![](./images/lab_08_fig_02.png)
### Шаг 3.	Произведите базовую настройку маршрутизаторов.
- a.	Назначьте маршрутизатору имя устройства.
- b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
- c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
- d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
- e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
- f.	Зашифруйте открытые пароли.
- g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
- h.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
- i.	Установите часы на маршрутизаторе на сегодняшнее время и дату
```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1
R1(config)#no ip domain-lookup
R1(config)#enable secret class
R1(config)#line con 0
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#exit
R1(config)#line vty 0 15
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#exit
R1(config)#service password-encryption
R1(config)#banner motd #
Enter TEXT message.  End with the character '#'.
This is R1 router.
Authorized Users Only!#

R1(config)#exit
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#wr
Building configuration...
[OK]
R1#clock set 19:32:00 Mar 23 2026
R1#
```
*Данную настройку повторяем на маршрутизаторе R2.*
### Шаг 4.	Настройка маршрутизации между сетями VLAN на маршрутизаторе R1.
- a.	Активируйте интерфейс G0/0/1 на маршрутизаторе.
```
R1(config)#interface gigabitEthernet 0/0/1
R1(config-if)#no shutdown 

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1, changed state to up

R1(config-if)#
```
- b.	Настройте подинтерфейсы для каждой VLAN в соответствии с требованиями таблицы IP-адресации. Все субинтерфейсы используют инкапсуляцию 802.1Q и назначаются первый полезный адрес из вычисленного пула IP-адресов. Убедитесь, что подинтерфейсу для native VLAN не назначен IP-адрес. Включите описание для каждого подинтерфейса.
```
R1(config)#interface gigabitEthernet 0/0/1.100
R1(config-subif)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/1.100, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1.100, changed state to up

R1(config-subif)#description CLIENTS
R1(config-subif)#encapsulation dot1Q 100
R1(config-subif)#ip address 192.168.1.1 255.255.255.192
R1(config-subif)#exit
R1(config)#interface GigabitEthernet0/0/1.200
R1(config-subif)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/1.200, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1.200, changed state to up

R1(config-subif)#description Management
R1(config-subif)#encapsulation dot1Q 200
R1(config-subif)#ip address 192.168.1.65 255.255.255.224
R1(config-subif)#exit
R1(config)#interface GigabitEthernet0/0/1.1000
R1(config-subif)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/1.1000, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1.1000, changed state to up

R1(config-subif)#description Native
R1(config-subif)#encapsulation dot1Q 1000 native
R1(config-subif)#no ip address
R1(config-subif)#
```
- c.	Убедитесь, что вспомогательные интерфейсы работают.
```
R1#show ip interface brief 
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0/1   unassigned      YES unset  up                    up 
GigabitEthernet0/0/1.100192.168.1.1     YES manual up                    up 
GigabitEthernet0/0/1.200192.168.1.65    YES manual up                    up 
GigabitEthernet0/0/1.1000unassigned      YES unset  up                    up 
Vlan1                  unassigned      YES unset  administratively down down
R1#
```
### Шаг 5.	Настройте G0/1 на R2, затем G0/0/0 и статическую маршрутизацию для обоих маршрутизаторов.
