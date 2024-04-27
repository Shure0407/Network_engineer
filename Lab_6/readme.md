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

![Vlan S1 ip address](https://github.com/Shure0407/Network_engineer/assets/162669909/6037c211-7d6d-45c3-a264-df940fa7203a)

![Vlan S2 ip address](https://github.com/Shure0407/Network_engineer/assets/162669909/503c5065-61a7-4a62-8ccb-4532a13ece2c)


c. Назначаем все неиспользуемые порты коммутатора VLAN Parking_Lot, настраиваем их для статического режима доступа и административно деактивируем их.

![Откл портов S1](https://github.com/Shure0407/Network_engineer/assets/162669909/a55f8d96-8a61-47e8-a1d0-deb48d9f300a)

![Откл портов S2](https://github.com/Shure0407/Network_engineer/assets/162669909/e1af8119-6583-475c-a67a-346cb5d89856)

- Шаг 2. Назнаем сети VLAN соответствующим интерфейсам коммутатора.

a.Назначаем используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настраиваем их для режима статического доступа.

![S2 f0-6](https://github.com/Shure0407/Network_engineer/assets/162669909/f958bdee-ed6d-4904-a33a-a7c20cc7bb30)

![S2 f0-18](https://github.com/Shure0407/Network_engineer/assets/162669909/d47ef9c7-767f-400f-95f8-9a84b6c06729)



















































































