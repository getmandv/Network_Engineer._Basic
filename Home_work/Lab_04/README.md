
# Лабораторная работа. Настройка IPv6-адресов на сетевых устройствах
### Дано:
###	Топология
![](./images/lab_04_fig_01.png)
###	Таблица адресации
|Устройство  |Интерфейс  |IPv6-адрес         |Link local IPv6-адрес|Длина префикса|Шлюз по умолчанию|
|------------|-----------|-------------------|---------------------|--------------|-----------------|
|R1          |G0/0/0     | 2001:db8:acad:a::1|fe80::1              |64            |-                |
|R1          |G0/0/1     | 2001:db8:acad:1::1|fe80::1              |64            |-                |
|S1          |VLAN 1     | 2001:db8:acad:1::b|fe80::b              |64            |-                |
|PC-A        |NIC        | 2001:db8:acad:1::3|SLACC                |64            |fe80::1          |
|PC-B        |NIC        | 2001:db8:acad:a::3|SLACC                |64            |fe80::1          |
### Задание:
1. [Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора]()
2. [Часть 2. Ручная настройка IPv6-адресов]()
3. [Часть 3. Проверка сквозного подключения]()
4. [Вопросы для повторения]()
5. Файлы Cisco Packet Tracer
   - [Основной файл домашнего задания]()


## Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора
###  Шаг 1. Настройте маршрутизатор.
- Назначьте имя хоста и настройте основные параметры устройства.
```
Router>
Router>enable
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
R1(config-line)#transport input ssh
R1(config-line)#login local
R1(config-line)#exit
R1(config)#service password-encryption
R1(config)#banner motd #
Enter TEXT message.  End with the character '#'.
Router R1 otus.ru HW 4
Authorized User Only!#

R1(config)#ip domain-name otus.ru
R1(config)#crypto key generate rsa general-keys modulus 1024
The name for the keys will be: R1.otus.ru

% The key modulus size is 1024 bits
% Generating 1024 bit RSA keys, keys will be non-exportable...[OK]
*Mar 1 0:22:7.287: %SSH-5-ENABLED: SSH 1.99 has been enabled
R1(config)#username admin privilege 15 secret Adm1nP@55
R1(config)#ip ssh version 2
R1(config)#exit
R1#wr
Building configuration...
[OK]
R1#
```
###  Шаг 2. Настройте коммутатор.
- Назначьте имя хоста и настройте основные параметры устройства.
```
Switch>
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
S1(config-line)#transport input ssh
S1(config-line)#login local
S1(config-line)#exit
S1(config)#service password-encryption
S1(config)#banner motd #
Enter TEXT message.  End with the character '#'.
Switch S1 otus.ru HW 4
Authorized User Only!#

S1(config)#ip domain-name otus.ru
S1(config)#crypto key generate rsa general-keys modulus 1024
The name for the keys will be: S1.otus.ru

% The key modulus size is 1024 bits
% Generating 1024 bit RSA keys, keys will be non-exportable...[OK]
*Mar 1 0:56:25.840: %SSH-5-ENABLED: SSH 1.99 has been enabled
S1(config)#username admin privilege 15 secret Adm1nP@55
S1(config)#ip ssh version 2
S1(config)#exit
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#wr
Building configuration...
[OK]
S1#
```
Дополнительно переключаем шаблон для возмодности адресации ipv6.
```
S1#show sdm prefer 
 The current template is "default" template.
 The selected template optimizes the resources in
 the switch to support this level of features for
 0 routed interfaces and 1024 VLANs.

  number of unicast mac addresses:                  8K
  number of IPv4 IGMP groups + multicast routes:    0.25K
  number of IPv4 unicast routes:                    0
  number of IPv6 multicast groups:                  0
  number of directly-connected IPv6 addresses:      0
  number of indirect IPv6 unicast routes:           0
  number of IPv4 policy based routing aces:         0
  number of IPv4/MAC qos aces:                      0.125k
  number of IPv4/MAC security aces:                 0.375k
  number of IPv6 policy based routing aces:         0
  number of IPv6 qos aces:                          20
  number of IPv6 security aces:                     25

S1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#sdm prefer dual-ipv4-and-ipv6 default 
Changes to the running SDM preferences have been stored, but cannot take effect until the next reload.
Use 'show sdm prefer' to see what SDM preference is currently active.
S1(config)#end
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#wr
Building configuration...
[OK]
S1#reload
```
## Часть 2. Ручная настройка IPv6-адресов
### Шаг 1. Назначьте IPv6-адреса интерфейсам Ethernet на R1.
a.	Назначьте глобальные индивидуальные IPv6-адреса, указанные в таблице адресации обоим интерфейсам Ethernet на R1.
