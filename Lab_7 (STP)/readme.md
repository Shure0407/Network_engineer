## Лабораторная работа №7. Развертывание коммутируемой сети с резервными каналами.

### Топология.

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/ae5d5177-1acd-47cd-9673-0e4714ff476f)

### Таблица адресации.

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/28eed0e3-a202-471c-a664-33eef953e32e)

### Цели.

Часть 1. Создание сети и настройка основных параметров устройства.

Часть 2. Выбор корневого моста.

Часть 3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов.

Часть 4. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов.

### Выполнение задания.

#### Часть 1. Создание сети и настройка основных параметров устройства.

- Шаг 1. Создаем сеть согласно топологии.

![Сеть](https://github.com/Shure0407/Network_engineer/assets/162669909/2560a9b3-1989-429d-b6f1-035fc9ef277c)

- Шаг 2. Выполняем инициализацию и перезагрузку коммутаторов.

- Шаг 3. Настраиваем базовые параметры каждого коммутатора.

S1:

![S1](https://github.com/Shure0407/Network_engineer/assets/162669909/ca5568bc-965d-44c2-8e3a-e7981da39e1c)

S2:

![S2](https://github.com/Shure0407/Network_engineer/assets/162669909/a29fe79c-4482-4cf6-836f-8a4066803bde)

S3:

![S3](https://github.com/Shure0407/Network_engineer/assets/162669909/02ac0f0f-2a9a-48b4-972d-b8af8ffc009b)

- Шаг 4. Проверяем связь.

Успешно ли выполняется эхо-запрос от коммутатора S1 на коммутатор S2?

![ping S1 to S2](https://github.com/Shure0407/Network_engineer/assets/162669909/e856ce06-b357-4ace-9e75-f96aea0eaac8)

Успешно ли выполняется эхо-запрос от коммутатора S1 на коммутатор S3?

![ping S1 to S3](https://github.com/Shure0407/Network_engineer/assets/162669909/6623b0da-2484-4cb7-8fdc-f40d33bb2b42)

Успешно ли выполняется эхо-запрос от коммутатора S2 на коммутатор S3?

![ping S2 to S3](https://github.com/Shure0407/Network_engineer/assets/162669909/b9116532-21a5-463a-8096-1c919c20d431)


#### Часть 2. Определение корневого моста

- Шаг 1. Отключаем все порты на коммутаторах.

![off fa0-4 S1](https://github.com/Shure0407/Network_engineer/assets/162669909/9e634a53-224d-4daf-bba2-a0e1d39cc01f)

![off fa0-4 S2](https://github.com/Shure0407/Network_engineer/assets/162669909/93dc5e9e-18ed-4f6e-b9ad-2457e8dc1275)

![off fa0-4 S3](https://github.com/Shure0407/Network_engineer/assets/162669909/ecebb1f1-b80f-4271-a69b-c7373f8bde2a)

- Шаг 2. Настройте подключенные порты в качестве транковых.

![trunk S1](https://github.com/Shure0407/Network_engineer/assets/162669909/c098ce60-bd87-409d-bb1b-14202c9b88e3)

![trunk S2](https://github.com/Shure0407/Network_engineer/assets/162669909/77ab1756-2431-4f9c-b121-33f174b82f00)

![trunk S3](https://github.com/Shure0407/Network_engineer/assets/162669909/3508d173-a94b-454c-8c9c-c61794e45b17)

- Шаг 3. Включаем порты F0/2 и F0/4 на всех коммутаторах.

![on fa2 4 S1](https://github.com/Shure0407/Network_engineer/assets/162669909/e9844865-f764-422f-8a68-19925a57fa0d)

![on fa2 4 S2](https://github.com/Shure0407/Network_engineer/assets/162669909/e47f870e-9997-47ee-b493-f6bb5c664257)

![on fa2 4 S3](https://github.com/Shure0407/Network_engineer/assets/162669909/4b342948-e2b5-4b34-a5a0-151eefe59b2a)

- Шаг 4. Отображаем данные протокола spanning-tree на всех коммутаторах.

  Стоимость портов одинаковая, поэтому сравнение по идентификатору моста (BID).

![sh span tree S1](https://github.com/Shure0407/Network_engineer/assets/162669909/547b47fc-c80e-4506-ac03-2fd762204caa)

![sh span tree S2](https://github.com/Shure0407/Network_engineer/assets/162669909/12172261-219d-47a9-a01e-c45b76beb384)

![sh span tree S3](https://github.com/Shure0407/Network_engineer/assets/162669909/ecd88739-6863-43c9-af20-93ca005f0e6c)

- Какой коммутатор является корневым мостом?  Почему этот коммутатор был выбран протоколом spanning-tree в качестве корневого моста? 

S2 является корневым мостом. S2 имеет наименьший BID (32769.000143555D17) по сравнению с S1(32769.0030A3382D15) и S3(32769.0060705D756C).

- Какие порты на коммутаторе являются корневыми портами?

S1 F0/2 и S3 F0/2 являются корневыми, потому что смотрят в сторону корневого моста.

- Какие порты на коммутаторе являются назначенными портами?

S2 F0/2, S2 F0/4 являются назначенными, потому что находятся на корневом мосте, и S1 F0/4 тоже является назначенным.

- Какой порт отображается в качестве альтернативного и в настоящее время заблокирован?

S3 F0/4 является альтернативным и заблокирован.

- Почему протокол spanning-tree выбрал этот порт в качестве невыделенного (заблокированного) порта?

Протокол spanning-tree выбрал S3 F0/4 в качестве заблокированного, потому что при сравнении BID на S1 и S3, на последнем он больше
и поэтому на S1 порт F0/4 - назначенный, а на S3 F0/4 - альтернативный (заблокированный).

![Сеть часть 2](https://github.com/Shure0407/Network_engineer/assets/162669909/4885dd0f-f753-40fe-a194-0e460828f3d9)

#### Часть 3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов.

- Шаг 1. Определите коммутатор с заблокированным портом.

  

- Шаг 2. Измените стоимость порта.

![f0 2 S3 cost 18](https://github.com/Shure0407/Network_engineer/assets/162669909/f9dbfdc4-6f36-4ad9-980d-2818d259ac7a)

- Шаг 3. Проверяем изменения протокола spanning-tree.

![sh span tree S1 cost 18](https://github.com/Shure0407/Network_engineer/assets/162669909/41acfafe-c7fa-4358-ac00-ad4b4280b7a4)

![sh span tree S3 cost 18](https://github.com/Shure0407/Network_engineer/assets/162669909/fca29985-ba82-4b20-afc7-227b7fe2e2ba)

![Сеть часть 3 cost 18](https://github.com/Shure0407/Network_engineer/assets/162669909/a96ab8df-0500-451a-9596-8f49b566d592)

- Почему протокол spanning-tree заменяет ранее заблокированный порт на назначенный порт и блокирует порт, который был назначенным портом на другом коммутаторе?

Протокол заменил на S3 заблокированный порт на назначенный потому что изменилась стоимость порта с 19 на 18 и соответственно обменявшись информацией S1 и S3 положение последнего "улучшилось". На S1 назначенный порт заменился на альтернативный (заблокированный).

- Шаг 4. Удаляем изменения стоимости порта.

![f0 2 S3  no cost 18](https://github.com/Shure0407/Network_engineer/assets/162669909/7d937e31-fbd2-4487-97c9-e405bdb5aa38)

![sh span tree S1 cost 19](https://github.com/Shure0407/Network_engineer/assets/162669909/7e0c83cc-cea6-408d-90cf-cc4e64c902ff)

![sh span tree S3 cost 19](https://github.com/Shure0407/Network_engineer/assets/162669909/3b7d8459-dd51-4400-80d9-76618926f238)

![Сеть часть 3 cost 19](https://github.com/Shure0407/Network_engineer/assets/162669909/56d9dcc2-0046-44f0-bdca-be8280692b4a)







