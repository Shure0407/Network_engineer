## Лабораторная работа - Настройка NAT для IPv4

### Топология.

![Topology](https://github.com/user-attachments/assets/9237c3c6-b727-434d-b4b9-897356edf5c1)

### Таблица адресации.

![Address table](https://github.com/user-attachments/assets/8ccdc5ec-95f1-48e0-9f12-a748f95ccab2)

## Задачи.

Часть 1. Создание сети и настройка основных параметров устройства.

Часть 2. Настройка и проверка NAT для IPv4.

Часть 3. Настройка и проверка PAT для IPv4.

Часть 4. Настройка и проверка статического NAT для IPv4.

### Выполнение задания.

### Часть 1. Создание сети и настройка основных параметров устройства.

- Шаг 1. Подключите кабели сети согласно приведенной топологии.

![Net12](https://github.com/user-attachments/assets/b7177ccd-0d5e-4649-9bc9-93f341314252)

- Шаг 2. Произведим базовую настройку маршрутизаторов.

R1:

![R1](https://github.com/user-attachments/assets/d611e41e-086f-4df3-bfc4-a336331da629)

R2:

![R2 1](https://github.com/user-attachments/assets/ed012dec-572f-431d-9ef3-86258914a30f)
![R2 2](https://github.com/user-attachments/assets/8f234fce-8687-4a0e-9e58-b2c9d8a678e6)

- Шаг 3. Настраиваем базовые параметры каждого коммутатора.

S1:

![S1 1](https://github.com/user-attachments/assets/72c3c00b-44b9-4860-8d01-863ac36af56b)
![S1 2](https://github.com/user-attachments/assets/f9e61363-80f5-4556-80ee-0359747544dc)

S2:

![S2 1](https://github.com/user-attachments/assets/e983008b-a8a8-429f-b173-647dc9944e47)
![S2 2](https://github.com/user-attachments/assets/e26a6f06-2584-41e1-b757-f919b7371a05)


### Часть 2. Настройка и проверка NAT для IPv4.

- Шаг 1. Настройте NAT на R1, используя пул из трех адресов 209.165.200.226-209.165.200.228. 

a. Настройте простой список доступа, который определяет, какие хосты будут разрешены для трансляции. В этом случае все устройства в локальной сети R1 имеют право на трансляцию.
R1(config)# access-list 1 permit 192.168.1.0 0.0.0.255 
b. Создайте пул NAT и укажите ему имя и диапазон используемых адресов.
R1(config)# ip nat pool PUBLIC_ACCESS 209.165.200.226 209.165.200.228 netmask 255.255.255.248 
Примечание. Параметр маски сети не является разделителем IP-адресов. Это должна быть правильная маска подсети для назначенных адресов, даже если вы используете не все адреса подсети в пуле. 
c. Настройте перевод, связывая ACL и пул с процессом преобразования.
R1(config)# ip nat inside source list 1 pool PUBLIC_ACCESS 
Примечание: Три очень важных момента. Во-первых, слово «inside» имеет решающее значение для работы такого рода NAT. Если вы опустить его, NAT не будет работать. Во-вторых, номер списка — это номер ACL, настроенный на предыдущем шаге. В-третьих, имя пула чувствительно к регистру. 
d. Задайте внутренний (inside) интерфейс. 
R1(config)# interface g0/0/1
R1(config-if)# ip nat inside
e. Определите внешний (outside) интерфейс.
R1(config)# interface g0/0/0
R1(config-if)# ip nat outside

![R1 nat](https://github.com/user-attachments/assets/54292c42-9302-4f6b-a8f2-434e8966b97d)

- Шаг 2. Протестируйте и проверьте конфигурацию. 

a. С PC-B,  запустите эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. 
Если эхо-запрос не прошел, выполните процес поиска и устранения неполадок. 
На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.

![PC-B ip conf](https://github.com/user-attachments/assets/ecc5fc44-68c2-4039-a67c-a9af62029f4e)


b. С PC-A, запустите  эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. 
Если эхо-запрос не прошел, выполните отладку. 
На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.

![PC-A ip conf](https://github.com/user-attachments/assets/f2841bbc-1d23-4d9b-9c54-9e6a9555139d)


c. Обратите внимание, что предыдущая трансляция для PC-B все еще находится в таблице. Из S1, эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. 
Если эхо-запрос не прошел, выполните отладку. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.

![S1 ip def](https://github.com/user-attachments/assets/abf80bac-bd3f-4fd4-b8d3-d76b7622e818)

![S2 ip def](https://github.com/user-attachments/assets/bc05c065-50a6-4e25-b5f6-85a278845850)

d. Теперь запускаем пинг R2 Lo1 из S2. На этот раз перевод завершается неудачей, и вы получаете эти сообщения (или аналогичные) на консоли R1:
***Делал два теста (на самом деле их было больше) в первом случае запускал пинги с PC-B, S1, S2 - удачно и  после PC-A - перевод не удачен (выделено красным).
Во втором случае запускал пинги с PC-A, PC-B, S1 - удачно и  после S2 - перевод не удачен (выделено красным).***

PC-B:

![NAT PC-B ping to R2](https://github.com/user-attachments/assets/008b4b55-a96e-49c2-9491-9447b76ff710)

S1:

![NAT S1 ping to R2](https://github.com/user-attachments/assets/26f9165f-213f-4bf2-9033-0a92a21eaed2)

PC-A:

![NAT PC-A ping to R2](https://github.com/user-attachments/assets/34a74e9c-da67-4696-9094-9cb6aebec32e)

S2:

![NAT S2 ping to R2](https://github.com/user-attachments/assets/b578f059-7f7a-42c9-bbc3-ea9fc14bea7f)

e. Это ожидаемый результат, потому что выделено только 3 адреса, и мы попытались ping Lo1 с четырех устройств.
Напомним, что NAT — это трансляция «один-в-один». Как много выделено трансляций? 
Введите команду show ip nat translations verbose , и вы увидите, что ответ будет 24 часа.

Для первого случая:

![NAT R1 transl block PC-A](https://github.com/user-attachments/assets/f0884f19-de3c-4b9f-823f-a7be9c32eb25)

Для второго случая:

![NAT R1 transl block S2](https://github.com/user-attachments/assets/a60bd016-de36-4c6e-9d65-4a14b46ee056)

***При этом на консоли никакие предупреждающие надписи не выходили***

f. Учитывая, что пул ограничен тремя адресами, NAT для пула адресов недостаточно для нашего приложения.
Очистите преобразование NAT и статистику, и мы перейдем к PAT.

![NAT R1 clear](https://github.com/user-attachments/assets/02a29025-1fd2-4f2f-910b-e29b834df183)

### Часть 3. Настройка и проверка PAT для IPv4.

- Шаг 1-2 Удалите команду преобразования на R1.
Добавьте команду PAT на R1.

Теперь настройте преобразование PAT в пул адресов (помните, что ACL и Pool уже настроены, так что это единственная команда, которую нам нужно изменить с NAT на PAT).

![PAT R1](https://github.com/user-attachments/assets/042c32d8-18a5-4877-9cf7-b874ae61623f)

- Шаг 3. Протестируйте и проверьте конфигурацию.

a. Давайте проверим, что PAT работает. С PC-B,  запустите эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. 
Если эхо-запрос не прошел, выполните отладку. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.

![PAT PC-B ping to R2](https://github.com/user-attachments/assets/ecefb1c6-34e9-43f7-84a4-804901cb9acb)

![PAT R1 transl PC-B](https://github.com/user-attachments/assets/e16843a7-0d93-4086-ad7f-5ec6f1c51565)



b. С PC-A, запустите эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. 
Если эхо-запрос не прошел, выполните отладку. 
На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.

![PAT PC-A ping to R2](https://github.com/user-attachments/assets/1a4ec766-df8d-48dc-82e7-a095934a86dc)

![PAT R1 transl PC-A](https://github.com/user-attachments/assets/47d26d6e-b71a-43ff-8c0d-53b9f537ddef)

c. Генерирует трафик с нескольких устройств для наблюдения PAT. 
На PC-A и PC-B используйте параметр -t с командой ping, чтобы отправить безостановочный ping на интерфейс Lo1 R2 (ping -t 209.165.200.1), 
затем вернитесь к R1 и выполните команду show ip nat translations:

![PAT PC-A ping to R2](https://github.com/user-attachments/assets/43280dd3-67e6-48ea-935c-1373999ae074)

![PAT PC-B ping to R2](https://github.com/user-attachments/assets/f5228c8c-8743-44d0-b351-ae07244bfc8f)

![PAT R1 transl](https://github.com/user-attachments/assets/58792c87-e82b-4210-89bd-27a012829d80)

d. PAT в пул является очень эффективным решением для малых и средних организаций. 
Тем не менее есть неиспользуемые адреса IPv4, задействованные в этом сценарии. 
Мы перейдем к PAT с перегрузкой интерфейса, чтобы устранить эту трату IPv4 адресов. 
Остановите ping на PC-A и PC-B с помощью комбинации клавиш Control-C, затем очистите трансляции и статистику:

![PAT R1 clear](https://github.com/user-attachments/assets/1021b92e-bb0e-458f-8e01-9989e69f4ff1)

- Шаг 4-5. На R1 удалите команды преобразования nat pool.
Добавьте команду PAT overload, указав внешний интерфейс.

![PAT R1 no nat pool](https://github.com/user-attachments/assets/fcc62f76-f18f-40ff-8f92-c9da3619e07c)

- Шаг 6. Протестируйте и проверьте конфигурацию. 

a. Давайте проверим PAT, чтобы интерфейс работал. С PC-B,  запустите эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. 
Если эхо-запрос не прошел, выполните отладку. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.

![PAT R1 overload g000 ping PC-B](https://github.com/user-attachments/assets/59567f6e-bf4c-44b3-91dc-2da286cd4572)

![PAT R1 overload g000 transl PC-B](https://github.com/user-attachments/assets/f7218f31-2417-4a4b-817b-1fad8f12277e)

b. Сделайте трафик с нескольких устройств для наблюдения PAT. На PC-A и PC-B используйте параметр -t с командой ping для отправки безостановочного ping на интерфейс Lo1 R2 (ping -t 209.165.200.1).
На S1 и S2 выполните привилегированную команду exec ping 209.165.200.1 повторить 2000 ***Команда не работает***. Затем вернитесь к R1 и выполните команду show ip nat translations.

![PAT PC-A ping to R2](https://github.com/user-attachments/assets/b5b7fb8e-6e91-4489-a3db-2468e75b32c2)

![PAT PC-B ping to R2](https://github.com/user-attachments/assets/e663bca9-e221-4ffb-8e03-4eec824ea6c3)

![PAT R1 overload g000 transl](https://github.com/user-attachments/assets/fff6968b-4084-4ab0-bcfe-d78ffb7644a6)

Теперь все внутренние глобальные адреса сопоставляются с IP-адресом интерфейса g0/0/0.

### Часть 4. Настройка и проверка статического NAT для IPv4.

- Шаг 1. На R1 очистите текущие трансляции и статистику.

![PAT R1 clear 1](https://github.com/user-attachments/assets/1cd21bff-68f0-4e12-a957-944c8b80622f)

- Шаг 2-3. На R1 настройте команду NAT, необходимую для статического сопоставления внутреннего адреса с внешним адресом.
Протестируйте и проверьте конфигурацию.

a. Давайте проверим, что статический NAT работает. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations, и вы увидите статическое сопоставление.
R1# show ip nat translations

![Static NAT R1 ](https://github.com/user-attachments/assets/616c9091-72bb-48a0-b17f-845d9dcf2683)

b. Таблица перевода показывает, что статическое преобразование действует. 
Проверьте это, запустив ping  с R2 на 209.165.200.229. Плинги должны работать.

![Static NAT R2 ping to R1](https://github.com/user-attachments/assets/2715d505-0f5e-4519-98af-669b5f9d9ebe)

c. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations, и вы увидите статическое сопоставление и преобразование на уровне порта для входящих pings.

![Static NAT R1 transl](https://github.com/user-attachments/assets/ad93d5b8-1fb6-4877-a5fa-3ce1d81d4e5b)

Это подтверждает, что статический NAT работает.







