## Лабораторная работа №9. Конфигурация безопасности коммутатора.

### Топология.

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/b3b17044-2191-468d-94dc-f8d6304c77a7)

### Таблица адресации.

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/30b53bc5-3e45-4477-8973-355190d121c2)

### Цели.

Часть 1. Настройка основного сетевого устройства.

Часть 2. Настройка сетей VLAN.

Часть 3: Настройки безопасности коммутатора.


### Выполнение задания.


#### Часть 1. Настройка основного сетевого устройства.

- Шаг 1. Создаем сеть.

![Сеть](https://github.com/Shure0407/Network_engineer/assets/162669909/334a80c6-bdef-4d57-bef1-1f4435cafea2)

- Шаг 2. Настройте маршрутизатор R1.

![R1 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/7c308c64-7fa9-4c87-b66f-01d68361074c)

![R1 sh ip int br](https://github.com/Shure0407/Network_engineer/assets/162669909/e9acc010-f7d3-4438-9463-65e35c99765a)

- Шаг 3. Настройка и проверка основных параметров коммутатора.

Настройка коммутатора S1

![S1 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/32453037-3df6-496d-975d-150f586495d2)

Описание интерфейсов S1

![S1 int descript](https://github.com/Shure0407/Network_engineer/assets/162669909/d5c7c7c0-08ad-40b3-bb6c-06789644dc56)

Настройка коммутатора S2

![S2 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/5c58099e-f427-48d7-a278-13ebde8e0d64)

Описание интерфейсов S2

![S2 int descript](https://github.com/Shure0407/Network_engineer/assets/162669909/b9de4c59-6d47-42de-bbfc-8c7581edf1d8)

Настройка default gateway для S1 и S2

![S1 def-gateway](https://github.com/Shure0407/Network_engineer/assets/162669909/9c023b3f-9975-4cd6-bfc5-df8efa93d8a1)

![S2 def-gateway](https://github.com/Shure0407/Network_engineer/assets/162669909/652515ab-91fe-4fe1-a465-cd339a629c09)


#### Часть 2. Настройка сетей VLAN на коммутаторах.

- Шаг 1. Сконфигруриуйте VLAN 10. Сконфигруриуйте SVI для VLAN 10. Настройте VLAN 333 с именем Native на S1 и S2. Настройте VLAN 999 с именем ParkingLot на S1 и S2.

S1

![S1 Vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/1e21dc7d-4e1c-4f7d-994f-83e7af580ce1)

![S1 manag descr](https://github.com/Shure0407/Network_engineer/assets/162669909/de4cd0da-2d1b-43fa-b6bb-37dee288c216)

![S1 Vlan 999 int shut](https://github.com/Shure0407/Network_engineer/assets/162669909/0a563ae0-667b-4045-a0b5-5c27bfdf6d2d)

S2

![S2 Vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/2179c597-2221-47ee-928e-c2955508bab1)

![S2 manag descr](https://github.com/Shure0407/Network_engineer/assets/162669909/18edc473-c3a3-4389-a631-ac85ad92e126)

![S2 Vlan 999 int shut](https://github.com/Shure0407/Network_engineer/assets/162669909/0f1e8f46-ebec-434b-9d37-58a2fe267f3a)

#### Часть 3. Настройки безопасности коммутатора.

- Шаг 1. Релизация магистральных соединений 802.1Q.

- Шаг 2. Настройка портов доступа.

- Шаг 3. Безопасность неиспользуемых портов коммутатора.

- Шаг 4. Документирование и реализация функций безопасности порта.

- Шаг 5. Реализовать безопасность DHCP snooping.

- Шаг 6. Реализация PortFast и BPDU Guard.

- Шаг 7. Проверьте наличие сквозного ⁪подключения.
