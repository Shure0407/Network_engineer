## Лабораторная работа №4. Настройка IPv6-адресов на сетевых устройствах.

### Топология.

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/e800d2f7-2b96-4386-8e0f-ace783c306e4)

### Таблица адресации.

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/8677f1e3-a908-4889-9264-f9eedf1c1766)

### Задачи

Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора

Часть 2. Ручная настройка IPv6-адресов

Часть 3. Проверка сквозного соединения

### Выполнение задания.

#### Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора

- Шаг 1. Настройте маршрутизатор.

- Шаг 2. Настройте коммутатор.

#### Часть 2. Ручная настройка IPv6-адресов.

- Шаг 1. Назначьте IPv6-адреса интерфейсам Ethernet на R1.

a. 

b. 

c.

d. 

- Шаг 2. Активируйте IPv6-маршрутизацию на R1.

a. В командной строке на PC-B вводим команду ipconfig, чтобы получить данные IPv6-адреса, назначенного интерфейсу ПК.
 
На PC-B индивидуальный IPv6-адрес сетевой интерфейсной карте (NIC) ***не назначился***.

![ipconfig до unicast](https://github.com/Shure0407/Network_engineer/assets/162669909/4479fb5a-9d8c-428d-a5e7-0e015bb81f81)

b. Активируем IPv6-маршрутизацию на R1 с помощью команды IPv6 unicast-routing

![unicast](https://github.com/Shure0407/Network_engineer/assets/162669909/32effe70-cf95-4e49-8565-9008962fc9e7)

c. Еще раз проверяем данные IPv6-адреса.

Для PC-B

![PC-B ipconfig automatic](https://github.com/Shure0407/Network_engineer/assets/162669909/6419bfe5-4d87-44ae-af06-b30044ac4a3e)

Для PC-A

![PC-A ipconfig automatic](https://github.com/Shure0407/Network_engineer/assets/162669909/3e37fd25-e27d-4ab4-89ca-c40fb1be946c)


- Шаг 3. Назначьте IPv6-адреса интерфейсу управления (SVI) на S1.

a. 

b. 

- Шаг 4.Назначьте компьютерам статические IPv6-адреса.

a. Открываем окно IP configuration для каждого ПК и назначаем адресацию IPv6.

![PC A ipv6](https://github.com/Shure0407/Network_engineer/assets/162669909/e315af42-a151-469d-b0a4-69849da777d2)

![PC B ipv6](https://github.com/Shure0407/Network_engineer/assets/162669909/5b738741-cc59-4349-9e1b-bd04147336c7)

b. Проверяем адресацию.

![PC-A ipconfig](https://github.com/Shure0407/Network_engineer/assets/162669909/6f1f7b5a-c7b1-4c12-b501-17ccd7e60260)

![PC-B ipconfig](https://github.com/Shure0407/Network_engineer/assets/162669909/79ee56e3-4d77-43a9-a2ea-5894525d3e02)



#### Часть 3. Проверка сквозного подключения

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
