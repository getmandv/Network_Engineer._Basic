# Настройка протокола OSPFv2 для одной области.
### Дано:
###	Топология
![](./images/lab_10_fig_01.png)
###	Таблица адресации
|Устройство|Интерфейс|IP-адрес   |Маска подсети|
|----------|---------|-----------|-------------|
|R1        |G0/0/1   |10.53.0.1  |255.255.255.0|
|R1        |Loopback1|172.16.1.1 |255.255.255.0|
|R2        |G0/0/1   |10.53.0.2  |255.255.255.0|
|R2        |Loopback1|192.168.1.1|255.255.255.0|
### Задание:
1. [Часть 1. Создание сети и настройка основных параметров устройства.]()
2. [Часть 2. Настройка и проверка базовой работы протокола  OSPFv2 для одной области.]()
3. [Часть 3: Оптимизация и проверка конфигурации OSPFv2 для одной области.]()
4. Файлы Cisco Packet Tracer
   - [Основной файл домашнего задания](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_09/pkt/lab_09.pkt)
## Часть 1. Создание сети и настройка основных параметров устройства.
###  Шаг 1. Создайте сеть согласно топологии.
![](./images/lab_10_fig_02.png)
### Шаг 2. Произведите базовую настройку маршрутизаторов.
- a.	Назначьте маршрутизатору имя устройства.
- b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
- c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
- d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
- e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
- f.	Зашифруйте открытые пароли.
- g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
- h.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
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

R1(config)#end
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#wr
Building configuration...
[OK]
R1#
```
*Повтоярем аналогичную настройку на маршрутизаторе R2.*
### Шаг 3. Настройка и проверка основных параметров коммутатора
- a.	Назначьте коммутатору имя устройства.
- b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
- c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
- d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
- e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
- f.	Зашифруйте открытые пароли.
- g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
- h.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
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

S1(config)#end
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#wr
Building configuration...
[OK]
S1#
```
*Повтоярем аналогичную настройку на коммутаторе S2.*
## Часть 2. Настройка и проверка базовой работы протокола OSPFv2 для одной области.
###  Шаг 1. Настройте адреса интерфейса и базового OSPFv2 на каждом маршрутизаторе.
- a.	Настройте адреса интерфейсов на каждом маршрутизаторе, как показано в таблице адресации выше.

*Маршрутизатор R1*
```
R1(config)#interface gigabitEthernet 0/0/1
R1(config-if)#ip address 10.53.0.1 255.255.255.0
R1(config-if)#no shutdown 

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1, changed state to up

R1(config-if)#exit
R1(config)#interface loopback 1

R1(config-if)#
%LINK-5-CHANGED: Interface Loopback1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback1, changed state to up

R1(config-if)#ip address 172.16.1.1 255.255.255.0
R1(config-if)#
```
*Не забываем включить интерфейс GigabitEthernet0/0/1 после настрйки адреса.*
*Повтоярем аналогичную настройку на маршрутизаторе R2, с учётом соответствующих адресов.*
- b.	Перейдите в режим конфигурации маршрутизатора OSPF, используя идентификатор процесса 56.
- c.	Настройте статический идентификатор маршрутизатора для каждого маршрутизатора (1.1.1.1 для R1, 2.2.2.2 для R2).
- d.	Настройте инструкцию сети для сети между R1 и R2, поместив ее в область 0.

*Маршрутизатор R1*
```
R1(config)#router ospf 56
R1(config-router)#router-id 1.1.1.1
R1(config-router)#exit
R1(config)#interface gigabitEthernet 0/0/1
R1(config-if)#ip ospf 56 area 0
R1(config-if)#
```
*Маршрутизатор R2*
```
R2(config)#router ospf 56
R2(config-router)#router-id 2.2.2.2
R2(config-router)#
R2(config-router)#exit
R2(config)#interface gigabitEthernet 0/0/1
R2(config-if)#ip ospf 56 area 0
R2(config-if)#
```
- e.	Только на R2 добавьте конфигурацию, необходимую для объявления сети Loopback 1 в область OSPF 0.
```
R2(config)#interface loopback 1
R2(config-if)#ip ospf 56 area 0
R2(config-if)#
```
- f.	Убедитесь, что OSPFv2 работает между маршрутизаторами. Выполните команду, чтобы убедиться, что R1 и R2 сформировали смежность.

*Маршрутизатор R1*
```
R1#show ip ospf neighbor 


Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           1   FULL/DR         00:00:39    10.53.0.2       GigabitEthernet0/0/1
R1#
```
*Маршрутизатор R2*
```
R2#show ip ospf neighbor 


Neighbor ID     Pri   State           Dead Time   Address         Interface
1.1.1.1           1   FULL/BDR        00:00:33    10.53.0.1       GigabitEthernet0/0/1
R2#
```
- Какой маршрутизатор является DR?

*DR является маршрутизатор R2*

- Какой маршрутизатор является BDR?

*BDR является маршрутизатор R1*

- Каковы критерии отбора?

*Приоритет и Router ID. В нашем случае приоритет олинаковый, по этому выбор DR основывается на router id.*

- g.	На R1 выполните команду show ip route ospf, чтобы убедиться, что сеть R2 Loopback1 присутствует в таблице маршрутизации. Обратите внимание, что поведение OSPF по умолчанию заключается в объявлении интерфейса обратной связи в качестве маршрута узла с использованием 32-битной маски.
```
R1#show ip route ospf 
     192.168.1.0/32 is subnetted, 1 subnets
O       192.168.1.1 [110/2] via 10.53.0.2, 4294967275:4294967253:4294967284, GigabitEthernet0/0/1

R1#
```
- h.	Запустите Ping до  адреса интерфейса R2 Loopback 1 из R1. Выполнение команды ping должно быть успешным.

![](./images/lab_10_fig_03.png)
## Часть 2. Настройка и проверка базовой работы протокола OSPFv2 для одной области.
### Шаг 1. Реализация различных оптимизаций на каждом маршрутизаторе.
