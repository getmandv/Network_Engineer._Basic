# Лабраторная работа - Настройка DHCP.
### Дано:
### Топология:
![](./images/lab_08_v6_fig_01.png)
### Таблица адресации:
|Устройство|Интерфейс|IPv6-адрес           |
|----------|---------|---------------------|
|R1        |G0/0/0   |2001:db8:acad:2::1/64|
|R1        |G0/0/0   |fe80::1              |
|R1        |G0/0/1   |2001:db8:acad:1::1/64|
|R1        |G0/0/1   |fe80::1              |
|R2        |G0/0/0   |2001:db8:acad:2::2/64|
|R2        |G0/0/0   |fe80::2              |
|R2        |G0/0/1   |2001:db8:acad:3::1/64|
|R2        |G0/0/1   |fe80::2              |
|PC-A      |NIC      |DHCP                 |
|PC-B      |NIC      |DHCP                 |

### Задание:
1. [Часть 1. Создание сети и настройка основных параметров устройства.]()
2. [Часть 2. Проверка назначения адреса SLAAC от R1.]()
3. [Часть 3. Настройка и проверка сервера DHCPv6 без гражданства на R1.]()
4. [Часть 4. Настройка и проверка состояния DHCPv6 сервера на R1.]()
5. [Часть 5. Настройка и проверка DHCPv6 Relay на R2.]()
6. Файлы Cisco Packet Tracer
   - [Основной файл домашнего задания](https://github.com/getmandv/Network_Engineer._Basic/blob/main/Home_work/Lab_07/pkt/lab_07.pkt)
## Часть 1. Создание сети и настройка основных параметров устройства.
###  Шаг 1:	Создайте сеть согласно топологии.
![](./images/lab_08_v6_fig_02.png)
### Шаг 2. Настройте базовые параметры каждого коммутатора. (необязательно)
- a.	Присвойте коммутатору имя устройства.
- b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
- c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
- d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
- e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
- f.	Зашифруйте открытые пароли.
- g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
- h.	Отключите все неиспользуемые порты.
- i.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
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

S1(config)#interface range fastEthernet 0/1-04, fastEthernet 0/7-24, gigabitEthernet 0/1-2
S1(config-if-range)#shutdown

%LINK-5-CHANGED: Interface FastEthernet0/1, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/2, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to administratively down

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
S1(config-if-range)#exit
S1(config)#exit
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#wr
Building configuration...
[OK]
S1#
```
Данную настройку повторяем на коммутаторе S2, с учётом изменившихся портов для отключения согластно пункта i.
### Шаг 3. Произведите базовую настройку маршрутизаторов.
- a.	Назначьте маршрутизатору имя устройства.
- b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
- c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
- d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
- e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
- f.	Зашифруйте открытые пароли.
- g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
- h.	Активация IPv6-маршрутизации
- i.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
```
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

R1(config)#ipv6 unicast-routing
R1(config)#exit
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#wr
Building configuration...
[OK]
R1#
```
Данную настройку повторяем на маршрутизаторе R2.
### Шаг 4. Настройка интерфейсов и маршрутизации для обоих маршрутизаторов.

- a.	Настройте интерфейсы G0/0/0 и G0/1 на R1 и R2 с адресами IPv6, указанными в таблице выше

Маршрутизатор R1
```
R1(config)#interface gigabitEthernet 0/0/0
R1(config-if)#ipv6 address fe80::1 link-local 
R1(config-if)#ipv6 address 2001:db8:acad:2::1/64
R1(config-if)#exit
R1(config)#interface gigabitEthernet 0/0/1
R1(config-if)#ipv6 address fe80::1 link-local 
R1(config-if)#ipv6 address 2001:db8:acad:1::1/64
R1(config-if)#
```
Маршрутизатор R2
```
R2(config)#interface gigabitEthernet 0/0/0
R2(config-if)#ipv6 address fe80::2 link-local
R2(config-if)#ipv6 address 2001:db8:acad:2::2/64
R2(config-if)#exit
R2(config)#interface gigabitEthernet 0/0/1
R2(config-if)#ipv6 address fe80::1 link-local 
R2(config-if)#ipv6 address 2001:db8:acad:3::1/64
R2(config-if)#
```
- b.	Настройте маршрут по умолчанию на каждом маршрутизаторе, который указывает на IP-адрес G0/0/0 на другом маршрутизаторе.
Маршрутизатор R1
```
R1(config)#ipv6 route ::/0 2001:DB8:ACAD:2::2
R1(config)#
```
Маршрутизатор R2
```
R2(config)#ipv6 route ::/0 2001:DB8:ACAD:2::1
R2(config)#
```
- c.	Убедитесь, что маршрутизация работает с помощью пинга адреса G0/0/1 R2 из R1

Прежде чем выполнить этот пункт, нам потребуется включить интерфейсы G0/0/0 и G0/0/1 на обоих маршрутизаторах, так как "из коробки" они выключены.
Для этого на обоих маршрутизаторах выполняем:
```
R1(config)#interface range gigabitEthernet 0/0/0-1
R1(config-if-range)#no shutdown 
R1(config-if-range)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up

%LINK-5-CHANGED: Interface GigabitEthernet0/0/1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1, changed state to up

R1(config-if-range)#
```
Теперь проверяем работу маршрутизации.

![](./images/lab_08_v6_fig_03.png)

- d.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
Маршрутизатор R1
```
R1#wr
Building configuration...
[OK]
R1#
```
Маршрутизатор R2
```
R2#wr
Building configuration...
[OK]
R2#
```
## Часть 2. Проверка назначения адреса SLAAC от R1
- Включите PC-A и убедитесь, что сетевой адаптер настроен для автоматической настройки IPv6.

![](./images/lab_08_v6_fig_04.png)

- Через несколько минут результаты команды ipconfig должны показать, что PC-A присвоил себе адрес из сети 2001:db8:1::/64.

![](./images/lab_08_v6_fig_05.png)

- Откуда взялась часть адреса с идентификатором хоста?

Сформирована хостом автоматически с помощью алгоритма EUI-64.
## Часть 3. Настройка и проверка сервера DHCPv6 на R1.
### Шаг 1. Более подробно изучите конфигурацию PC-A.
- a.	Выполните команду ipconfig /all на PC-A и посмотрите на результат.

![](./images/lab_08_v6_fig_06.png)
### Шаг 2. Настройте R1 для предоставления DHCPv6 без состояния для PC-A.
- a.	Создайте пул DHCP IPv6 на R1 с именем R1-STATELESS. В составе этого пула назначьте адрес DNS-сервера как 2001:db8:acad::1, а имя домена — как stateless.com.

Предположу что в данном пункте опечатка, так как в задании указано в качестве DNS сервера указать адрес 001:db8:acad::1, а в команде указан адрес 2001:db8:acad::254. Судя по дальнейшему выводу команды ipconfig /all в метдичке, правильный адрес всё же 2001:db8:acad::254, по этому использую его.  
```
R1(config)#ipv6 dhcp pool R1-STATELESS
R1(config-dhcpv6)#dns-server 2001:db8:acad::254
R1(config-dhcpv6)#domain-name STATELESS.com
R1(config-dhcpv6)#
```
-  b.	Настройте интерфейс G0/0/1 на R1, чтобы предоставить флаг конфигурации OTHER для локальной сети R1 и укажите только что созданный пул DHCP в качестве ресурса DHCP для этого интерфейса.
```
R1(config)#interface gigabitEthernet 0/0/1
R1(config-if)#ipv6 nd other-config-flag 
R1(config-if)#ipv6 dhcp server R1-STATELESS
R1(config-if)#
```
- c.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
```
R1#wr
Building configuration...
[OK]
R1#
```
- d.	Перезапустите PC-A.

ПК PC-A перезапущен.
- e.	Проверьте вывод ipconfig /all и обратите внимание на изменения.

![](./images/lab_08_v6_fig_07.png)
- f.	Тестирование подключения с помощью пинга IP-адреса интерфейса G0/1 R2.

![](./images/lab_08_v6_fig_08.png)
## Часть 4. Настройка сервера DHCPv6 с сохранением состояния на R1.
- a.	Создайте пул DHCPv6 на R1 для сети 2001:db8:acad:3:aaa::/80. Это предоставит адреса локальной сети, подключенной к интерфейсу G0/0/1 на R2. В составе пула задайте DNS-сервер 2001:db8:acad: :254 и задайте доменное имя STATEFUL.com.
```
R1(config)#ipv6 dhcp pool R2-STATEFUL
R1(config-dhcpv6)#address prefix 2001:db8:acad:3:aaa::/80
R1(config-dhcpv6)#dns-server 2001:db8:acad::254
R1(config-dhcpv6)#domain-name STATEFUL.com
R1(config-dhcpv6)#
```
- b.	Назначьте только что созданный пул DHCPv6 интерфейсу g0/0/0 на R1.
```
R1(config)#interface g0/0/0
R1(config-if)#ipv6 dhcp server R2-STATEFUL
R1(config-if)#
```
## Часть 5. Настройка и проверка ретрансляции DHCPv6 на R2.
### Шаг 1. Включите PC-B и проверьте адрес SLAAC, который он генерирует.
![](./images/lab_08_v6_fig_09.png)
### Шаг 2. Настройте R2 в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1.
CPT не поддерживает функционал ipv6 dhcp relay, в связи с этим произведём настройку DHCPv6 на маршрутизаторе R2.
Однако прежде удалим созданный на коммутаторе R1 пул DHCPv6 и его привязку к интерфейсу g0/0/0.
```
R1(config)#no ipv6 dhcp pool R2-STATEFUL
R1(config)#interface gigabitEthernet 0/0/0
R1(config-if)#no ipv6 dhcp server R2-STATEFUL
R1(config-if)#
```
Теперь настроим пул DHCPv6 на коммутаторе R2 для интерфейса G0/0/1.
```
R2(config)#ipv6 dhcp pool R2-STATEFUL
R2(config-dhcpv6)#address prefix 2001:db8:acad:3:aaa::/80
R2(config-dhcpv6)#dns-server 2001:db8:acad::254
R2(config-dhcpv6)#domain-name STATEFUL.com
R2(config-dhcpv6)#exit
R2(config)#interface g0/0/1
R2(config-if)#ipv6 dhcp server R2-STATEFUL
R2(config-if)#ipv6 nd managed-config-flag
R2(config-if)#
```
### Шаг 3. Попытка получить адрес IPv6 из DHCPv6 на PC-B.
- a.	Перезапустите PC-B.

ПК PC-B перезапущен.
- b.	Откройте командную строку на PC-B и выполните команду ipconfig /all и проверьте выходные данные, чтобы увидеть результаты операции ретрансляции DHCPv6.

![](./images/lab_08_v6_fig_10.png)
- c.	Проверьте подключение с помощью пинга IP-адреса интерфейса R0 G0/0/1.

Полагаю что в пункте опечатка и подразумевался коммутатор R1.

![](./images/lab_08_v6_fig_11.png)
