## Лабораторная работа №1. Базовая настройка коммутатора.

### Топология

![топология](https://github.com/Shure0407/Network_engineer/assets/162669909/cdca3b13-dd03-4b90-b0f8-ff38f3cdb80d)

### Таблица адресации
![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/728b67d7-98c8-4fbd-96fd-825ba88d5c18)

### Задачи.
Часть 1. Проверка конфигурации коммутатора по умолчанию

Часть 2. Создание сети и настройка параметров устройства.
- Настройте базовые параметры коммутатора.
- Настройте IP-адрес для ПК.

Часть 3. Проверка сетевых подключений
- Отобразите конфигурацию устройства.
- Протестируйте сквозное соединение, отправив эхо-запрос.
- Протестируйте возможности удаленного управления с помощью Telnet.
__________________________________________________________________________________________________________________

### Выполнение задания.

#### Часть 1. Проверка конфигурации коммутатора по умолчанию

- Шаг 1. Создать сеть согласно топологии.

a. Подключаем к разъему компьютера RS232 и консольному порту Switch0

![](https://github.com/Shure0407/Network_engineer/assets/162669909/ba87b916-0db5-4fe2-b67b-df4e4b38b2d1)

b. На Cisco PT заходим в терминал и подключаемся к Switch0

![Подключение к switch](https://github.com/Shure0407/Network_engineer/assets/162669909/f8c82a5a-9d50-4605-a42b-452d34bb84ca)

Подключаемя через консольный порт для выполнения начальных конфигураций. Без настроенного IP адреса мы не можем подключиться через Telnet или SSH.

- Шаг 2. Проверить настройки коммутатора по умолчанию.

a. Входим в привелигированный режим и вводим команду show running-config

![running-config](https://github.com/Shure0407/Network_engineer/assets/162669909/8860a44f-7368-4cf7-adf4-e18a0c8fd5d1)
![running-config2](https://github.com/Shure0407/Network_engineer/assets/162669909/6f5f6fd6-9308-4f46-8400-e7c44b328dd4)
![флэш память](https://github.com/Shure0407/Network_engineer/assets/162669909/0409d3ef-743c-4231-b0f9-1e89c38952b3)

b. На коммутаторе 2960 имеется 24 интерфейса Fast Ethernet

   На коммутаторе 2960 имеется 2 интерфейса Gigabit Ethernet

   Количество VTY линий от 0 до 15

c. Файл стартовой загрузки не сформирован   

![startup config](https://github.com/Shure0407/Network_engineer/assets/162669909/ac31d4c4-a479-4f29-aaec-bf0f723fe497)

d. IP-адрес сети VLAN 1 не назначен. Данный интерфейс выключен

![Vlan1](https://github.com/Shure0407/Network_engineer/assets/162669909/75a95993-b155-4734-ac88-5e607da5966d)

   Мас адрес интерфейса VLAN1

![Vlan1 MAC](https://github.com/Shure0407/Network_engineer/assets/162669909/67d09cb5-da92-49e3-9864-d202728dd102)

e. Виртуальный порт для удаленного подключения к коммутатору. Количество виртуальных портов равно 16, Каждому порту можно назначить IP адрес IPv4 и маску. 

![Vlan](https://github.com/Shure0407/Network_engineer/assets/162669909/dd528f8b-1681-475c-b4e1-ecd947058d09)

f. При подключении Ethernet кабеля к порту 0/6, интерфейс и линейный протокол "поднялся"

![схема подключения](https://github.com/Shure0407/Network_engineer/assets/162669909/5d116db1-f547-4d46-b247-03597c48cf43)

![Подключение к порту FE0_6](https://github.com/Shure0407/Network_engineer/assets/162669909/5b423f14-dd46-4aa3-8788-85cec6a20489)

g. Версия ОС Cisco IOS на коммутаторе 15.0(2)SE4, файл образа системы с расширением bin.

![OC Cisco vers](https://github.com/Shure0407/Network_engineer/assets/162669909/144ef130-3d36-4e16-80c3-7fd578657b8b)

h. Интерфейс включен. MAC-адрес интерфейса 00:e0:b0:d2:c4:06. Full-duplex, 100Mb/s

![Интерфейс FE0_6](https://github.com/Shure0407/Network_engineer/assets/162669909/f317995a-ae62-4709-87d6-9ff2f4ff4107)

i. Образу Cisco присвоено имя 2960-lanbasek9-mz.150-2.SE4.bin

![флэш память](https://github.com/Shure0407/Network_engineer/assets/162669909/7d8e5789-3668-46a3-8d03-db9c5233946e)

#### Часть 2. Настройка базовых параметров сетевых устройств

- Шаг 1. Настройте базовые параметры коммутатора.

a. В режиме глобальной конфигурации настраиваем базовые параметры и копируем в start-config на коммутаторе

Изменение имени хоста

![Изменение имени хоста](https://github.com/Shure0407/Network_engineer/assets/162669909/48ef2c43-128c-4be0-8ee2-b1e1ac91c11b)

Установка пароля на привилегированный режим

![установка пароля на привелиг режим](https://github.com/Shure0407/Network_engineer/assets/162669909/a07ad063-3022-4cc8-b260-5a08d0f92822)


Включение кодировки пароля

![service pass-encr](https://github.com/Shure0407/Network_engineer/assets/162669909/2c58a02c-970c-4629-9d4c-6c352b39a4d5)

![service pass-encr1](https://github.com/Shure0407/Network_engineer/assets/162669909/841b3142-4fd5-4e5d-a246-b1dec13b345c)

![service pass-encr2](https://github.com/Shure0407/Network_engineer/assets/162669909/72eed2f3-d90c-4163-8a4d-3948f3d6fd24)

Установка приветственного баннера

![Banner](https://github.com/Shure0407/Network_engineer/assets/162669909/b61dcbd3-f129-41b9-9289-c0cd46462c2c)

Настройка виртуальных портов

![line vty](https://github.com/Shure0407/Network_engineer/assets/162669909/4f52dda3-94d7-479a-afc6-4f3a7c3116b9)

Копируем из running-config в start-config на коммутаторе

![copy startup config ](https://github.com/Shure0407/Network_engineer/assets/162669909/5efccba2-27dc-4db7-afbc-9b69a0d1a920)

Загрузочный файл на коммутаторе

![startup config 1](https://github.com/Shure0407/Network_engineer/assets/162669909/a6f963c6-46d2-430c-a20d-2ffa4b6b07a5)

![startup config 2](https://github.com/Shure0407/Network_engineer/assets/162669909/66068f79-8958-4809-acbf-90b2b6e5325a)

b. Назначаем IP-адрес интерфейсу SVI на коммутаторе.

![IP SVI](https://github.com/Shure0407/Network_engineer/assets/162669909/c039c64c-058f-4036-bf5a-09eafb7b7041)

![int vlan в run conf](https://github.com/Shure0407/Network_engineer/assets/162669909/75f20c0b-a607-4356-b192-fd23063ee65d)

c. Установка пароля консольного подключения.

![Установка пароля консоли](https://github.com/Shure0407/Network_engineer/assets/162669909/10929267-0dc2-4391-8afe-4c32936e2510)

d. Настройка каналов виртуального соединения для удаленного управления (vty)

![Настройка подкл vty по протоколу telnet](https://github.com/Shure0407/Network_engineer/assets/162669909/44e8fcb4-0e95-45dd-9a09-b2b7de94cbfd)

- Шаг 2. Настройте IP-адрес на компьютере PC-A.

![IP адрес РС](https://github.com/Shure0407/Network_engineer/assets/162669909/a99baaed-859a-4490-bb22-8d422270e487)

#### Часть 3. Проверка сетевых подключений

- Шаг 1. Конфигурация коммутатора.

a. running-config

![running-config 3](https://github.com/Shure0407/Network_engineer/assets/162669909/2b2400f1-676c-4705-b283-f57ea1affcb6)

![running-config4](https://github.com/Shure0407/Network_engineer/assets/162669909/9ae9d7b8-1903-46ef-b692-e3a52e83a09b)

b. Проверка параметров VLAN 1.
Полоса  пропускания BW - 100000Kbit

![interface vlan1](https://github.com/Shure0407/Network_engineer/assets/162669909/0a63a1a8-342f-4132-ade8-6ff949bb236a)

- Шаг 2. Тестируем сквозное соединение, отправив эхо-запрос.

a. Проверяем связь с адресом PC-A.

![ping to PC](https://github.com/Shure0407/Network_engineer/assets/162669909/04f95dd0-ff07-4ad9-bf6b-3099dc68acc4)

b. Отправляем эхо-запрос на административный адрес интерфейса SVI коммутатора S1

![ping to S1](https://github.com/Shure0407/Network_engineer/assets/162669909/fe261808-246e-4ae0-9d12-495271c50076)

- Шаг 3. Проверка удаленного управления коммутатором S1.

![Telnet подключение](https://github.com/Shure0407/Network_engineer/assets/162669909/a463c0bb-673a-4604-b120-a93a4bc7bc8c)

![Удаленный доступ к S1](https://github.com/Shure0407/Network_engineer/assets/162669909/a5e1815e-fa82-4dfa-982f-70a1c5145ea6)
