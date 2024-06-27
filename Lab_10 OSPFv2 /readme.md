## Лабораторная работа №10. Настройка протокола OSPFv2 для одной области.

### Топология

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/f55b4d10-d7c4-47ad-b3c9-f67b7972a97c)

### Таблица адресации

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/1d4e1819-a028-47c4-9dd0-f8be9c8ab0df)

### Задачи.

Часть 1. Создание сети и настройка основных параметров устройства

Часть 2. Настройка и проверка базовой работы протокола  OSPFv2 для одной области

Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области

### Выполнение задания.

#### Часть 1. Создание сети и настройка основных параметров устройства.

- Шаг 1. Создайте сеть согласно топологии.

![Net](https://github.com/Shure0407/Network_engineer/assets/162669909/bfd8f446-3ef2-4c21-99a5-7521bf09ea86)

- Шаг 2. Произведите базовую настройку маршрутизаторов.

R1:

![R1 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/29683091-0a05-4eb3-84a1-5b7f929920b5)

R2:

![R2 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/d6b4e517-163f-439c-b8df-fa38167cb34a)

- Шаг 3. Настройте базовые параметры каждого коммутатора.

S1:

![S1 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/2c164633-47fd-4477-ac0a-82c48eddc324)

S2:

![S2 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/b77e7e19-846f-4b77-b7dc-c3a381272ba4)

#### Часть 2. Настройка и проверка базовой работы протокола OSPFv2 для одной области

- Шаг 1. Настройте адреса интерфейса и базового OSPFv2 на каждом маршрутизаторе.

Настройте адреса интерфейсов на каждом маршрутизаторе, как показано в таблице адресации выше.

R1:

![R1 interface](https://github.com/Shure0407/Network_engineer/assets/162669909/017dc798-3152-4d65-b1b1-1cc1cfb1c45e)

R2:

![R2 interface](https://github.com/Shure0407/Network_engineer/assets/162669909/289d6c01-46f9-4baa-b0a9-16c09869c1a1)

Перейдите в режим конфигурации маршрутизатора OSPF, используя идентификатор процесса 56.
Настройте статический идентификатор маршрутизатора для каждого маршрутизатора (1.1.1.1 для R1, 2.2.2.2 для R2).
Настройте инструкцию сети для сети между R1 и R2, поместив ее в область 0
Только на R2 добавьте конфигурацию, необходимую для объявления сети Loopback 1 в область OSPF 0.

![R1 ospf](https://github.com/Shure0407/Network_engineer/assets/162669909/227879df-bb02-47b0-badb-3a4768f0be4d)

![R2 ospf](https://github.com/Shure0407/Network_engineer/assets/162669909/8f91d2c3-d47c-4022-b22e-38a95ebd9d4a)

Убедитесь, что OSPFv2 работает между маршрутизаторами. Выполните команду, чтобы убедиться, что R1 и R2 сформировали смежность.

![R1 sh ospf neighbor](https://github.com/Shure0407/Network_engineer/assets/162669909/6b1c08bc-a9fe-4977-9c71-e1b6458d6d5f)

![R2 sh ospf neighbor](https://github.com/Shure0407/Network_engineer/assets/162669909/98ffda37-fede-467e-896f-b5fd016f802f)

На R1 выполните команду show ip route ospf, чтобы убедиться, что сеть R2 Loopback1 присутствует в таблице маршрутизации.

![R1 sh ospf](https://github.com/Shure0407/Network_engineer/assets/162669909/4e7bcd0a-1b28-4853-bf34-8d414535dbf5)


#### Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области

- Шаг 1. Реализация различных оптимизаций на каждом маршрутизаторе.


- Шаг 2. Убедитесь, что оптимизация OSPFv2 реализовалась.









