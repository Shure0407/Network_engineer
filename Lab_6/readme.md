## Лабораторная работа №6. Внедрение маршрутизации между виртуальными локальными сетями.

### Топология.

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/8c365b50-11e6-412a-845c-c4205f9b7a3b)

### Таблица адресации.

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/42b2af2a-4c7a-46eb-8a1f-b4a16c7d7fdf)

### Таблица VLAN.

![Таблица Vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/191569c1-5fbe-4fcd-aeb9-2d46b744f0ba)

### Задачи.

Часть 1. Создание сети и настройка основных параметров устройства.

Часть 2. Создание сетей VLAN и назначение портов коммутатора.

Часть 3. Настройка транка 802.1Q между коммутаторами.

Часть 4. Настройка маршрутизации между сетями VLAN.

Часть 5. Проверка, что маршрутизация между VLAN работает.

### Выполнение задания.

#### Часть 1. Создание сети и настройка основных параметров устройства.

- Шаг 1. Создаем сеть согласно топологии.

![Сеть](https://github.com/Shure0407/Network_engineer/assets/162669909/53d79953-7688-4ac3-bfe0-5159054e60ea)

- Шаг 2. Настраиваем базовые параметры для маршрутизатора R1.

![R1](https://github.com/Shure0407/Network_engineer/assets/162669909/e7a054f6-2015-4d17-843c-b2abff4cf328)

- Шаг 3. Настраиваем базовые параметры каждого коммутаторов S1 и S2.

![S1](https://github.com/Shure0407/Network_engineer/assets/162669909/f64aae40-4971-4b28-b6db-7b1a56f37778)

![S2](https://github.com/Shure0407/Network_engineer/assets/162669909/0af2b1f6-3f53-43d3-9225-450088a41504)

- Шаг 4. Настраиваем узлы PC-A, PC-B.

![PC-A](https://github.com/Shure0407/Network_engineer/assets/162669909/fc58bb35-010c-40d9-934f-3b7fde835425)

![PC-B](https://github.com/Shure0407/Network_engineer/assets/162669909/090d00f1-492a-4ce0-a919-9c357f3fa7e5)

#### Часть 2. Создание сетей VLAN и назначение портов коммутатора.

- Шаг 1. Создаем сети VLAN на коммутаторах.

а.Создаем и даем название необходимым VLAN на каждом коммутаторе из таблицы выше.

![Vlan S1](https://github.com/Shure0407/Network_engineer/assets/162669909/1e551b60-3613-4d2a-9353-e39eb28530be)

![Vlan S2](https://github.com/Shure0407/Network_engineer/assets/162669909/8020e17c-6ed8-4858-99df-51332dd0728c)


b.Настраиваем интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации.

![Manage vlan10 S1](https://github.com/Shure0407/Network_engineer/assets/162669909/5a6dcc48-a816-4a76-b4c2-258236546df9)

![Manage vlan10 S2](https://github.com/Shure0407/Network_engineer/assets/162669909/7f12d7bc-83ba-4828-819b-cb2691b465ab)

c. Назначаем все неиспользуемые порты коммутатора VLAN Parking_Lot, настраиваем их для статического режима доступа и административно деактивируем их.

![Откл портов S1](https://github.com/Shure0407/Network_engineer/assets/162669909/a55f8d96-8a61-47e8-a1d0-deb48d9f300a)

![Откл портов S2](https://github.com/Shure0407/Network_engineer/assets/162669909/e1af8119-6583-475c-a67a-346cb5d89856)

- Шаг 2. Назнаем сети VLAN соответствующим интерфейсам коммутатора.

a.Назначаем используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настраиваем их для режима статического доступа.

![S2 f0-6](https://github.com/Shure0407/Network_engineer/assets/162669909/f958bdee-ed6d-4904-a33a-a7c20cc7bb30)

![S2 f0-18](https://github.com/Shure0407/Network_engineer/assets/162669909/d47ef9c7-767f-400f-95f8-9a84b6c06729)

b. Проверяем, что VLAN назначены на правильные интерфейсы.


#### Часть 3. Конфигурация магистрального канала стандарта 802.1Q между коммутаторами.

- Шаг 1. Вручную настраиваем магистральный интерфейс F0/1 на коммутаторах S1 и S2.

Настраивем статический транкинг на интерфейсе F0/1 для обоих коммутаторов, установливаем native VLAN 1000 на обоих коммутаторах,
указываем, что VLAN 10, 20, 30 и 1000 могут проходить по транку, проверяем транки, native VLAN и разрешенные VLAN через транк.

![f0-1 S1](https://github.com/Shure0407/Network_engineer/assets/162669909/972e739b-8e62-4c7d-ab2d-6d0b40b298ca)

![sh trunk S1](https://github.com/Shure0407/Network_engineer/assets/162669909/6f98c870-5a4d-43e6-9925-e53cca56a148)

![f0-1 S2](https://github.com/Shure0407/Network_engineer/assets/162669909/fe2c455c-f430-4278-b2bc-0fa3e22793b4)

![sh trunk S2](https://github.com/Shure0407/Network_engineer/assets/162669909/3c7ea977-777a-43db-93a5-b5339995407f)

- Шаг 2. Вручную настраиваем магистральный интерфейс F0/5 на коммутаторе S1.

Настраиваем интерфейс S1 F0/5 с теми же параметрами транка, что и F0/1.
Сохраните текущую конфигурацию в файл загрузочной конфигурации.


Проверка транкинга.



#### Часть 4. Настройка маршрутизации между сетями VLAN.


- Шаг 1. Настраиваем маршрутизатор.

Настраиваем подинтерфейсы для каждой VLAN, как указано в таблице IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q.
Проверяем, что подинтерфейсу для native VLAN не назначен IP-адрес. Включаем описание для каждого подинтерфейса.

![g0-0-1 R1 vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/1a60505c-3d5e-46ab-98c9-2dedcadb6463)

Проверяем, что вспомогательные интерфейсы работают.

![R1 g001 up](https://github.com/Shure0407/Network_engineer/assets/162669909/9c458d7c-881c-49ef-8b0e-5535129b93f3)

#### Часть 5. Проверка: работает ли маршрутизация между VLAN.

- Шаг 1. Выполняем следующие тесты с PC-A. Все должно быть успешно.

a. Отправьте эхо-запрос с PC-A на шлюз по умолчанию.

![ping PCA to default](https://github.com/Shure0407/Network_engineer/assets/162669909/738e3d05-d686-4316-ac1b-8d18301430e4)

b. Отправьте эхо-запрос с PC-A на PC-B.

![ping PCA to PCB](https://github.com/Shure0407/Network_engineer/assets/162669909/8a52a8bd-1290-4fdb-8c2f-e3767ed6ebec)

c. Отправьте команду ping с компьютера PC-A на коммутатор S2.

![ping PCA to S2](https://github.com/Shure0407/Network_engineer/assets/162669909/fc67a393-dcf4-442a-a30d-7b814db6f37c)

- Шаг 2. Пройдите следующий тест с PC-B.

на PC-B выполняем команду tracert на адрес PC-A.

![tracert to PCA](https://github.com/Shure0407/Network_engineer/assets/162669909/aeb93f38-e311-4e21-996f-898763ef5712)

 отображаемый промежуточный IP-адрес 192.168.30.1 шлюз по умолчанию для хоста PC-B

- Шаг 3.Подключение по SSH к S1 и S2

PC-A to S1

![SSH to S1  1](https://github.com/Shure0407/Network_engineer/assets/162669909/1dbc1695-a152-44dc-9b93-bf26053887cd)

![SSH to S1  2](https://github.com/Shure0407/Network_engineer/assets/162669909/8113d38a-0b26-4567-ab55-078bde93c9ad)

PC-A to S2

![SSH to S2  1](https://github.com/Shure0407/Network_engineer/assets/162669909/355abf6d-20cf-44ba-8bfa-7cbc22200ce5)

![SSH to S2  2](https://github.com/Shure0407/Network_engineer/assets/162669909/ad3c74d5-5cf3-490c-a6a6-493253176d99)




