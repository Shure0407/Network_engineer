## Лабораторная работа №11. Настройка и проверка расширенных списков контроля доступа.

### Топология.

![Topology](https://github.com/user-attachments/assets/68cd0b56-887b-48b5-b9da-4f21ece30d8a)

### Таблица адресации.

![Address table](https://github.com/user-attachments/assets/f4976d9f-61ca-4758-93a7-f0a49e25ce55)

### Таблица VLAN.

![VLAN table](https://github.com/user-attachments/assets/1edc3539-9e8b-4d51-b467-b5c690a0ca1b)

## Задачи.

Часть 1. Создание сети и настройка основных параметров устройства.

Часть 2. Настройка и проверка списков расширенного контроля доступа.

### Выполнение задания.

#### Часть 1. Создание сети и настройка основных параметров устройства. 

- Шаг 1. Создаем сеть согласно топологии.

![Net 11](https://github.com/user-attachments/assets/3f28558f-c9ea-4737-bd6b-23b0848db910)

- Шаг 2. Произведим базовую настройку маршрутизаторов.

R1:

![R1](https://github.com/user-attachments/assets/05dfcf8f-b3da-4273-b411-193c94605bee)

R2:

![R2](https://github.com/user-attachments/assets/5d176962-50a1-4132-8107-7ed223b08d33)

- Шаг 3. Настраиваем базовые параметры каждого коммутатора.

S1:

![S1](https://github.com/user-attachments/assets/894e0cf5-a99d-4076-8028-da95055867a5)

S2:

![S2](https://github.com/user-attachments/assets/98f5c582-4cc4-4756-9480-165a7c2d6c0f)

#### Часть 2. Настройка сетей VLAN на коммутаторах.

- Шаг 1. Создаем сети VLAN на коммутаторах.

a.	Создаем необходимые VLAN и называем их на каждом коммутаторе из приведенной выше таблицы.

S1:

![S1 make VLAN](https://github.com/user-attachments/assets/efd27fdf-f7e3-486d-83fb-e656bfdfbf08)

S2:

![S2 make VLAN](https://github.com/user-attachments/assets/3443320c-8841-4f38-b961-89e23f5f5792)

b.	Настраиваем интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации. 

S1:

![S1 int vlan 20](https://github.com/user-attachments/assets/fc68a6a1-b110-4d37-b3e0-140f942a08c9)

S2:

![S2 int vlan 20](https://github.com/user-attachments/assets/7298998e-80b7-4589-8f8c-61e5192e2e0d)

c.	Назначаем все неиспользуемые порты коммутатора VLAN Parking Lot, настраиваем их для статического режима доступа и административно деактивируем их.

S1:

![S1 vlan 999 1](https://github.com/user-attachments/assets/0513b341-96b9-4f7c-9f43-d2f30439ca8a)
![S1 vlan 999 2](https://github.com/user-attachments/assets/8e95d41f-e559-4e26-af2d-975f45df278e)


S2:

![S2 vlan 999 1](https://github.com/user-attachments/assets/320e7129-679e-488f-8283-bbcf5d88b006)
![S2 vlan 999 2](https://github.com/user-attachments/assets/3c4b5ed4-d8d1-49c8-840f-055d2b05e384)


- Шаг 2. Назначаем сети VLAN соответствующим интерфейсам коммутатора.

a.	Назначаем используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настраиваем их для режима статического доступа.

S1:

![S1 int f06](https://github.com/user-attachments/assets/567a2499-9fd3-4ab9-bab8-3c2de6d37cc3)

S2:

![S2 int f05](https://github.com/user-attachments/assets/828ebcf2-e926-438d-8c0f-9b25553605a0)

![S2 int f018](https://github.com/user-attachments/assets/eb28d946-dabf-4f53-8946-1761cc10960c)

b.	Выполняем команду ***show vlan brief***, чтобы убедиться, что сети VLAN назначены правильным интерфейсам

S1:

![S1 sh vlan br](https://github.com/user-attachments/assets/bbc23673-94bb-4fdd-88f8-c1549a92c59c)

S2:

![S2 sh vlan br](https://github.com/user-attachments/assets/8f2cbfaf-7fd8-4076-a555-eb1a8e6d519e)

#### Часть 3. Настройте транки (магистральные каналы).

- Шаг 1. Вручную настройте магистральный интерфейс F0/1.
- 
a.	Изменяем режим порта коммутатора на интерфейсе F0/1 на обоих коммутаторах, чтобы принудительно создать магистральную связь.

b.	В рамках конфигурации транка установливаем для native vlan значение 1000 на обоих коммутаторах. 
При настройке двух интерфейсов для разных собственных VLAN сообщения об ошибках могут отображаться временно.

c.	Указываем, что VLAN 10, 20, 30 и 1000 разрешены в транке.

S1:

![S1 trunk f01](https://github.com/user-attachments/assets/f35d8fe5-49e7-4367-bde6-b7440dab6edd)

S2:

![S2 trunk f01](https://github.com/user-attachments/assets/25e76a32-8f8e-440e-bd89-8b886e9a6b4c)

d.	Выполняем команду ***show interfaces trunk*** для проверки портов магистрали, собственной VLAN и разрешенных VLAN через магистраль.

S1:

![S1 sh int trunk f01](https://github.com/user-attachments/assets/54ec16f5-fb24-417e-b282-aecfdbedc646)

S2:

![S2 sh int trunk f01](https://github.com/user-attachments/assets/5f1076f2-998e-45f3-9b93-03b13848d42a)

- Шаг 2. Вручную настройте магистральный интерфейс F0/5 на коммутаторе S1.

a.	Настраиваем интерфейс S1 F0/5 с теми же параметрами транка, что и F0/1. Это транк до маршрутизатора.
b.	Сохраняем текущую конфигурацию в файл загрузочной конфигурации.

![S1 trunk f05](https://github.com/user-attachments/assets/1c8eb509-b2f8-475d-8494-15128d6e47b9)

c.	После активации интерфейса G0/0/1 на R1 используем команду ***show interfaces trunk*** для проверки настроек транка.

![R1 int g001](https://github.com/user-attachments/assets/a4a758b9-02ee-470d-ab44-21debc23c75d)

S1:

![S1 sh int trunk f01 f05](https://github.com/user-attachments/assets/5b3e1fe5-a2b7-4ef0-8b0f-d6f41d470478)

#### Часть 4. Настройте маршрутизацию.

- Шаг 1. Настройка маршрутизации между сетями VLAN на R1.

a.	Активируем интерфейс G0/0/1 на маршрутизаторе.

![R1 int g001](https://github.com/user-attachments/assets/3a331046-d211-4fdf-ac22-537de7155b35)

b.	Настраиваем подинтерфейсы для каждой VLAN, как указано в таблице IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q. 
Убеждаемся, что подинтерфейс для собственной VLAN не имеет назначенного IP-адреса. Включаем описание для каждого подинтерфейса.

![R1 sub if](https://github.com/user-attachments/assets/83dafb87-327f-4c41-8655-2719d4abf78f)

c.	Настраиваем интерфейс Loopback 1 на R1 с адресацией из приведенной выше таблицы.

![R1 Loopback1](https://github.com/user-attachments/assets/29f60103-f754-4383-a300-dde9546cb938)

d.	С помощью команды ***show ip interface brief*** проверьте конфигурацию подинтерфейса.

![R1 sh ip int br](https://github.com/user-attachments/assets/9bf03e5f-3ef3-4f26-a352-aefb52e83421)
  
- Шаг 2. Настройка интерфейса R2 g0/0/1 с использованием адреса из таблицы и маршрута по умолчанию с адресом следующего перехода 10.20.0.1

![R2 int g001](https://github.com/user-attachments/assets/7dd7a61f-49d9-423f-b212-4a5936098418)

#### Часть 5. Настройте удаленный доступ.

- Шаг 1. Настройте все сетевые устройства для базовой поддержки SSH.

a.	Создаем локального пользователя с именем пользователя SSHadmin и зашифрованным паролем $cisco123!

b.	Используем ccna-lab.com в качестве доменного имени.

c.	Генерируем криптоключи с помощью 1024 битного модуля.

d.	Настраиваем первые пять линий VTY на каждом устройстве, чтобы поддерживать только SSH-соединения и с локальной аутентификацией.

R1:

![R1 ssh](https://github.com/user-attachments/assets/480c5538-8dca-48b1-8060-b0a191de8f05)

R2:

![R2 ssh](https://github.com/user-attachments/assets/21c0c028-e560-47fd-94a2-1d3610ad7715)

S1:

![S1 ssh](https://github.com/user-attachments/assets/f3d83d28-a3bf-4ca2-a679-b921cd597d99)

S2:

![S2 ssh](https://github.com/user-attachments/assets/65880cd2-9143-40fb-a850-499a0c1eb4a2)

- Шаг 2. Включите защищенные веб-службы с проверкой подлинности на R1.

a.	Включаем сервер HTTPS на R1.
R1(config)# ip http secure-server

b.	Настраиваем R1 для проверки подлинности пользователей, пытающихся подключиться к веб-серверу.
R1(config)# ip http authentication local

**В CPT данные команды не работают**


#### Часть 6. Проверка подключения.

- Шаг 1. Настройте узлы ПК.

PC-A:

![PCA ip](https://github.com/user-attachments/assets/b8467647-61bb-4d57-8fd3-fd3167bf474b)

PC-B:

![PCB ip](https://github.com/user-attachments/assets/8dc793ae-b1a8-46a0-b90a-562594577c7f)


- Шаг 2. Выполните следующие тесты. Эхозапрос должен пройти успешно.

![Таблица тестов](https://github.com/user-attachments/assets/8fa7a228-807d-4fd4-8499-5f295004c909)

ping PC-A to PC-B, R1:

![ping PCA to PCB R1](https://github.com/user-attachments/assets/3c9471cf-95de-471c-bb39-c21e7d35acbb)

ping PC-B to PC-A, R1:

![ping PCB to PCA R1](https://github.com/user-attachments/assets/dacbbcc8-c4c2-4439-90e9-02183ffb788a)

SSH PC-A to R1,R2,S1,S2:

![SSH PCA to R1](https://github.com/user-attachments/assets/f0bed4cf-4d2e-40cf-b190-b4553645e5e0)

![SSH PCA to R1 to R2 to S1 to S2](https://github.com/user-attachments/assets/32223564-2dd6-4e22-9cdd-6054a64f5f66)

SSH PC-B to R1

![SSH PCB to R1](https://github.com/user-attachments/assets/f3b3b81e-9de4-4f6b-8fbb-1d2fac5c15ec)

![SSH PCB to R1 to R1 loop](https://github.com/user-attachments/assets/4550cc31-5180-409b-a6db-e18b3892cde6)

#### Часть 7. Настройка и проверка списков контроля доступа (ACL).

- Шаг 1. Проанализируйте требования к сети и политике безопасности для планирования реализации ACL.

При проверке базового подключения компания требует реализации следующих политик безопасности:

Политика1. Сеть Sales не может использовать SSH в сети Management (но в  другие сети SSH разрешен). 

Политика 2. Сеть Sales не имеет доступа к IP-адресам в сети Management с помощью любого веб-протокола (HTTP/HTTPS). 
Сеть Sales также не имеет доступа к интерфейсам R1 с помощью любого веб-протокола. 
Разрешён весь другой веб-трафик (обратите внимание — Сеть Sales  может получить доступ к интерфейсу Loopback 1 на R1).

Политика3. Сеть Sales не может отправлять эхо-запросы ICMP в сети Operations или Management. Разрешены эхо-запросы ICMP к другим адресатам. 

Политика 4: Cеть Operations  не может отправлять ICMP эхозапросы в сеть Sales. Разрешены эхо-запросы ICMP к другим адресатам. 

- Шаг 2. Разработка и применение расширенных списков доступа, которые будут соответствовать требованиям политики безопасности.

- Политика1. Сеть Sales не может использовать SSH в сети Management (но в  другие сети SSH разрешен).

![ACL R1 SSH](https://github.com/user-attachments/assets/0472149e-c0f0-45c0-a0e7-dd93aeb1c5cf)

![ACL PC-A SSH](https://github.com/user-attachments/assets/1570929f-ac30-482a-885a-84b5a7b4b276)

![ACL PC-B SSH](https://github.com/user-attachments/assets/1312a12e-3872-44f5-91c2-92b2666b0bbd)

- Политика 2. Сеть Sales не имеет доступа к IP-адресам в сети Management с помощью любого веб-протокола (HTTP/HTTPS). 
Сеть Sales также не имеет доступа к интерфейсам R1 с помощью любого веб-протокола. 
Разрешён весь другой веб-трафик (обратите внимание — Сеть Sales  может получить доступ к интерфейсу Loopback 1 на R1).

Дополнил схему подключением к g0/0/0 R1 сервера Server0:

![Net 11 with server](https://github.com/user-attachments/assets/c33aa9df-ec10-46b3-bd52-666d64cf6b5f)

![Server 0 conf](https://github.com/user-attachments/assets/af0b2bab-5cf8-4ee5-92dc-19cbc6d5c55e)

Настроил ACL для доступа к Server0:

![ACL R1 HTTPS last](https://github.com/user-attachments/assets/fc5db8a4-79ad-4d34-b519-0a951285ae15)

PC-A:

![ACL PC-A http ](https://github.com/user-attachments/assets/30b3c714-882a-40bf-b3e2-83f305bef6c7)

![ACL PC-A https ](https://github.com/user-attachments/assets/3e83a302-fc7a-43d0-a0ef-b3fbbae1a5c2)

PC-B:

![ACL PC-B http to serv0 ](https://github.com/user-attachments/assets/3b2cfb68-48df-4adb-8661-5ca6330fee57)

![ACL PC-B https to serv0 ](https://github.com/user-attachments/assets/0598fac9-2470-4352-8cb6-b8ca47911ec0)

- Политика3. Сеть Sales не может отправлять эхо-запросы ICMP в сети Operations или Management. Разрешены эхо-запросы ICMP к другим адресатам.

![ACL R1 ping to Oper   Manage](https://github.com/user-attachments/assets/25514751-6b34-4ae0-9b1c-88dbb5946820)

![ACL PC-B ping ](https://github.com/user-attachments/assets/9f27e3c8-ef4b-4d11-a593-434b3e68900c)

- Политика 4: Cеть Operations  не может отправлять ICMP эхозапросы в сеть Sales. Разрешены эхо-запросы ICMP к другим адресатам.

![ACL R1 ping to Sales](https://github.com/user-attachments/assets/84a89e1b-38bd-46e7-9f30-add195505a68)

![ACL PC-A ping ](https://github.com/user-attachments/assets/65ab99a3-64bf-46d8-8a3a-87f0cb34c8fb)

- Шаг 3. Убедитесь, что политики безопасности применяются развернутыми списками доступа.

![test final](https://github.com/user-attachments/assets/ba8fa453-4358-4cc0-bc85-855bcc289e39)




