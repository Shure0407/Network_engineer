## Лабораторная работа №13. Настройка протоколов CDP, LLDP и NTP.

### Топология.

![Topology](https://github.com/user-attachments/assets/e25aeed0-1c24-4896-bb05-e315a633a905)

### Таблица адресации.

![Address table](https://github.com/user-attachments/assets/ec14edeb-78d2-413b-b1e0-aa3567532e4b)

### Задачи.

Часть 1. Создание сети и настройка основных параметров устройства.

Часть 2. Обнаружение сетевых ресурсов с помощью протокола CDP.

Часть 3. Обнаружение сетевых ресурсов с помощью протокола LLDP.

Часть 4. Настройка и проверка NTP.

### Выполнение задания.

### Часть 1. Создание сети и настройка основных параметров устройства.

- Шаг 1. Создайте сеть согласно топологии.

![Net 13](https://github.com/user-attachments/assets/84b844fa-a2b0-4082-a5f4-b7890342a2d9)

- Шаг 2. Настройте базовые параметры для маршрутизатора.

![R1](https://github.com/user-attachments/assets/294407ac-e23e-49b1-8e69-76ee8a66c0ed)

- Шаг 3. Настройте базовые параметры каждого коммутатора.

S1:

![S1 1](https://github.com/user-attachments/assets/ff634034-4cd7-4544-91fd-b0899af53c6d)

![S1 2](https://github.com/user-attachments/assets/a08c531a-91c0-41f7-ba60-1cd7c773b205)

S2:

![S2 1](https://github.com/user-attachments/assets/4e6f8153-62e2-4b81-ab83-700e44c86d52)

![S2 2](https://github.com/user-attachments/assets/06d43231-1ec5-48d2-a2cc-fe4736445324)

![S2 3](https://github.com/user-attachments/assets/f9eefb20-285c-4c79-98fa-2dc170e2e349)

### Часть 2. Обнаружение сетевых ресурсов с помощью протокола CDP.

На устройствах Cisco протокол CDP включен по умолчанию. Воспользуйтесь CDP, чтобы обнаружить порты, к которым подключены кабели.
Откройте окно конфигурации

a. На R1 используйте соответствующую команду show cdp, чтобы определить, сколько интерфейсов включено CDP, сколько из них включено и сколько отключено.

 ![R1 CDP int](https://github.com/user-attachments/assets/b927982a-259d-4811-a7b0-292f629d9b90)

***Вопрос:
Сколько интерфейсов участвует в объявлениях CDP? Какие из них активны?***

***Ответ: 
Задействовано 4 интерфейса G0/0/0-G0/0/2, Vlan1. Активный G0/0/1.***
 
b. На R1 используйте соответствующую команду show cdp, чтобы определить версию IOS, используемую на S1.

![R1 CDP entry S1](https://github.com/user-attachments/assets/119badaf-c4fd-4a95-87d1-bf04e77619c8)

***Вопрос:
Какая версия IOS используется на  S1?***

***Ответ:
Используется Версия 15.0(2)SE4***

c. На S1 используйте соответствующую команду show cdp, чтобы определить, сколько пакетов CDP было выданных.

![S1 CDP sh](https://github.com/user-attachments/assets/829860aa-0eb1-4cf8-ad82-4171cb590486)

d. Настройте SVI для VLAN 1 на S1 и S2, используя IP-адреса, указанные в таблице адресации выше. Настройте шлюз по умолчанию для каждого коммутатора на основе таблицы адресов.

e. На R1 выполните команду show cdp entry S1 . 

![R1 CDP entry S1 ip](https://github.com/user-attachments/assets/6208bb73-6a7d-4e52-bbd2-42bc94786b95)

***Вопрос:
Какие дополнительные сведения доступны теперь?***

***Ответ:
Теперь доступен ip адрес Vlan1***

f. Отключить CDP глобально на всех устройствах. 

R1:

![R1 no cdp run](https://github.com/user-attachments/assets/5a35bcec-b823-4f55-a232-e94499e9ef7f)

S1:

![S1 no cdp run](https://github.com/user-attachments/assets/7cab3a57-27f5-4eae-80e0-1b4c1adf660d)

S2:

![S2 no cdp run](https://github.com/user-attachments/assets/23756d61-272c-4cfd-8b27-690f832c964f)

### Часть 3. Обнаружение сетевых ресурсов с помощью протокола LLDP.

На устройствах Cisco протокол LLDP может быть включен по умолчанию. Воспользуйтесь LLDP, чтобы обнаружить порты, к которым подключены кабели.

a. Введите соответствующую команду lldp, чтобы включить LLDP на всех устройствах в топологии.

R1:

![R1 LLDP run](https://github.com/user-attachments/assets/442f1979-8ca4-477b-aaf3-2633a60876c6)

S1:

![S1 LLDP run](https://github.com/user-attachments/assets/58a0efac-49d1-46fc-bb8d-d72245184158)

S2:

![S2 LLDP run](https://github.com/user-attachments/assets/3be4cf09-8f13-4fdf-824b-897e153f52f3)

b. На S1 выполните соответствующую команду lldp, чтобы предоставить подробную информацию о S2. 

Можно только посмотреть через команду ***show lldp neibours detail***

R1:

![R1 sh LLDP nei det](https://github.com/user-attachments/assets/f4ba58f1-6ba0-46d5-b754-a1d21d56bb9d)

S1:

![S1 sh LLDP nei det](https://github.com/user-attachments/assets/4f5834f2-0c58-4ccf-a3dc-11554a422c9e)

S2:

![S2 sh LLDP nei det](https://github.com/user-attachments/assets/a77e06ba-2ca6-40f9-8c1c-0d504bb1a05e)

***Вопрос
Что такое chassis ID  для коммутатора?***

***Ответ:
Это МАС адрес порта, например, 00d0.5878.9701 MAC адрес порта Fa0/1 на S2***

### Часть 4. Настройка NTP.

В части 4 необходимо настроить маршрутизатор R1 в качестве сервера NTP, а маршрутизатор R2 в качестве клиента NTP маршрутизатора R1. 
Необходимо выполнить синхронизацию времени для Syslog и отладочных функций. 
Если время не синхронизировано, сложно определить, какое сетевое событие стало причиной данного сообщения.

- Шаг 1. Выведите на экран текущее время.

Введите команду ***show clock*** для отображения текущего времени на R1. 

![R1 sh clock before](https://github.com/user-attachments/assets/64153d2f-7e1b-4a7d-bc18-88fbb4ac87be)

- Шаг 2. Установите время.

С помощью команды ***clock set*** установите время на маршрутизаторе R1. Введенное время должно быть в формате UTC. 

![R1 set clock](https://github.com/user-attachments/assets/b626d7dc-7076-4782-9f0b-ca7ce1da7f68)

- Шаг 3. Настройте главный сервер NTP.

Настройте R1 в качестве хозяина NTP с уровнем слоя 4.

![R1 NTP server](https://github.com/user-attachments/assets/e3c471f3-2d6f-404a-8e10-3c13fb9a411c)

![R1 sh NTP server](https://github.com/user-attachments/assets/be64c2b6-38b2-4909-bf93-3f646b431806)

- Шаг 4-5. Настройте клиент NTP. Проверьте настройку NTP.

a. Выполните соответствующую команду на S1 и S2, чтобы просмотреть настроенное время.

Время первоначальной загрузки на коммутаторах 

![Clock default](https://github.com/user-attachments/assets/7ed26772-ba8b-419a-b307-03a6822af9cd)

b. Настройте S1 и S2 в качестве клиентов NTP. Используйте соответствующие команды NTP для получения времени от интерфейса G0/0/1 R1, 
а также для периодического обновления календаря или аппаратных часов коммутатора.
Используйте соответствующую команду ***show*** , чтобы убедиться, что S1 и S2 синхронизированы с R1.

S1:

![S1 NTP synhr](https://github.com/user-attachments/assets/5363d882-80b9-408a-b8c4-c68f7155ad0b)

S2:

![S2 NTP synhr](https://github.com/user-attachments/assets/d1ac31a8-0620-43aa-8589-31da77331a5f)

c. Выполните соответствующую команду на S1 и S2, чтобы просмотреть настроенное время и сравнить ранее записанное время.

S1:

![S1 NTP sh clock](https://github.com/user-attachments/assets/ff8a0ba2-347c-48d9-b574-968b921482a5)

S2:

![S2 NTP sh clock](https://github.com/user-attachments/assets/13507c1e-8d56-4ab8-92ba-d812369b0fe6)
