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

Сконфигруриуйте VLAN 10. Сконфигруриуйте SVI для VLAN 10. Настройте VLAN 333 с именем Native на S1 и S2. Настройте VLAN 999 с именем ParkingLot на S1 и S2.

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

Настройте все магистральные порты Fa0/1 на обоих коммутаторах для использования VLAN 333 в качестве native VLAN.
Убедитесь, что режим транкинга успешно настроен на всех коммутаторах.

S1:

![S1 int f01](https://github.com/Shure0407/Network_engineer/assets/162669909/277e043b-c137-4924-a0c7-77f97dbe9f02)

![S1 sh int trunk](https://github.com/Shure0407/Network_engineer/assets/162669909/fd7e8eb0-caa0-4b53-8115-bd087df1729d)

S2:

![S2 int f01](https://github.com/Shure0407/Network_engineer/assets/162669909/d833357b-4d67-42b9-98a5-429cffdc0fbd)

Отключить согласование DTP F0/1 на S1 и S2. Проверьте с помощью команды show interfaces.
S1:

![S1 f01 negotiation](https://github.com/Shure0407/Network_engineer/assets/162669909/1b70bfce-3189-4c99-8d6c-41828c23efce)

![S1 f01 show negotiation](https://github.com/Shure0407/Network_engineer/assets/162669909/36c98b2e-76ec-47f6-bd33-948ce2cfe4e3)

S2:

![S2 f01 negotiation](https://github.com/Shure0407/Network_engineer/assets/162669909/dc9d09e1-4e1b-4afe-83de-4d32c428a611)

- Шаг 2. Настройка портов доступа.

На S1 настройте F0/5 и F0/6 в качестве портов доступа и свяжите их с VLAN 10.

![S1 f05](https://github.com/Shure0407/Network_engineer/assets/162669909/24a88212-4acb-4509-9e3d-288b376e33ce)

![S1 f06](https://github.com/Shure0407/Network_engineer/assets/162669909/d97ed44d-2ea2-4c5b-a4f7-f0b6e99c11c9)

На S2 настройте порт доступа Fa0/18 и свяжите его с VLAN 10.

![S2 f018](https://github.com/Shure0407/Network_engineer/assets/162669909/605f4026-1678-4426-8d65-4396325fd1a6)

- Шаг 3. Безопасность неиспользуемых портов коммутатора.

На S1 и S2 переместите неиспользуемые порты из VLAN 1 в VLAN 999 и отключите неиспользуемые порты.

Частично отключил в Части 2.

S1:

![S1 Vlan 999 int shut 2](https://github.com/Shure0407/Network_engineer/assets/162669909/5986f9e9-0ec6-4dea-b156-8c362777e87a)

S2:

![S2 Vlan 999 int shut 2](https://github.com/Shure0407/Network_engineer/assets/162669909/0c0822f1-fd5b-463e-b806-1a75831dea6a)

Убедитесь, что неиспользуемые порты отключены и связаны с VLAN  999, введя команду  show.

S1:

![S1 sh int status](https://github.com/Shure0407/Network_engineer/assets/162669909/e22bce6c-0964-4723-8b5e-7d58a6394cd2)

![S1 sh int trunk sh vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/2c506e7e-fd0a-4798-8bd7-df4c02fac0ca)

S2:

![S2 sh int status](https://github.com/Shure0407/Network_engineer/assets/162669909/3e278759-3984-43da-894d-f4b8794f5c4c)

![S2 sh int trunk sh vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/4b844163-0144-4724-a8b8-89ed465d296b)

- Шаг 4. Документирование и реализация функций безопасности порта.

- Шаг 5. Реализовать безопасность DHCP snooping.

- Шаг 6. Реализация PortFast и BPDU Guard.

- Шаг 7. Проверьте наличие сквозного ⁪подключения.
