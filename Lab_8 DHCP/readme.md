## Лабраторная работа №8.1. Настройка DHCPv6.

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

- Шаг 2. Создаем пул DHCPv6 на R2 для сети 2001:db8:acad:3:aaa::/80. Это предоставит адреса локальной сети, подключенной к интерфейсу G0/0/1 на R2. 
В составе пула задаем DNS-сервер 2001:db8:acad::254 и задаем доменное имя STATEFUL.com.


- Шаг 3. Попытка получить адрес IPv6 из DHCPv6 на PC-B.




## Лабраторная работа №8.2. Реализация DHCPv4.

### Топология.

![Topology](https://github.com/Shure0407/Network_engineer/assets/162669909/9b99cb0e-fbd5-47b0-8634-0eaeea77f2b6)

### Таблица адресации.

![Address table](https://github.com/Shure0407/Network_engineer/assets/162669909/db39b214-bcdb-481b-a833-195874cd95d6)

### Таблица VLAN.

![VLAN table](https://github.com/Shure0407/Network_engineer/assets/162669909/fd7af04a-654a-4aed-8543-ebd0b0871cee)

### Задачи.

Часть 1. Создание сети и настройка основных параметров устройства.

Часть 2. Настройка и проверка двух серверов DHCPv4 на R1.

Часть 3. Настройка и проверка DHCP-ретрансляции на R2.

### Выполнение задания.

#### Часть 1.	Создание сети и настройка основных параметров устройства.

- Шаг 1.	Создание схемы адресации.

a. Одна подсеть «Подсеть A», поддерживающая 58 хостов (клиентская VLAN на R1).
Подсеть A. Первый IP-адрес в таблице адресации для R1 G0/0/1.100

b. Одна подсеть «Подсеть B», поддерживающая 28 хостов (управляющая VLAN на R1). 
Подсеть B: Первый IP-адрес в таблице адресации для R1 G0/0/1.200. Второй IP-адрес в таблице адресов для S1 VLAN 200 и введите соответствующий шлюз по умолчанию.

c. Одна подсеть «Подсеть C», поддерживающая 12 узлов (клиентская сеть на R2).
Подсеть C: Первый IP-адрес в таблице адресации для R2 G0/0/1.

![Создание схемы адресации](https://github.com/user-attachments/assets/ddd11e6a-4ee1-4f61-8632-1bbdd85bca44)

- Шаг 2.	Создаем сеть согласно топологии.

![Сеть DHCPv4](https://github.com/user-attachments/assets/3f3c938e-2db7-4f7f-8e60-5aed28e2fd7f)

- Шаг 3.	Произведим базовую настройку маршрутизаторов.

R1:

![R1](https://github.com/user-attachments/assets/ef20ebd6-b2a5-4214-987b-cdd0a1ff0b91)

R2:

![R2](https://github.com/user-attachments/assets/72f01661-680d-42f8-b8e5-4dc4a7a981e0)

- Шаг 4.	Настраиваем маршрутизации между сетями VLAN на маршрутизаторе R1

a. Активируйте интерфейс G0/0/1 на маршрутизаторе.

b. Настраиваем подинтерфейсы для каждой VLAN в соответствии с требованиями таблицы IP-адресации. Все субинтерфейсы используют инкапсуляцию 802.1Q и назначаются первый полезный адрес из вычисленного пула IP-адресов. Убедитесь, что подинтерфейсу для native VLAN не назначен IP-адрес. Включите описание для каждого подинтерфейса.

![R1 Sub int](https://github.com/user-attachments/assets/c654c5a6-3f64-4ee5-8776-d2b6ddff6567)

с. Проверяем, что вспомогательные интерфейсы работают.

![R1 sh ip int br](https://github.com/user-attachments/assets/39c7ca8c-01a4-4255-8b0b-09c52d3f9f86)

- Шаг 5.	Настройте G0/1 на R2, затем G0/0/0 и статическую маршрутизацию для обоих маршрутизаторов

а. Настраиваем G0/0/1 на R2 с первым IP-адресом подсети C, рассчитанным ранее.

![R2 g001](https://github.com/user-attachments/assets/330610bc-8d2f-44bc-9386-b2c6e5e0e1a6)

b. Настраиваем интерфейс G0/0/0 для каждого маршрутизатора на основе приведенной выше таблицы IP-адресации.

c. Настраиваем маршрут по умолчанию на каждом маршрутизаторе, указываемом на IP-адрес G0/0/0 на другом маршрутизаторе.

![R1 g000   route](https://github.com/user-attachments/assets/be310d6c-0297-4c20-bda7-8e15fe9eafbc)

![R2 route ](https://github.com/user-attachments/assets/d3754366-1b38-419c-b441-632cd5744b0a)

d. Убеждаемся, что статическая маршрутизация работает с помощью пинга до адреса G0/0/1 R2 от R1.

![R1 ping to R2 g001](https://github.com/user-attachments/assets/9c87f9db-56b0-4046-8f4c-33846aed42b7)

с. Сохраняем конфигурацию

- Шаг 6.	Настройте базовые параметры каждого коммутатора.

S1:

![S1 1](https://github.com/user-attachments/assets/51876ee7-1d88-486d-ae35-146eb90c7ea2)

![S1 2](https://github.com/user-attachments/assets/d080a673-1d76-4d54-80aa-53303915506b)

S2:

![S2](https://github.com/user-attachments/assets/469a9e7a-20ad-48eb-8717-e8eb066423cc)

- Шаг 7.	Создайте сети VLAN на коммутаторе S1.

a. Создаем необходимые VLAN на коммутаторе 1 и присваиваем им имена из приведенной выше таблицы.

![S1 VLAN](https://github.com/user-attachments/assets/44cd2817-9a59-47a7-bd10-374663059846)

b. Настраиваем и активируем интерфейс управления на S1 (VLAN 200), используя второй IP-адрес из подсети, рассчитанный ранее. Кроме того устанавливаем шлюз по умолчанию на S1.

![S1 vlan 200](https://github.com/user-attachments/assets/a396dc21-5698-4d7c-ad24-c92329884e2b)

с. Настраиваем и активируем интерфейс управления на S2 (VLAN 1), используя второй IP-адрес из подсети, рассчитанный ранее. Кроме того, устанавливаем шлюз по умолчанию на S2

![S2 Vlan 1](https://github.com/user-attachments/assets/c2552ff3-a511-4065-b0c5-34c845cb5bb0)

d. Назначаем все неиспользуемые порты S1 VLAN Parking_Lot, настраиваем их для статического режима доступа и административно деактивируем их. На S2 административно деактивируем все неиспользуемые порты.

S1:

![S1 vlan 999 shutdown](https://github.com/user-attachments/assets/bbd2658d-a313-49fc-a0eb-24813fa4cd8c)

S2:

![S2 shutdown](https://github.com/user-attachments/assets/9be4a7f4-ef22-4715-a2e0-bd7f14d9343a)

-Шаг 8.	Назначьте сети VLAN соответствующим интерфейсам коммутатора.

S1:

![S1 int f06](https://github.com/user-attachments/assets/3687a5ce-4f3f-48dc-b978-b4c6dd876234)

S2:

![S2 int f018](https://github.com/user-attachments/assets/7de0ff5b-4bee-4901-b011-4313c2b9b314)

- Шаг 9.	Вручную настройте интерфейс S1 F0/5 в качестве транка 802.1Q.

a. Изменяем режим порта коммутатора, чтобы принудительно создать магистральный канал.

b. В рамках конфигурации транка  устанавливаем для native  VLAN значение 1000.

c. В качестве другой части конфигурации магистрали указываем, что VLAN 100, 200 и 1000 могут проходить по транку.
                
d. Сохраняем текущую конфигурацию в файл загрузочной конфигурации.

е. Проверяем состояние транка.

![S1 f05 trunk](https://github.com/user-attachments/assets/63aaad18-a61b-49d2-964c-fc766eba5e7a)

![S1 sh vlan](https://github.com/user-attachments/assets/f5c65c0f-36ea-419e-a41a-ffedd36bac2e)

![S2 sh vlan](https://github.com/user-attachments/assets/fbe526f6-b4ad-4a98-961f-fb727ffcfaf7)

#### Часть 2.	Настройка и проверка двух серверов DHCPv4 на R1.


- Шаг 1.	Настраиваем R1 с пулами DHCPv4 для двух поддерживаемых подсетей. Ниже приведен только пул DHCP для подсети A

a. Исключаем первые пять используемых адресов из каждого пула адресов.

b. Создаем пул DHCP (используйте уникальное имя для каждого пула).

c. Указываем сеть, поддерживающую этот DHCP-сервер.

d. В качестве имени домена указываем CCNA-lab.com.

e. Настраиваем соответствующий шлюз по умолчанию для каждого пула DHCP.

f. Настраиваем время аренды на 2 дня 12 часов и 30 минут.

g. Затем настраиваем второй пул DHCPv4, используя имя пула R2_Client_LAN и 
вычислите сеть, маршрутизатор по умолчанию, и используйте то же имя домена и время аренды, что и предыдущий пул DHCP.

![R1 dhcp](https://github.com/user-attachments/assets/a553b215-4d06-42e4-ac27-7c6c247036d4)

- Шаг 2.	Сохраните конфигурацию.

- Шаг 3.	Проверка конфигурации сервера DHCPv4

![R1 dhcp binding   pool](https://github.com/user-attachments/assets/f7b5fc4e-8564-4fa6-821b-b31048982d22)


- Шаг 4.	Попытка получить IP-адрес от DHCP на PC-A

![PC-A IP dhcp](https://github.com/user-attachments/assets/9f6c765d-a996-4c2c-9e0a-5ce1606a54a1)

![PC-A ipconfig](https://github.com/user-attachments/assets/9f7a1130-906b-44f9-9ed1-ef67659b9edb)

Проверяем подключение с помощью пинга IP-адреса интерфейса R1 G0/0/1.

![PC-A ping](https://github.com/user-attachments/assets/d050377a-3624-43c3-a948-93690f0b6c45)


#### Часть 3.	Настройка и проверка DHCP-ретрансляции на R2.

- Шаг 1.	Настраиваем R2 с пулом DHCPv4

![R2 dhcp](https://github.com/user-attachments/assets/94b8cc26-3a9f-4019-a48c-26965f326bcd)

- Шаг 2.	Попытка получить IP-адрес от DHCP на PC-B

![PC-B IP dhcp](https://github.com/user-attachments/assets/d698d7bf-7886-44a9-ac55-63bbf5dcb62a)

![R2 dhcp binding   pool](https://github.com/user-attachments/assets/290a2aee-8ef9-423d-9b18-ea182cc25939)




