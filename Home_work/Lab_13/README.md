# Лабораторная работа - Настройка протоколов CDP, LLDP и NTP.
### Дано:
###	Топология
![](./images/lab_13_fig_01.png)
###	Таблица адресации
|Устройство  |Интерфейс |IP-адрес  |Маска подсети|Шлюз по умолчанию|
|------------|----------|----------|-------------|-----------------|
|R1          |Loopback1 |172.16.1.1|255.255.255.0|                 |
|R1          |G0/0/1    |10.22.0.1 |255.255.255.0|                 |
|S1          |SVI VLAN 1|10.22.0.2 |255.255.255.0|10.22.0.1        |
|S2          |SVI VLAN 1|10.22.0.3 |255.255.255.0|10.22.0.1        |
### Задание:
1. [Часть 1. Создание сети и настройка основных параметров устройства.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_13/README.md#%D1%87%D0%B0%D1%81%D1%82%D1%8C-1-%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D1%81%D0%B5%D1%82%D0%B8-%D0%B8-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D1%85-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D0%BE%D0%B2-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%B0)
2. [Часть 2. Обнаружение сетевых ресурсов с помощью протокола CDP.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_13/README.md#%D1%87%D0%B0%D1%81%D1%82%D1%8C-2-%D0%BE%D0%B1%D0%BD%D0%B0%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D1%8B%D1%85-%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D0%BE%D0%B2-%D1%81-%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E-%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D0%B0-cdp)
3. [Часть 3. Обнаружение сетевых ресурсов с помощью протокола LLDP.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_13/README.md#%D1%87%D0%B0%D1%81%D1%82%D1%8C-3-%D0%BE%D0%B1%D0%BD%D0%B0%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D1%8B%D1%85-%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D0%BE%D0%B2-%D1%81-%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E-%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D0%B0-lldp)
4. [Часть 4. Настройка и проверка NTP.](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_13/README.md#%D1%87%D0%B0%D1%81%D1%82%D1%8C-4-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-ntp)
5. Файлы Cisco Packet Tracer
   - [Основной файл домашнего задания](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_13/pkt/lab_13.pkt)
## Часть 1. Создание сети и настройка основных параметров устройства.
###  Шаг 1. Создайте сеть согласно топологии.
![](./images/lab_13_fig_03.png)
###  Шаг 2. Настройте базовые параметры для маршрутизатора.
- a.	Назначьте маршрутизатору имя устройства.
- b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
- c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
- d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
- e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
- f.	Зашифруйте открытые пароли.
- g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
- h.	Настройка интерфейсов, перечисленных в таблице выше
- i.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.

*Маршрутизатор R1*
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

R1(config)#interface loopback1

R1(config-if)#
%LINK-5-CHANGED: Interface Loopback1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback1, changed state to up

R1(config-if)#ip address 172.16.1.1 255.255.255.0
R1(config-if)#exit
R1(config)#interface gigabitEthernet 0/0/1
R1(config-if)#ip address 10.22.0.1 255.255.255.0
R1(config-if)#end
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#wr
Building configuration...
[OK]
R1#
```
###  Шаг 3. Настройте базовые параметры каждого коммутатора.
- a.	Присвойте коммутатору имя устройства.
- b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
- c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
- d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
- e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
- f.	Зашифруйте открытые пароли.
- g.	Создайте баннер, который предупреждает всех, кто обращается к устройству, видит баннерное сообщение «Только авторизованные пользователи!».  
- h.	Отключите неиспользуемые интерфейсы
- i.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.

*Коммутатор S1*
```
Switch>en
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S1
S1(config)#no ip domain-lookup
S1(config)#enable secret class
S1(config)#line con 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#line vty 0 15
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#service password-encryption
S1(config)#banner motd #
Enter TEXT message.  End with the character '#'.
This is S1 switch.
Authorized Users Only!#

S1(config)#interface range fastEthernet 0/2-4, fastEthernet 0/6-24, gigabitEthernet 0/1-2
S1(config-if-range)#shutdown 

%LINK-5-CHANGED: Interface FastEthernet0/2, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/6, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/7, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/8, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/9, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/10, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/11, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/12, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/13, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/14, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/15, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/16, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/17, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/18, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/19, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/20, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/21, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/22, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/23, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/24, changed state to administratively down

%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to administratively down

%LINK-5-CHANGED: Interface GigabitEthernet0/2, changed state to administratively down
S1(config-if-range)#end
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#wr
Building configuration...
[OK]
S1#
```
*Повторяем аналогичную настройку для коммутатора S2, с учётом изменившихся портов для отключения.*
## Часть 2. Обнаружение сетевых ресурсов с помощью протокола CDP.
- a.	На R1 используйте соответствующую команду show cdp, чтобы определить, сколько интерфейсов включено CDP, сколько из них включено и сколько отключено.
*Что бы полноценно отработать данный пункт, потребуется предварительно включить порт Gig 0/0/1, так как "из коробки" он выключен.*
```
R1#show cdp interface
Vlan1 is administratively down, line protocol is down
  Sending CDP packets every 60 seconds
  Holdtime is 180 seconds
GigabitEthernet0/0/0 is administratively down, line protocol is down
  Sending CDP packets every 60 seconds
  Holdtime is 180 seconds
GigabitEthernet0/0/1 is up, line protocol is up
  Sending CDP packets every 60 seconds
  Holdtime is 180 seconds
R1#
```
- Сколько интерфейсов участвует в объявлениях CDP? Какие из них активны?

*Участвует 3 интерфейса, активный только GigabitEthernet0/0/1*
- b.	На R1 используйте соответствующую команду show cdp, чтобы определить версию IOS, используемую на S1.

```
R1#show cdp entry  S1

Device ID: S1
Entry address(es): 
Platform: cisco 2960, Capabilities: Switch
Interface: GigabitEthernet0/0/1, Port ID (outgoing port): FastEthernet0/5
Holdtime: 123

Version :
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2013 by Cisco Systems, Inc.
Compiled Wed 26-Jun-13 02:49 by mnguyen

advertisement version: 2
Duplex: full

R1#
```
- Какая версия IOS используется на  S1?

*Version: Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)*
- c.	На S1 используйте соответствующую команду show cdp, чтобы определить, сколько пакетов CDP было выданных.
*CPT не знает команду "show cdp traffic" по этому воспользуемся предложеным выводом из домашнего задания.*
```
S1# show cdp traffic
CDP counters : 
        Total packets output: 179, Input: 148 
        Hdr syntax: 0, Chksum error: 0, Encaps failed: 0 
        No memory: 0, Invalid packet: 0, 
        CDP version 1 advertisements output: 0, Input: 0 
        CDP version 2 advertisements output: 179, Input: 148
```
- Сколько пакетов имеет выход CDP с момента последнего сброса счетчика?

*output: 179*

- d.	Настройте SVI для VLAN 1 на S1 и S2, используя IP-адреса, указанные в таблице адресации выше. Настройте шлюз по умолчанию для каждого коммутатора на основе таблицы адресов.

*Коммутатор S1*
```
S1(config)#interface vlan 1
S1(config-if)#ip address 10.22.0.2 255.255.255.0
S1(config-if)#no shutdown 

S1(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up

S1(config-if)#exit
S1(config)#ip default-gateway 10.22.0.1
S1(config)#
```
*Коммутатор S2*
```
S2(config)#interface Vlan1
S2(config-if)#ip address 10.22.0.3 255.255.255.0
S2(config-if)#no shutdown 

S2(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up

S2(config-if)#exit
S2(config)#ip default-gateway 10.22.0.1
S2(config)#
```
- e.	На R1 выполните команду show cdp entry S1 .
```
R1#show cdp entry S1

Device ID: S1
Entry address(es): 
  IP address : 10.22.0.2
Platform: cisco 2960, Capabilities: Switch
Interface: GigabitEthernet0/0/1, Port ID (outgoing port): FastEthernet0/5
Holdtime: 125

Version :
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2013 by Cisco Systems, Inc.
Compiled Wed 26-Jun-13 02:49 by mnguyen

advertisement version: 2
Duplex: full

R1#
```
- Какие дополнительные сведения доступны теперь?

*Entry address(es):  IP address : 10.22.0.2*
- f.	Отключить CDP глобально на всех устройствах.

*Маршрутизатор R1*
```
R1(config)#no cdp run
R1(config)#
```
*Повторяем команду на оставшемся оборудовании.*
## Часть 3. Обнаружение сетевых ресурсов с помощью протокола LLDP.
- a.	Введите соответствующую команду lldp, чтобы включить LLDP на всех устройствах в топологии.

*Маршрутизатор R1*
```
R1(config)#lldp run
R1(config)#
```
*Повторяем команду на оставшемся оборудовании.*
- b.	На S1 выполните соответствующую команду lldp, чтобы предоставить подробную информацию о S2.
*CPT не знает о такой команде, но знает о show lldp neighbors, использую её.*
```
S1#show lldp neighbors 
Capability codes:
    (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device
    (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other
Device ID           Local Intf     Hold-time  Capability      Port ID
R1                  Fa0/5          120        R               Gig0/0/1
S2                  Fa0/1          120        B               Fa0/1

Total entries displayed: 2
S1#
```
- Что такое chassis ID  для коммутатора S2?

*МАС-адрес устройства*
- c.	Соединитесь через консоль на всех устройствах и используйте команды LLDP, необходимые для отображения топологии физической сети только из выходных данных команды show.

*Маршрутизатор R1*
```
R1#show lldp neighbors 
Capability codes:
    (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device
    (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other
Device ID           Local Intf     Hold-time  Capability      Port ID
S1                  Gig0/0/1       120        B               Fa0/5

Total entries displayed: 1
R1#
```

*Коммутатор S1*
```
S1#show lldp neighbors 
Capability codes:
    (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device
    (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other
Device ID           Local Intf     Hold-time  Capability      Port ID
R1                  Fa0/5          120        R               Gig0/0/1
S2                  Fa0/1          120        B               Fa0/1

Total entries displayed: 2
S1#
```

*Коммутатор S2*
```
S2#show lldp neighbors 
Capability codes:
    (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device
    (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other
Device ID           Local Intf     Hold-time  Capability      Port ID
S1                  Fa0/1          120        B               Fa0/1

Total entries displayed: 1
S2#
```
## Часть 4. Настройка NTP.
### Шаг 1. Выведите на экран текущее время.
```
R1#show clock 
*21:11:9.209 UTC Mon Mar 8 1993
R1#
```
- Запишите отображаемые сведения о текущем времени в следующей таблице.

|Дата      |Время      |Часовой пояс|Источник времени|
|----------|-----------|------------|----------------|
|Mar 8 1993|21:11:9.209|UTC         |R1              |

### Шаг 2. Установите время.
```
R1#clock set 17:41:00 01 jun 2026
R1#
```
### Настройте R1 в качестве хозяина NTP с уровнем слоя 4.
```
R1(config)#ntp master 4
R1(config)#ntp update-calendar 
R1(config)#
```
### Шаг 4. Настройте клиент NTP.
- a.	Выполните соответствующую команду на S1 и S2, чтобы просмотреть настроенное время. Запишите текущее время,  в следующей таблице.
|Дата      |Время      |Часовой пояс|Источник времени|
|----------|-----------|------------|----------------|
|Mar 1 1993|0:48:9.464 |UTC         |S1              |
|Mar 1 1993|0:49:50.865|UTC         |S2              |

- b.	Настройте S1 и S2 в качестве клиентов NTP. Используйте соответствующие команды NTP для получения времени от интерфейса G0/0/1 R1, а также для периодического обновления календаря или аппаратных часов коммутатора.

*Коммутатор S1*
```
S1(config)#ntp server 10.22.0.1
S1(config)#
```
*Повторяем настройку на коммутаторе S2.*
### Шаг 5. Проверьте настройку NTP.
- a.	Используйте соответствующую команду show , чтобы убедиться, что S1 и S2 синхронизированы с R1.

*Коммутатор S1*
```
S1#show ntp associations

address         ref clock       st   when     poll    reach  delay          offset            disp
*~10.22.0.1     127.127.1.1     4    15       16      377    0.00           0.00              0.12
 * sys.peer, # selected, + candidate, - outlyer, x falseticker, ~ configured
S1#
```

*Коммутатор S2*
```
S2#show ntp associations

address         ref clock       st   when     poll    reach  delay          offset            disp
*~10.22.0.1     127.127.1.1     4    9        16      377    0.00           0.00              0.12
 * sys.peer, # selected, + candidate, - outlyer, x falseticker, ~ configured
S2#
```
- b.	Выполните соответствующую команду на S1 и S2, чтобы просмотреть настроенное время и сравнить ранее записанное время.

*Коммутатор S1*
```
S1#show clock 
17:55:59.903 UTC Mon Jun 1 2026
S1#
```

*Коммутатор S2*
```
S2#show clock 
17:56:43.44 UTC Mon Jun 1 2026
S2#
```
- Для каких интерфейсов в пределах сети не следует использовать протоколы обнаружения сетевых ресурсов? Поясните ответ.

*На пограничных интерфейсах сети, что бы собственноручно не предоставить информацию о нашей системе злоумышленнику.
