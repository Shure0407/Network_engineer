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

- Шаг 2. Настраиваем маршрутизатор R1.

![R1 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/7c308c64-7fa9-4c87-b66f-01d68361074c)

![R1 sh ip int br](https://github.com/Shure0407/Network_engineer/assets/162669909/e9acc010-f7d3-4438-9463-65e35c99765a)

- Шаг 3. Настраиваем и проверяем основные параметры коммутаторов.

Настройка коммутатора S1:

![S1 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/32453037-3df6-496d-975d-150f586495d2)

Описание интерфейсов S1:

![S1 int descript](https://github.com/Shure0407/Network_engineer/assets/162669909/d5c7c7c0-08ad-40b3-bb6c-06789644dc56)

Настройка коммутатора S2:

![S2 conf](https://github.com/Shure0407/Network_engineer/assets/162669909/5c58099e-f427-48d7-a278-13ebde8e0d64)

Описание интерфейсов S2:

![S2 int descript](https://github.com/Shure0407/Network_engineer/assets/162669909/b9de4c59-6d47-42de-bbfc-8c7581edf1d8)

Настройка default gateway для S1 и S2:

![S1 def-gateway](https://github.com/Shure0407/Network_engineer/assets/162669909/9c023b3f-9975-4cd6-bfc5-df8efa93d8a1)

![S2 def-gateway](https://github.com/Shure0407/Network_engineer/assets/162669909/652515ab-91fe-4fe1-a465-cd339a629c09)


#### Часть 2. Настройка сетей VLAN на коммутаторах.

Сконфигруриуйте VLAN 10. Сконфигруриуйте SVI для VLAN 10. Настройте VLAN 333 с именем Native на S1 и S2. Настройте VLAN 999 с именем ParkingLot на S1 и S2.

S1:

![S1 Vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/1e21dc7d-4e1c-4f7d-994f-83e7af580ce1)

![S1 manag descr](https://github.com/Shure0407/Network_engineer/assets/162669909/de4cd0da-2d1b-43fa-b6bb-37dee288c216)

![S1 Vlan 999 int shut](https://github.com/Shure0407/Network_engineer/assets/162669909/0a563ae0-667b-4045-a0b5-5c27bfdf6d2d)

S2:

![S2 Vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/bc4c01fc-80ef-407e-bb10-57bf1794e55d)

![S2 manag descr](https://github.com/Shure0407/Network_engineer/assets/162669909/18edc473-c3a3-4389-a631-ac85ad92e126)

![S2 Vlan 999 int shut](https://github.com/Shure0407/Network_engineer/assets/162669909/0f1e8f46-ebec-434b-9d37-58a2fe267f3a)

#### Часть 3. Настройки безопасности коммутатора.

- Шаг 1. Релизация магистральных соединений 802.1Q.

Настраиваем все магистральные порты Fa0/1 на обоих коммутаторах для использования VLAN 333 в качестве native VLAN.
Убеждаемся, что режим транкинга успешно настроен на всех коммутаторах.

S1:

![S1 int f01](https://github.com/Shure0407/Network_engineer/assets/162669909/277e043b-c137-4924-a0c7-77f97dbe9f02)

![S1 sh int trunk](https://github.com/Shure0407/Network_engineer/assets/162669909/fd7e8eb0-caa0-4b53-8115-bd087df1729d)

S2:

![S2 int f01](https://github.com/Shure0407/Network_engineer/assets/162669909/d833357b-4d67-42b9-98a5-429cffdc0fbd)

Отключаем согласование DTP F0/1 на S1 и S2. Проверяем с помощью команды show interfaces.

S1:

![S1 f01 negotiation](https://github.com/Shure0407/Network_engineer/assets/162669909/1b70bfce-3189-4c99-8d6c-41828c23efce)

![S1 f01 show negotiation](https://github.com/Shure0407/Network_engineer/assets/162669909/36c98b2e-76ec-47f6-bd33-948ce2cfe4e3)

S2:

![S2 f01 negotiation](https://github.com/Shure0407/Network_engineer/assets/162669909/dc9d09e1-4e1b-4afe-83de-4d32c428a611)

- Шаг 2. Настройка портов доступа.

На S1 настраиваем F0/5 и F0/6 в качестве портов доступа и связываем их с VLAN 10.

![S1 f05](https://github.com/Shure0407/Network_engineer/assets/162669909/24a88212-4acb-4509-9e3d-288b376e33ce)

![S1 f06](https://github.com/Shure0407/Network_engineer/assets/162669909/d97ed44d-2ea2-4c5b-a4f7-f0b6e99c11c9)

На S2 настраиваем порт доступа Fa0/18 и связываем его с VLAN 10.

![S2 f018](https://github.com/Shure0407/Network_engineer/assets/162669909/605f4026-1678-4426-8d65-4396325fd1a6)

- Шаг 3. Безопасность неиспользуемых портов коммутатора.

На S1 и S2 перемещаем неиспользуемые порты из VLAN 1 в VLAN 999 и отключаем неиспользуемые порты.

Частично отключил в Части 2.

S1:

![S1 Vlan 999 int shut 2](https://github.com/Shure0407/Network_engineer/assets/162669909/5986f9e9-0ec6-4dea-b156-8c362777e87a)

S2:

![S2 Vlan 999 int shut 2](https://github.com/Shure0407/Network_engineer/assets/162669909/0c0822f1-fd5b-463e-b806-1a75831dea6a)

Убеждаемся, что неиспользуемые порты отключены и связаны с VLAN  999, введя команду  show.

S1:

![S1 sh int status](https://github.com/Shure0407/Network_engineer/assets/162669909/e22bce6c-0964-4723-8b5e-7d58a6394cd2)

![S1 sh int trunk sh vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/2c506e7e-fd0a-4798-8bd7-df4c02fac0ca)

S2:

![S2 sh int status](https://github.com/Shure0407/Network_engineer/assets/162669909/3e278759-3984-43da-894d-f4b8794f5c4c)

![S2 sh int trunk sh vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/4b844163-0144-4724-a8b8-89ed465d296b)

- Шаг 4. Документирование и реализация функций безопасности порта.

На S1, вводим команду show port-security interface f0/6  для отображения настроек по умолчанию безопасности порта для интерфейса F0/6.

  ![S1 f06  sh port secure before](https://github.com/Shure0407/Network_engineer/assets/162669909/1882abdc-fc3b-4f0d-b2de-bb6279b8e3ee)

На S1 включаем защиту порта на F0 / 6 :

![S1 f06 port secure](https://github.com/Shure0407/Network_engineer/assets/162669909/d8d4291e-f500-4323-9e44-1cfeb5133e73)

Проверка функции безопасности портов на S1 F0/6.

![S1 f06  sh port secure after](https://github.com/Shure0407/Network_engineer/assets/162669909/959303a2-5c1b-481c-86df-07e7ac8b8486)

![S1 f06  sh port secure address](https://github.com/Shure0407/Network_engineer/assets/162669909/2aee9162-6628-41f0-9507-22bba6f1ccf1)

Включаем безопасность порта для F0 / 18 на S2. Настраиваем каждый активный порт доступа таким образом, чтобы он автоматически добавлял адреса МАС, изученные на этом порту, в текущую конфигурацию.

![S2 f018  sh port secure before](https://github.com/Shure0407/Network_engineer/assets/162669909/94ec92f3-b3e6-41b4-92a0-73d6ca03c064)

Настройте следующие параметры безопасности порта на S2 F / 18

![S2 f018 port secure](https://github.com/Shure0407/Network_engineer/assets/162669909/9de2395b-23c5-4192-a366-6804b44eb1ec)

Проверка функции безопасности портов на S2 F0/18.

![S2 f018  sh port secure after](https://github.com/Shure0407/Network_engineer/assets/162669909/8bf48be1-721d-4154-b390-6b91bfe32034)

![S2 f018  sh port secure address](https://github.com/Shure0407/Network_engineer/assets/162669909/de83eb0f-07c3-4c3b-895c-edd15969ff3d)

- Шаг 5. Реализовать безопасность DHCP snooping.

  На S2 включите DHCP snooping и настройте DHCP snooping во VLAN 10.

![S2 dhcp snooping](https://github.com/Shure0407/Network_engineer/assets/162669909/588f0ad9-3783-4b73-b89e-5f468a356041)

  Настройте магистральные порты на S2 как доверенные порты.

![S2 dhcp snooping f01](https://github.com/Shure0407/Network_engineer/assets/162669909/50a87ee3-52bb-4a0b-ada2-edb1cf030df2)
  
  Ограничьте ненадежный порт Fa0/18 на S2 пятью DHCP-пакетами в секунду.

![S2 dhcp snooping rate](https://github.com/Shure0407/Network_engineer/assets/162669909/007b3500-96d7-4e47-9181-1f3bc15cde70)

 Проверка DHCP Snooping на S2. 

 ![S2 show dhcp snooping](https://github.com/Shure0407/Network_engineer/assets/162669909/827915a3-8c5d-455a-b359-e7205fa4a318)

В командной строке на PC-B освободите, а затем обновите IP-адрес.

![PC-B ipconfig](https://github.com/Shure0407/Network_engineer/assets/162669909/7517fd3f-8e75-458f-8e05-f97042c8c2ae)

Проверьте привязку отслеживания DHCP с помощью команды show ip dhcp snooping binding.

![S2 show dhcp snooping binding](https://github.com/Shure0407/Network_engineer/assets/162669909/67039af7-323f-41f9-b73e-099882164b1e)

- Шаг 6. Реализация PortFast и BPDU Guard.

Настройте PortFast на всех портах доступа, которые используются на обоих коммутаторах
Включите защиту BPDU на портах доступа VLAN 10 S1 и S2, подключенных к PC-A и PC-B
Убедитесь, что защита BPDU и PortFast включены на соответствующих портах.

S1:

![S1 portfast](https://github.com/Shure0407/Network_engineer/assets/162669909/a3db0e2a-9b21-4f70-97b4-a6a0337158ef)

S2:

![S2 portfast](https://github.com/Shure0407/Network_engineer/assets/162669909/726b77b3-93b9-4dbd-9286-b12ca40fc8c0)

- Шаг 7. Проверьте наличие сквозного ⁪подключения.

![Ping PC-A](https://github.com/Shure0407/Network_engineer/assets/162669909/b41e65aa-3b03-485f-b1ab-29a85e26bbc0)

![Ping PC-B](https://github.com/Shure0407/Network_engineer/assets/162669909/48949422-e9a9-45cf-9766-4406579e6e9b)

![Ping R1](https://github.com/Shure0407/Network_engineer/assets/162669909/36501ae1-de38-4b43-adc2-475449299cf8)
