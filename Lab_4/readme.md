## Лабораторная работа №4. Настройка IPv6-адресов на сетевых устройствах.

### Топология.

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/e800d2f7-2b96-4386-8e0f-ace783c306e4)

### Таблица адресации.

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/8677f1e3-a908-4889-9264-f9eedf1c1766)

### Задачи.

Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора.

Часть 2. Ручная настройка IPv6-адресов.

Часть 3. Проверка сквозного соединения.

### Выполнение задания.

#### Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора.

- Шаг 1. Настраиваем маршрутизатор.

  

- Шаг 2. Настраиваем коммутатор.

  

#### Часть 2. Ручная настройка IPv6-адресов.

- Шаг 1. Назначаем IPv6-адреса интерфейсам Ethernet на R1.

a. Назнаем глобальные индивидуальные IPv6-адреса, указанные в таблице адресации обоим интерфейсам Ethernet на R1.

Для интерфейса G0/0/0.

![ipv6 for R1 G000](https://github.com/Shure0407/Network_engineer/assets/162669909/4ae213f3-f290-4997-a982-11399f6542b7)

Для интерфейса G0/0/1.

![ipv6 for R1 G001](https://github.com/Shure0407/Network_engineer/assets/162669909/3198ef5a-63bf-4ed4-b554-53b19c81c378)

b. Вводим команду show ipv6 interface brief для проверки.

![show ipv6 for R1 all ](https://github.com/Shure0407/Network_engineer/assets/162669909/24c3e025-4eae-40ee-86cd-b6d79346f524)

MAC адрес G0/0/0 : 0050.***0fb4.8701***  -> локальный адрес : fe80::25***0:f***ff:fe***b4:8701***

MAC адрес G0/0/1 : 0050.***0fb4.8702***  -> локальный адрес : fe80::25***0:f***ff:fe***b4:8702***

c. Чтобы обеспечить соответствие локальных адресов канала индивидуальному адресу, вручную вводим локальные адреса канала на каждом интерфейсе Ethernet на R1.

![link local G000](https://github.com/Shure0407/Network_engineer/assets/162669909/4df034c6-b832-4783-b9e0-7812f2fbe0b8)

![link local G001](https://github.com/Shure0407/Network_engineer/assets/162669909/0752cbe0-7d0e-448d-9cfc-7fa8fcac4480)

d. Проверяем, что локальный адрес связи изменен на fe80::1. 

![show ipv6 for R1 all2](https://github.com/Shure0407/Network_engineer/assets/162669909/69e1f674-fdbe-428e-87ab-d0c3bc1da2c7)

- Шаг 2. Активируем IPv6-маршрутизацию на R1.

a. В командной строке на PC-B вводим команду ipconfig, чтобы получить данные IPv6-адреса, назначенного интерфейсу ПК.
 
На PC-B индивидуальный IPv6-адрес сетевой интерфейсной карте (NIC) ***не назначился***.

![ipconfig до unicast PC B](https://github.com/Shure0407/Network_engineer/assets/162669909/fae227c0-72cd-4424-a50e-b9bb80d0a83a)

b. Активируем IPv6-маршрутизацию на R1 с помощью команды IPv6 unicast-routing.

![unicast](https://github.com/Shure0407/Network_engineer/assets/162669909/32effe70-cf95-4e49-8565-9008962fc9e7)

c. Еще раз проверяем данные IPv6-адреса.

Для PC-B.

![PC-B ipconfig automatic](https://github.com/Shure0407/Network_engineer/assets/162669909/6419bfe5-4d87-44ae-af06-b30044ac4a3e)

Для PC-A.

![PC-A ipconfig automatic](https://github.com/Shure0407/Network_engineer/assets/162669909/3e37fd25-e27d-4ab4-89ca-c40fb1be946c)


- Шаг 3. Назначаем IPv6-адреса интерфейсу управления (SVI) на S1.

a. Назначаем адрес IPv6 для S1. Также назначаем этому интерфейсу локальный адрес канала.

![ipv6 для S1](https://github.com/Shure0407/Network_engineer/assets/162669909/91671bc7-d5c9-4ca2-8d52-8900523015b2)

![link local vlan1 S1](https://github.com/Shure0407/Network_engineer/assets/162669909/0d54e4ed-9491-4462-a6c3-ac0dfbbaf438)


b. Проверяем правильность назначения IPv6-адресов интерфейсу управления.

![show ipv6 для S1 br](https://github.com/Shure0407/Network_engineer/assets/162669909/ba35354b-65b2-47fa-a7e8-55d068516f0d)


- Шаг 4.Назначаем компьютерам статические IPv6-адреса.

a. Открываем окно IP configuration для каждого ПК и назначаем адресацию IPv6.

![PC A ipv6](https://github.com/Shure0407/Network_engineer/assets/162669909/e315af42-a151-469d-b0a4-69849da777d2)

![PC B ipv6](https://github.com/Shure0407/Network_engineer/assets/162669909/6c670a95-6c46-4ef9-8c23-400b6cad0e03)

b. Проверяем, что оба компьютера имеют правильную информацию адреса IPv6

![IP config auto PC A](https://github.com/Shure0407/Network_engineer/assets/162669909/9f4f48fb-2ce7-4ebc-b9a6-a8b1ba7c0fcd)

![IP config auto PC B](https://github.com/Shure0407/Network_engineer/assets/162669909/f929cb65-803c-4e0e-9c73-e773cc1d4559)

![PC-A ipconfig](https://github.com/Shure0407/Network_engineer/assets/162669909/6f1f7b5a-c7b1-4c12-b501-17ccd7e60260)

![PC-B ipconfig](https://github.com/Shure0407/Network_engineer/assets/162669909/79ee56e3-4d77-43a9-a2ea-5894525d3e02)


#### Часть 3. Проверка сквозного подключения.

a. С PC-A отправляем эхо-запрос на локальный адрес интерфейса G 0/0/1 на R1: FE80::1. 

![ping PC A to fe80 1](https://github.com/Shure0407/Network_engineer/assets/162669909/834feb11-f98a-4b67-9fb3-f635143a4f99)

b. Отправляем эхо-запрос с PC-A на интерфейс управления S1.

![ping PC A to fe80 5 S1](https://github.com/Shure0407/Network_engineer/assets/162669909/921b2eda-7712-4b57-91c5-97c5aa434720)

с. Вводим команду tracert на PC-A, чтобы проверить наличие сквозного подключения к PC-B.

С PC-B отправляем эхо-запрос на PC-A.

![tracert](https://github.com/Shure0407/Network_engineer/assets/162669909/8af206fa-489d-4d5b-9a78-c2109c903d98)

![ping PC B to PC A](https://github.com/Shure0407/Network_engineer/assets/162669909/6dbee0aa-ec4a-4b94-8a42-89b77e481468)

d. С PC-B отправляем эхо-запрос на локальный адрес канала интерфейса G0/0/0 на R1.

![ping PC B to fe80 1 G000 R1](https://github.com/Shure0407/Network_engineer/assets/162669909/7854409e-34db-4205-8852-97126e7587a0)
