
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
Delete filename [vlan.dat]?
Delete flash:/vlan.dat? [confirm]y%Error deleting flash:/vlan.dat (No such file or directory)
Router#reload
Proceed with reload? [confirm]y
Initializing Hardware ...
```
- Коммутатор
```
Switch>enable 
Switch#erase startup-config 
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]y[OK]
Erase of nvram: complete
%SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
Switch#delete vlan.dat
Delete filename [vlan.dat]?
Delete flash:/vlan.dat? [confirm]y%Error deleting flash:/vlan.dat (No such file or directory)
Switch#reload
Proceed with reload? [confirm]y
C2960 Boot Loader (C2960-HBOOT-M) ...
```
###  Шаг 3. Настройте маршрутизатор.
a.	Подключитесь к маршрутизатору с помощью консоли и активируйте привилегированный режим EXEC.
```
Router>enable 
Router#
```
b.	Войдите в режим конфигурации.
```
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#
```
c.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
```
Router(config)#no ip domain-lookup 
Router(config)#
```
d.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
```
Router(config)#enable secret class 
Router(config)#
```
e.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
```
Router(config)#line con 0
Router(config-line)#password cisco
Router(config-line)#login
Router(config-line)#
```
f.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
```
Router(config)#line vty 0 15
Router(config-line)#password cisco
Router(config-line)#login
Router(config-line)#
```
g.	Зашифруйте открытые пароли.
```
Router(config)#service password-encryption 
Router(config)#
```
h.	Создайте баннер, который предупреждает о запрете несанкционированного доступа.
```
Router(config)#banner motd #
Enter TEXT message.  End with the character '#'.
Authorized Users Only!#

Router(config)#
```
i.	Настройте и активируйте на маршрутизаторе интерфейс G0/0/1, используя информацию, приведенную в таблице адресации.
```
Router(config)#interface gig0/0/1
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#no shutdown 
Router(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1, changed state to up

Router(config-if)#
```
j.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
```
Router#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
Router#
```
###  Шаг 4. Настройте компьютер PC-A.
a.	Настройте для PC-A IP-адрес и маску подсети.
![](./images/lab_05_fig_03.png)
