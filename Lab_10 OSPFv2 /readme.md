## Лабораторная работа №10. Настройка протокола OSPFv2 для одной области.

### Топология.

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/f55b4d10-d7c4-47ad-b3c9-f67b7972a97c)

### Таблица адресации.

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/1d4e1819-a028-47c4-9dd0-f8be9c8ab0df)

### Задачи.

Часть 1. Создание сети и настройка основных параметров устройства.

Часть 2. Настройка и проверка базовой работы протокола  OSPFv2 для одной области.

Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области.

### Выполнение задания.

#### Часть 1. Создание сети и настройка основных параметров устройства.

- Шаг 1. Создаем сеть согласно топологии.

![Net](https://github.com/Shure0407/Network_engineer/assets/162669909/bfd8f446-3ef2-4c21-99a5-7521bf09ea86)

- Шаг 2. Произведим базовую настройку маршрутизаторов.

R1:

![R1 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/29683091-0a05-4eb3-84a1-5b7f929920b5)

R2:

![R2 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/d6b4e517-163f-439c-b8df-fa38167cb34a)

- Шаг 3. Настраиваем базовые параметры каждого коммутатора.

S1:

![S1 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/2c164633-47fd-4477-ac0a-82c48eddc324)

S2:

![S2 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/b77e7e19-846f-4b77-b7dc-c3a381272ba4)


#### Часть 2. Настройка и проверка базовой работы протокола OSPFv2 для одной области.

- Шаг 1. Настройте адреса интерфейса и базового OSPFv2 на каждом маршрутизаторе.

Настраиваем адреса интерфейсов на каждом маршрутизаторе, как показано в таблице адресации.

R1:

![R1 interface](https://github.com/Shure0407/Network_engineer/assets/162669909/017dc798-3152-4d65-b1b1-1cc1cfb1c45e)

R2:

![R2 interface](https://github.com/Shure0407/Network_engineer/assets/162669909/289d6c01-46f9-4baa-b0a9-16c09869c1a1)

Переходим в режим конфигурации маршрутизатора OSPF, используя идентификатор процесса 56.
Настраиваем статический идентификатор маршрутизатора для каждого маршрутизатора (1.1.1.1 для R1, 2.2.2.2 для R2).
Настраиваем интерфейсы сети для сети между R1 и R2, поместив ее в область 0.
Только на R2 добавляем конфигурацию, необходимую для объявления сети Loopback 1 в область OSPF 0.

![R1 ospf](https://github.com/Shure0407/Network_engineer/assets/162669909/227879df-bb02-47b0-badb-3a4768f0be4d)

![R2 ospf](https://github.com/Shure0407/Network_engineer/assets/162669909/8f91d2c3-d47c-4022-b22e-38a95ebd9d4a)

Убеждаемся, что OSPFv2 работает между маршрутизаторами. Выполняем команду ***show ip ospf neighbor***, чтобы убедиться, что R1 и R2 сформировали смежность.

![R1 sh ospf neighbor](https://github.com/Shure0407/Network_engineer/assets/162669909/6b1c08bc-a9fe-4977-9c71-e1b6458d6d5f)

![R2 sh ospf neighbor](https://github.com/Shure0407/Network_engineer/assets/162669909/98ffda37-fede-467e-896f-b5fd016f802f)

На R1 выполняем команду ***show ip route ospf***, чтобы убедиться, что сеть R2 Loopback1 присутствует в таблице маршрутизации.

![R1 sh ospf](https://github.com/Shure0407/Network_engineer/assets/162669909/4e7bcd0a-1b28-4853-bf34-8d414535dbf5)


#### Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области.

- Шаг 1. Реализация различных оптимизаций на каждом маршрутизаторе.

На R1 настраиваем приоритет OSPF интерфейса G0/0/1 на 50, чтобы убедиться, что R1 является назначенным маршрутизатором.
Настраиваем таймеры ***hello*** и ***dead*** OSPF на G0/0/1 каждого маршрутизатора: для таймера приветствия, составляющего 30 секунд.

![R1 g001 priority time heldead](https://github.com/Shure0407/Network_engineer/assets/162669909/34111815-5fe8-4152-b44b-867fd99a041b)

![R2 time hello dead](https://github.com/Shure0407/Network_engineer/assets/162669909/5dda5e46-a99e-483f-a4c8-fab3ee56e432)

На R1 настраиваем статический маршрут по умолчанию, который использует интерфейс Loopback 1 в качестве интерфейса выхода. 
Затем распространяем маршрут по умолчанию в OSPF. 

![R1 ip route Lo1 ](https://github.com/Shure0407/Network_engineer/assets/162669909/c0cba5c3-1388-407a-a6be-5424950e16bc)

Добавляем конфигурацию, необходимую для OSPF для обработки R2 Loopback 1 как сети точка-точка. 
Это приводит к тому, что OSPF объявляет Loopback 1 использует маску подсети интерфейса.

![R1 Lo1 p-t-p](https://github.com/Shure0407/Network_engineer/assets/162669909/e9fc9d89-3d18-4cbf-a2ff-f64b1d8368a1)

Только на R2 добавляем конфигурацию, необходимую для предотвращения отправки объявлений OSPF в сеть Loopback 1.

![R2 no ospf to Lo1](https://github.com/Shure0407/Network_engineer/assets/162669909/8f53037d-f7c3-45d3-bce3-a46813017f49)

Изменяем базовую пропускную способность для маршрутизаторов. 
После этой настройки перезапускаем OSPF с помощью команды ***clear ip ospf process***. 
(Обратите внимание на сообщение консоли после установки новой опорной полосы пропускания.)

R1:

![R1 cost   clear](https://github.com/Shure0407/Network_engineer/assets/162669909/bb24b931-e45a-40d3-a64b-e0bde81e8bc7)

R2:

![R2 cost   clear](https://github.com/Shure0407/Network_engineer/assets/162669909/65a6e36b-6924-4ebb-9970-fdf68f47d265)

- Шаг 2. Убедитесь, что оптимизация OSPFv2 реализовалась.

Выполняем команду ***show ip ospf interface g0/0/1*** на R1 и убеждаемся, что приоритет интерфейса установлен равным 50, 
а временные интервалы — Hello 30, Dead 120, а тип сети по умолчанию — Broadcast

![R1 sh ospf int g001](https://github.com/Shure0407/Network_engineer/assets/162669909/1c8cad34-c87f-482f-bc39-ae5116bf5fad)

На R1 выполняем команду ***show ip route ospf***, чтобы убедиться, что сеть R2 Loopback1 присутствует в таблице маршрутизации. 
(Обратите внимание на разницу в метрике между этим выходным и предыдущим выходным. 
Также обратите внимание, что маска теперь составляет 24 бита, в отличие от 32 битов, ранее объявленных.)

![R1 sh ip ospf](https://github.com/Shure0407/Network_engineer/assets/162669909/9e830e3f-97e8-4671-8369-b5666359894e)

Вводим команду ***show ip route ospf*** на маршрутизаторе R2. 
Единственная информация о маршруте OSPF должна быть распространяемый по умолчанию маршрут R1.

![R2 sh ip route ospf](https://github.com/Shure0407/Network_engineer/assets/162669909/e28b8ff9-2edc-4d92-a8b6-ab0afb8c6379)

Запускаем ***Ping*** до адреса интерфейса R1 Loopback 1 из R2. (Выполнение команды ping должно быть успешным.)

![ping R2 to Lo1 R1](https://github.com/Shure0407/Network_engineer/assets/162669909/8def7fd9-ab2b-4a9c-89ee-9f05e016d504)


