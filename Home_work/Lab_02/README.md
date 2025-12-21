# Лабораторная работа. Просмотр таблицы MAC-адресов коммутатора.
### Дано:
###	Топология
![](./images/lab_02_fig_01.png)
###	Таблица адресации
| Устройство | Интерфейс | IP-адрес     | Маска         |
|------------|-----------|--------------|---------------|
| S1         | VLAN 1    | 192.168.1.11 | 255.255.255.0 |
| S2         | VLAN 1    | 192.168.1.12 | 255.255.255.0 |
| PC-A       | NIC       | 192.168.1.1  | 255.255.255.0 |
| PC-B       | NIC       | 192.168.1.2  | 255.255.255.0 |
### Задание:
1. [Часть 1. Создание и настройка сети.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_02/README.md#%D1%87%D0%B0%D1%81%D1%82%D1%8C-1-%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%B8-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D1%81%D0%B5%D1%82%D0%B8)
   - [Шаг 1. Подключите сеть в соответствии с топологией.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_02/README.md#1-%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5-%D1%81%D0%B5%D1%82%D1%8C-%D0%B2-%D1%81%D0%BE%D0%BE%D1%82%D0%B2%D0%B5%D1%82%D1%81%D1%82%D0%B2%D0%B8%D0%B8-%D1%81-%D1%82%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D0%B5%D0%B9)
   - [Шаг 2. Настройте узлы ПК.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_02/README.md#%D1%88%D0%B0%D0%B3-2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%82%D0%B5-%D1%83%D0%B7%D0%BB%D1%8B-%D0%BF%D0%BA)
2. [Часть 2. Настройка базовых параметров сетевых устройств.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D1%87%D0%B0%D1%81%D1%82%D1%8C-2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%B1%D0%B0%D0%B7%D0%BE%D0%B2%D1%8B%D1%85-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D0%BE%D0%B2-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D1%8B%D1%85-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2)
   - [Шаг 1. Настройте базовые параметры коммутатора.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D1%88%D0%B0%D0%B3-1-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%82%D0%B5-%D0%B1%D0%B0%D0%B7%D0%BE%D0%B2%D1%8B%D0%B5-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%B0)
   - [Шаг 2. Настройте IP-адрес на компьютере PC-A.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D1%88%D0%B0%D0%B3-2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%82%D0%B5-ip-%D0%B0%D0%B4%D1%80%D0%B5%D1%81-%D0%BD%D0%B0-%D0%BA%D0%BE%D0%BC%D0%BF%D1%8C%D1%8E%D1%82%D0%B5%D1%80%D0%B5-pc-a)
3. [Часть 3. Проверка сетевых подключений.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D1%87%D0%B0%D1%81%D1%82%D1%8C-3-%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D1%8B%D1%85-%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B9)
   - [Шаг 1. Отобразите конфигурацию коммутатора.](https://github.com/getmandv/Network_Engineer._Basic/edit/main/Home_work/Lab_01/README.md#%D1%88%D0%B0%D0%B3-1-%D0%BE%D1%82%D0%BE%D0%B1%D1%80%D0%B0%D0%B7%D0%B8%D1%82%D0%B5-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8E-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%B0)
   - [Шаг 2. Протестируйте сквозное соединение, отправив эхо-запрос.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D1%88%D0%B0%D0%B3-2-%D0%BF%D1%80%D0%BE%D1%82%D0%B5%D1%81%D1%82%D0%B8%D1%80%D1%83%D0%B9%D1%82%D0%B5-%D1%81%D0%BA%D0%B2%D0%BE%D0%B7%D0%BD%D0%BE%D0%B5-%D1%81%D0%BE%D0%B5%D0%B4%D0%B8%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BE%D1%82%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%B2-%D1%8D%D1%85%D0%BE-%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81)
   - [Шаг 3. Проверьте удаленное управление коммутатором S1.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D1%88%D0%B0%D0%B3-3-%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D1%8C%D1%82%D0%B5-%D1%83%D0%B4%D0%B0%D0%BB%D0%B5%D0%BD%D0%BD%D0%BE%D0%B5-%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%BC-s1)
4. [Вопросы для повторения](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D0%B2%D0%BE%D0%BF%D1%80%D0%BE%D1%81%D1%8B-%D0%B4%D0%BB%D1%8F-%D0%BF%D0%BE%D0%B2%D1%82%D0%BE%D1%80%D0%B5%D0%BD%D0%B8%D1%8F)
5. [Приложение А. Инициализация и перезагрузка коммутатора.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/README.md#%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B0-%D0%B8%D0%BD%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D0%B8-%D0%BF%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%B0)
6. Файлы Cisco Packet Tracer
   - [Основной файл домашнего задания](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/pkt/lab_01.pkt)
   - [Файл Приложения А](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_01/pkt/lab_01_appendix_a.pkt)


## Часть 1. Создание и настройка сети.
###  Шаг 1. Подключите сеть в соответствии с топологией.

![](./images/lab_02_fig_02.png)
###  Шаг 2. Настройте узлы ПК.
a. Введите команду enable, чтобы войти в привилегированный режим EXEC.
```
Switch>
Switch>enable
Switch#
```
b. Изучите текущий файл running configuration.
```
Switch#show running-config 
Building configuration...

Current configuration : 1080 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Switch
!
!
!
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
!
!
!
line con 0
!
line vty 0 4
 login
line vty 5 15
 login
!
!
!
!
end


Switch#
```
- Сколько интерфейсов FastEthernet имеется на коммутаторе 2960?

На коммутаторе Cisco Catalyst 2960 имеется 24 интерфейса FastEthernet.
```
interface FastEthernet0/24
```
- Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960?

На коммутаторе Cisco Catalyst 2960 имеется 2 интерфейса Gigabit Ethernet.
```
interface GigabitEthernet0/2
```
- Каков диапазон значений, отображаемых в vty-линиях?

Два диапазона. 5 линий с 0 по 4 и 10 линий с 5 по 15. Суммарно 16 линий.
```
line vty 0 4
 login
line vty 5 15
 login
```
c. Изучите файл загрузочной конфигурации (startup configuration), который содержится в энергонезависимом ОЗУ (NVRAM).
```
Switch#show startup-config 
startup-config is not present
Switch#
```
- Почему появляется это сообщение?

Потому что этого файла в энергонезависимой памяти ещё не существует, так как я не сохранял никаких изменений внесённых в runing-config

d. Изучите характеристики SVI для VLAN 1.
```
Switch#show interface vlan1
Vlan1 is administratively down, line protocol is down
  Hardware is CPU Interface, address is 0090.21b4.8c69 (bia 0090.21b4.8c69)
  MTU 1500 bytes, BW 100000 Kbit, DLY 1000000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 21:40:21, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     1682 packets input, 530955 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicast)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     563859 packets output, 0 bytes, 0 underruns
     0 output errors, 23 interface resets
     0 output buffer failures, 0 output buffers swapped out

Switch#
```
- Назначен ли IP-адрес сети VLAN 1?

Нет.
- Какой MAC-адрес имеет SVI?

SVI имеет базовый MAC-адрес коммутатора 00:90:21:B4:8C:69
```
Hardware is CPU Interface, address is 0090.21b4.8c69 (bia 0090.21b4.8c69)
```
- Данный интерфейс включен?

Нет, интерфейс выключен.

e. Изучите IP-свойства интерфейса SVI сети VLAN 1.
```
Switch#show ip interface vlan1
Vlan1 is administratively down, line protocol is down
  Internet protocol processing disabled

Switch#
```
- Какие выходные данные вы видите?

То, что интерфейс выключен.

f. Подсоедините кабель Ethernet компьютера PC-A к порту 6 на коммутаторе и изучите IP-свойства интерфейса SVI сети VLAN 1. Дождитесь согласования параметров скорости и дуплекса между коммутатором и ПК.

![](./images/lab_01_fig_04.png)
- Какие выходные данные вы видите?

6 интерфейс коммутатора включился.
```
Switch#
%LINK-5-CHANGED: Interface FastEthernet0/6, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/6, changed state to up

Switch#
```
g. Изучите сведения о версии ОС Cisco IOS на коммутаторе.
```
Switch#show version 
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2013 by Cisco Systems, Inc.
Compiled Wed 26-Jun-13 02:49 by mnguyen

ROM: Bootstrap program is C2960 boot loader
BOOTLDR: C2960 Boot Loader (C2960-HBOOT-M) Version 12.2(25r)FX, RELEASE SOFTWARE (fc4)

Switch uptime is 39 minutes
System returned to ROM by power-on
System image file is "flash:c2960-lanbasek9-mz.150-2.SE4.bin"


This product contains cryptographic features and is subject to United
States and local country laws governing import, export, transfer and
use. Delivery of Cisco cryptographic products does not imply
third-party authority to import, export, distribute or use encryption.
Importers, exporters, distributors and users are responsible for
compliance with U.S. and local country laws. By using this product you
agree to comply with applicable laws and regulations. If you are unable
to comply with U.S. and local laws, return this product immediately.

A summary of U.S. laws governing Cisco cryptographic products may be found at:
http://www.cisco.com/wwl/export/crypto/tool/stqrg.html

If you require further assistance please contact us by sending email to
export@cisco.com.

cisco WS-C2960-24TT-L (PowerPC405) processor (revision B0) with 65536K bytes of memory.
Processor board ID FOC1010X104
Last reset from power-on
1 Virtual Ethernet interface
24 FastEthernet interfaces
2 Gigabit Ethernet interfaces
The password-recovery mechanism is enabled.

64K bytes of flash-simulated non-volatile configuration memory.
Base ethernet MAC Address       : 00:90:21:B4:8C:69
Motherboard assembly number     : 73-10390-03
Power supply part number        : 341-0097-02
Motherboard serial number       : FOC10093R12
Power supply serial number      : AZS1007032H
Model revision number           : B0
Motherboard revision number     : B0
Model number                    : WS-C2960-24TT-L
System serial number            : FOC1010X104
Top Assembly Part Number        : 800-27221-02
Top Assembly Revision Number    : A0
Version ID                      : V02
CLEI Code Number                : COM3L00BRA
Hardware Board Revision Number  : 0x01


Switch Ports Model              SW Version            SW Image
------ ----- -----              ----------            ----------
*    1 26    WS-C2960-24TT-L    15.0(2)SE4            C2960-LANBASEK9-M


Configuration register is 0xF



Switch#
```
- Под управлением какой версии ОС Cisco IOS работает коммутатор?
```
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
```
- Как называется файл образа системы?
```
System image file is "flash:c2960-lanbasek9-mz.150-2.SE4.bin"
```
h. Изучите свойства по умолчанию интерфейса FastEthernet, который используется компьютером PC-A.
```
Switch#show interfaces f0/6
FastEthernet0/6 is up, line protocol is up (connected)
  Hardware is Lance, address is 000c.85e3.c106 (bia 000c.85e3.c106)
 BW 100000 Kbit, DLY 1000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full-duplex, 100Mb/s
  input flow-control is off, output flow-control is off
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:08, output 00:00:05, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue :0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     956 packets input, 193351 bytes, 0 no buffer
     Received 956 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 watchdog, 0 multicast, 0 pause input
     0 input packets with dribble condition detected
     2357 packets output, 263570 bytes, 0 underruns
     0 output errors, 0 collisions, 10 interface resets
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier
     0 output buffer failures, 0 output buffers swapped out

Switch#
```
- Интерфейс включен или выключен?

Интерфейс включен.
```
FastEthernet0/6 is up, line protocol is up (connected)
```
- Что нужно сделать, чтобы включить интерфейс?

Ничего, он включён. Однако если бы он был выключен, то потребовалась бы команда no shutdown из режима глобальной конфигурации.
- Какой MAC-адрес у интерфейса?

MAC-адрес 00:0C:85:E3:C1:06
```
Hardware is Lance, address is 000c.85e3.c106 (bia 000c.85e3.c106)
```
- Какие настройки скорости и дуплекса заданы в интерфейсе?
```
Full-duplex, 100Mb/s
```
i.	Изучите флеш-память.
```
Switch#show flash
Directory of flash:/

    1  -rw-     4670455          <no date>  2960-lanbasek9-mz.150-2.SE4.bin

64016384 bytes total (59345929 bytes free)
Switch#
```
- Какое имя присвоено образу Cisco IOS?
Образу Cisco IOS присвоено имя 2960-lanbasek9-mz.150-2.SE4.bin
## Часть 2. Настройка базовых параметров сетевых устройств.
###  Шаг 1. Настройте базовые параметры коммутатора.
a.	В режиме глобальной конфигурации скопируйте следующие базовые параметры конфигурации и вставьте их в файл на коммутаторе S1. 
```
Switch>
Switch>enable
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#no ip domain-lookup
Switch(config)#hostname S1
S1(config)#service password-encryption 
S1(config)#enable secret class
S1(config)#banner motd #
Enter TEXT message.  End with the character '#'.
Unauthorized access is strictly prohibited. #

S1(config)#
```

b.	Назначьте IP-адрес интерфейсу SVI на коммутаторе. Благодаря этому вы получите возможность удаленного управления коммутатором.
```
S1(config)#interface vlan1
S1(config-if)#ip address 192.168.1.2 255.255.255.0
S1(config-if)#no shutdown

S1(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up

S1(config-if)#
```

c.	Доступ через порт консоли также следует ограничить  с помощью пароля. Используйте cisco в качестве пароля для входа в консоль в этом задании. Чтобы консольные сообщения не прерывали выполнение команд, используйте параметр logging synchronous.
```
S1(config-if)#line console 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#
```
```
S1(config-line)#logging synchronous
S1(config-line)#
```
d.	Настройте каналы виртуального соединения для удаленного управления (vty), чтобы коммутатор разрешил доступ через Telnet. 
```

```
- Для чего нужна команда login?
Команда login непосредственно включает необходимость ввода ранее установленного пароля.
###  Шаг 2. Настройте IP-адрес на компьютере PC-A.
![](./images/lab_01_fig_05.png)
## Часть 3. Проверка сетевых подключений.
### Шаг 1. Отобразите конфигурацию коммутатора.
a.	Пример конфигурации приведен ниже.
```
S1#show run
Building configuration...

Current configuration : 1293 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
service password-encryption
!
hostname S1
!
enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1
!
!
!
no ip domain-lookup
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 ip address 192.168.1.2 255.255.255.0
!
banner motd ^C
Unauthorized access is strictly prohibited. ^C
!
!
!
line con 0
 password 7 0822455D0A16
 logging synchronous
 login
!
line vty 0 4
 password 7 0822455D0A16
 login
line vty 5 15
 login
!
!
!
!
end


S1#
```
b.	Проверьте параметры VLAN 1.
```
S1#show interface vlan 1
Vlan1 is up, line protocol is up
  Hardware is CPU Interface, address is 0090.21b4.8c69 (bia 0090.21b4.8c69)
  Internet address is 192.168.1.2/24
  MTU 1500 bytes, BW 100000 Kbit, DLY 1000000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 21:40:21, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     1682 packets input, 530955 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicast)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     563859 packets output, 0 bytes, 0 underruns
     0 output errors, 23 interface resets
     0 output buffer failures, 0 output buffers swapped out

S1#
```
- Какова полоса пропускания этого интерфейса?

100 мегабит в секунду.
```
BW 100000 Kbit
```
### Шаг 2. Протестируйте сквозное соединение, отправив эхо-запрос.
a.	В командной строке компьютера PC-A с помощью утилиты ping проверьте связь сначала с адресом PC-A.
```
Cisco Packet Tracer PC Command Line 1.0
C:\>ping 192.168.1.10

Pinging 192.168.1.10 with 32 bytes of data:

Reply from 192.168.1.10: bytes=32 time=8ms TTL=128
Reply from 192.168.1.10: bytes=32 time=5ms TTL=128
Reply from 192.168.1.10: bytes=32 time=5ms TTL=128
Reply from 192.168.1.10: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.1.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 8ms, Average = 4ms

C:\>
```
b.	Из командной строки компьютера PC-A отправьте эхо-запрос на административный адрес интерфейса SVI коммутатора S1.
```
C:\>ping 192.168.1.2

Pinging 192.168.1.2 with 32 bytes of data:

Request timed out.
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.1.2:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

C:\>
```
### Шаг 3. Проверьте удаленное управление коммутатором S1.
a.	Откройте Tera Term или другую программу эмуляции терминала с возможностью Telnet.

![](./images/lab_01_fig_06.png)

b.	Выберите сервер Telnet и укажите адрес управления SVI для подключения к S1.  Пароль: cisco.

![](./images/lab_01_fig_07.png)

c.	После ввода пароля cisco вы окажетесь в командной строке пользовательского режима. Для перехода в исполнительский режим EXEC введите команду enable и используйте секретный пароль class.

![](./images/lab_01_fig_08.png)

d.	Сохраните конфигурацию.
```
S1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
S1#
```

e.	Чтобы завершить сеанс Telnet, введите exit.

![](./images/lab_01_fig_09.png)

## Вопросы для повторения.
1.	Зачем необходимо настраивать пароль VTY для коммутатора?

Что бы при удлаённом подключении к коммутатору требовалось ввести устанолвенный пароль для установки соединения.

2.	Что нужно сделать, чтобы пароли не отправлялись в незашифрованном виде?

Подключаться к коммутатору по протоколу SSH.

## 	Приложение А. Инициализация и перезагрузка коммутатора.
a.	Подключитесь к коммутатору с помощью консоли и войдите в привилегированный режим EXEC.
```
Press RETURN to get started!


Unauthorized access is strictly prohibited. 

User Access Verification

Password: 

S1>enable
Password: 
S1#
```
b.	Воспользуйтесь командой show flash, чтобы определить, были ли созданы сети VLAN на коммутаторе.
```
S1#show flash
Directory of flash:/

    1  -rw-     4670455          <no date>  2960-lanbasek9-mz.150-2.SE4.bin
    3  -rw-        1293          <no date>  config.text

64016384 bytes total (59344636 bytes free)
S1#
```
c.	Если во флеш-памяти обнаружен файл vlan.dat, удалите его.

Файла отсутствует.

d.	Появится запрос о проверке имени файла.

При попытке удалить не существующий файл, запрос действительно появляется однако, разумеется появляется ошибка сообщающая об отсутствии файла.
```
S1#delete vlan.dat
Delete filename [vlan.dat]?
Delete flash:/vlan.dat? [confirm]
%Error deleting flash:/vlan.dat (No such file or directory)

S1#
```
e.	Введите команду erase startup-config.
```
S1#erase startup-config
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete
%SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
S1#
```
f.	Перезагрузите коммутатор, чтобы удалить устаревшую информацию о конфигурации из памяти. 
```
S1#reload
Proceed with reload? [confirm]
C2960 Boot Loader (C2960-HBOOT-M) Version 12.2(25r)FX, RELEASE SOFTWARE (fc4)
Cisco WS-C2960-24TT (RC32300) processor (revision C0) with 21039K bytes of memory.
2960-24TT starting...
Base ethernet MAC Address: 0090.21B4.8C69
Xmodem file system is available.
Initializing Flash...
```
g.	После перезагрузки коммутатора появится запрос о входе в диалоговое окно начальной конфигурации. 

Подобный запрос не появился, однако конфигурация коммутатора полностью сброшена.
```
Switch>
Switch>enable
Switch#show startup-config 
startup-config is not present
Switch#
```
```
Switch#show running-config 
Building configuration...

Current configuration : 1080 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Switch
!
!
!
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
!
!
!
line con 0
!
line vty 0 4
 login
line vty 5 15
 login
!
!
!
!
end


Switch#
```
