## Лабраторная работа №8. Настройка DHCPv6.

### Топология.

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/36c0ba8b-303e-483c-844c-34bbd89833ce)

### Таблица адресации.

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/05003610-49de-4f94-9240-6f883bdbc910)

### Задачи.

Часть 1. Создание сети и настройка основных параметров устройства.

Часть 2. Проверка назначения адреса SLAAC от R1.

Часть 3. Настройка и проверка сервера DHCPv6 без гражданства на R1.

Часть 4. Настройка и проверка состояния DHCPv6 сервера на R1.

Часть 5. Настройка и проверка DHCPv6 Relay на R2.


### Выполнение задания.

#### Часть 1. Создание сети и настройка основных параметров устройства.

- Шаг 1. Создаем сеть согласно топологии.

![Сеть](https://github.com/Shure0407/Network_engineer/assets/162669909/93e7861e-ac49-4a2a-a552-39bc8d623553)

- Шаг 2. Настраиваем базовые параметры каждого коммутатора. 

![S1 1](https://github.com/Shure0407/Network_engineer/assets/162669909/56e30437-9e07-4ef6-82e6-69564b34eed4)
![S1 2](https://github.com/Shure0407/Network_engineer/assets/162669909/94421ff3-a112-4c4e-8402-02c37438a8bc)

![S2 1](https://github.com/Shure0407/Network_engineer/assets/162669909/1e123e3f-9006-47ba-b779-53f7514982a0)
![S2 2](https://github.com/Shure0407/Network_engineer/assets/162669909/df400d4a-e194-472c-9965-44907714bced)

- Шаг 3. Произведим базовую настройку маршрутизаторов.

![R1](https://github.com/Shure0407/Network_engineer/assets/162669909/25e022b9-de97-4949-aee7-2388d23b8d0a)

![R2](https://github.com/Shure0407/Network_engineer/assets/162669909/4ce7939c-6ebe-424c-9245-88c6c8563f84)

- Шаг 4. Настройка интерфейсов и маршрутизации для обоих маршрутизаторов.

a. Настраиваем интерфейсы G0/0/0 и G0/0/1 на R1 и R2 с адресами IPv6, указанными в таблице адресаци.

![R1 g000 g001](https://github.com/Shure0407/Network_engineer/assets/162669909/c8e8cfb0-016f-464a-81bc-ae0d6cd308e9)

![R1 g000 g001 link local](https://github.com/Shure0407/Network_engineer/assets/162669909/9163ee29-f78f-45a0-ab3e-ba11209fe23a)

![R2 g000 g001](https://github.com/Shure0407/Network_engineer/assets/162669909/90adf97b-b1e4-423c-9f5c-512a709bd0bb)

![R2 g000 g001 link local](https://github.com/Shure0407/Network_engineer/assets/162669909/ad0b4f71-d8a9-4bf8-a16b-5e2c53967d51)

b. Настраиваем маршрут по умолчанию на каждом маршрутизаторе, который указывает на IP-адрес G0/0/0 на другом маршрутизаторе.

![R1 route](https://github.com/Shure0407/Network_engineer/assets/162669909/6dd7d371-e0c2-4741-ae7e-e0f5db5d00a4)

![R2 route](https://github.com/Shure0407/Network_engineer/assets/162669909/d49e1f97-d178-4697-a0aa-ed186702d235)

с. Убеждаемся, что маршрутизация работает с помощью пинга адреса G0/0/1 R2 из R1.

![R1 route ping g001](https://github.com/Shure0407/Network_engineer/assets/162669909/08217570-a3b9-4c43-86f6-21c15a2622af)

![R2 route ping g001](https://github.com/Shure0407/Network_engineer/assets/162669909/03acbb98-8ca3-48a0-ae6b-b4e7878bcd4c)

#### Часть 2. Проверка назначения адреса SLAAC от R1.

![PC-A IP](https://github.com/Shure0407/Network_engineer/assets/162669909/dab148c4-2257-4b48-bd55-eb014db2677a)

![PC-A ipconfig](https://github.com/Shure0407/Network_engineer/assets/162669909/8e5a7d18-b65e-427c-89dd-8152bb85a463)

Часть адреса с идентификатором хоста берется добавлением в 5-8 октеты ***63FE FF41 7C83*** частей МАС-адреса ***0001.6341.7C83***.


#### Часть 3. Настройка и проверка сервера DHCPv6 на R1.

- Шаг 1. Более подробно изучаем конфигурацию PC-A.

![PC-A ipconfig all](https://github.com/Shure0407/Network_engineer/assets/162669909/96b0faca-56a7-4409-b7f7-9c6036803801)

- Шаг 2. Настраиваем R1 для предоставления DHCPv6 без состояния для PC-A.

a. Создаем пул DHCP IPv6 на R1 с именем R1-STATELESS. В составе этого пула назначаем адрес DNS-сервера как 2001:db8:acad: :1, а имя домена — как stateless.com.

b. Настройте интерфейс G0/0/1 на R1, чтобы предоставить флаг конфигурации OTHER для локальной сети R1 и укажите только что созданный пул DHCP в качестве ресурса DHCP для этого интерфейса.

c. сохраняем конфигурацию.

![R1 dhcp pool ](https://github.com/Shure0407/Network_engineer/assets/162669909/2257111c-620d-4eea-9488-d75a8fc8464d)

e. Проверяем вывод ***ipconfig /all***

![PC-A ipconfig all after dhcp pool](https://github.com/Shure0407/Network_engineer/assets/162669909/9dc5061f-8b0f-44ee-b090-a74c077aba09)

f. Тестирование подключения с помощью пинга IP-адреса интерфейса G0/1 R2.

![ping PC-A to R2 g001](https://github.com/Shure0407/Network_engineer/assets/162669909/c0e85652-44e2-4e63-b42f-6b8817162408)

#### Часть 4. Настройка сервера DHCPv6 с сохранением состояния на R1.

a. Создаем пул DHCPv6 на R1 для сети 2001:db8:acad:3:aaa::/80. Это предоставит адреса локальной сети, подключенной к интерфейсу G0/0/1 на R2. 
В составе пула задаем DNS-сервер 2001:db8:acad::254 и задаем доменное имя STATEFUL.com.

b. Назначаем только что созданный пул DHCPv6 интерфейсу g0/0/0 на R1.

![R1 dhcp pool  g000](https://github.com/Shure0407/Network_engineer/assets/162669909/81434b5b-34cb-45e7-9839-c1cd348df2c5)

#### Часть 5. Настройка и проверка ретрансляции DHCPv6 на R2.


- Шаг 1. Включите PC-B и проверьте адрес SLAAC, который он генерирует.

![PC-B IP](https://github.com/Shure0407/Network_engineer/assets/162669909/a2b9e05b-88df-41f9-82c7-b1eeeac7a7b5)

![PC-B ipconfig all](https://github.com/Shure0407/Network_engineer/assets/162669909/47b60ba6-e78d-4eb1-a1ec-e30bea4ac26b)

- Шаг 2. Настройте R2 в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1.


- Шаг 3. Попытка получить адрес IPv6 из DHCPv6 на PC-B.