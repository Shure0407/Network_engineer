## Лабораторная работа №5. Доступ к сетевым устройствам по протоколу SSH.

### Топология.

![Топология](https://github.com/Shure0407/Network_engineer/assets/162669909/0f18e170-2491-46a1-ac97-c24ffc17f1b3)

### Таблица адресации.

![Таблица адресации](https://github.com/Shure0407/Network_engineer/assets/162669909/60cf8c08-4248-429f-aaec-cd36a46b253c)

### Задачи.
Часть 1. Настройка основных параметров устройства.

Часть 2. Настройка маршрутизатора для доступа по протоколу SSH.

Часть 3. Настройка коммутатора для доступа по протоколу SSH.

Часть 4. SSH через интерфейс командной строки (CLI) коммутатора.

### Выполнение задания.

#### Часть 1. Настройка основных параметров устройств.

- Шаг 1. Создаем сеть согласно топологии.

![Cheme](https://github.com/Shure0407/Network_engineer/assets/162669909/b6efc62f-4b1f-4d96-8fd3-c35c55ea2b63)

- Шаг 2. Выполняем инициализацию и перезагрузку маршрутизатора и коммутатора.

Выполняем перезагрузку маршрутизатора и коммутатора с помощью команды ***erase startup-config***

- Шаг 3. Настраиваем маршрутизатор.

Подключаемся через консольный порт и настроиваем основные параметры устройства:

a. Подключаемся к маршрутизатору с помощью консоли и активируем привилегированный режим EXEC.
                
b. Входим в режим конфигурации.
                
c. Отключаем поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
          
d. Назначаем class в качестве зашифрованного пароля привилегированного режима EXEC.
                
e. Назначаем cisco в качестве пароля консоли и включаем вход в систему по паролю.
                
f. Назначаем disco в качестве пароля VTY и включаем вход в систему по паролю.
                
g. Шифруем открытые пароли.
                
h. Создаем баннер, который предупреждает о запрете несанкционированного доступа.
                
i. Настраиваем и активируем на маршрутизаторе интерфейс G0/0/1, используя информацию, приведенную в таблице адресации.
                
j. Сохраняем текущую конфигурацию в файл загрузочной конфигурации.

![R1](https://github.com/Shure0407/Network_engineer/assets/162669909/227aacb7-67ae-432a-a05c-c8bf819a1096)

- Шаг 4. Настраиваем компьютер PC-A.

Настраиваем IP-адрес и маску подсети, шлюз по умолчанию.

![IPv4 PC-A](https://github.com/Shure0407/Network_engineer/assets/162669909/cc934d0c-a6b1-41fc-9e0b-2b7593e4d96b)
  
- Шаг 5. Проверяем подключение к сети.

![ping to R1](https://github.com/Shure0407/Network_engineer/assets/162669909/c085d9e1-f897-422d-a0e8-54d4a967e1f2)

#### Часть 2. Настройка маршрутизатора для доступа по протоколу SSH.

- Шаг 1. Настраиваем аутентификацию устройств.
Задаем домен для устройства.

![Domain R1](https://github.com/Shure0407/Network_engineer/assets/162669909/9460a570-ecbb-438d-9b53-c63a5777e8d8)

- Шаг 2. Создаем ключ шифрования с указанием его длины.

![crypto key R1](https://github.com/Shure0407/Network_engineer/assets/162669909/8eb07a2e-dd50-4c29-83fc-03b2735955de)

- Шаг 3. Создаем имя пользователя в локальной базе учетных записей.

![Login user pass R1](https://github.com/Shure0407/Network_engineer/assets/162669909/eb32d844-bf6a-4ab3-9e10-d36ce27cc693)

- Шаг 4. Активируем протокол SSH на линиях VTY.

Изменяем способ входа в систему, чтобы использовалась проверка пользователей по локальной базе учетных записей.
Активируем протоколы Telnet и SSH на входящих линиях VTY с помощью команды ***transport input***.

![vty R1](https://github.com/Shure0407/Network_engineer/assets/162669909/0792a63d-5957-456e-a7cc-e8681f16848a)

![sh vty R1](https://github.com/Shure0407/Network_engineer/assets/162669909/553e6955-7a00-4641-ab99-30c17e9a5e3a)

- Шаг 5. Сохраняем текущую конфигурацию в файл загрузочной конфигурации.

- Шаг 6. Установливаем соединение с маршрутизатором по протоколу SSH.

Устанавливаем SSH-подключение к R1.

![SSH to R1](https://github.com/Shure0407/Network_engineer/assets/162669909/246ba90e-01f5-489b-817c-72358ef7fc41)

![SSH to R1 pass](https://github.com/Shure0407/Network_engineer/assets/162669909/aee1a707-911e-4339-96e9-016cb7a76de7)

#### Часть 3. Настройка коммутатора для доступа по протоколу SSH.

- Шаг 1. Настраиваем основные параметры коммутатора.

Подключаемся через консольный порт и настроиваем основные параметры устройства:

a. Подключаемся к маршрутизатору с помощью консоли и активируем привилегированный режим EXEC.
                
b. Входим в режим конфигурации.
                
c. Отключаем поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
          
d. Назначаем class в качестве зашифрованного пароля привилегированного режима EXEC.
                
e. Назначаем cisco в качестве пароля консоли и включаем вход в систему по паролю.
                
f. Назначаем disco в качестве пароля VTY и включаем вход в систему по паролю.
                
g. Шифруем открытые пароли.
                
h. Создаем баннер, который предупреждает о запрете несанкционированного доступа.
                
i. Настраиваем и активируем на маршрутизаторе интерфейс VLAN 1, используя информацию, приведенную в таблице адресации.
                
j. Сохраняем текущую конфигурацию в файл загрузочной конфигурации.

![S1 1](https://github.com/Shure0407/Network_engineer/assets/162669909/57181135-05c1-4925-838b-b90db7174d69)

![S1 2](https://github.com/Shure0407/Network_engineer/assets/162669909/3e9a7222-266f-4fba-a5bd-e9fce56ed9b3)

- Шаг 2. Настраиваем коммутатор для соединения по протоколу SSH.

a. Настраиваем имя устройства, как указано в таблице адресации.

b. Задаем домен для устройства.

c. Создаем ключ шифрования с указанием его длины.

d. Создаем имя пользователя в локальной базе учетных записей.

e. Активируем протоколы Telnet и SSH на линиях VTY.

f. Изменяем способ входа в систему, чтобы использовалась проверка пользователей по локальной базе учетных записей.

![Domain crypto S1](https://github.com/Shure0407/Network_engineer/assets/162669909/6d933165-0596-4247-af47-732c150d8fe6)

- Шаг 3. Устанавливаем соединение с коммутатором по протоколу SSH.

![SSH to S1](https://github.com/Shure0407/Network_engineer/assets/162669909/cee6bf9e-f87d-47b2-9eca-531d84321791)

![SSH to S1 pass](https://github.com/Shure0407/Network_engineer/assets/162669909/e7b5fdc9-a42d-40b5-8fa5-194c195d0426)

#### Часть 4. Настройка протокола SSH с использованием интерфейса командной строки (CLI) коммутатора.

- Шаг 1. Смотрим доступные параметры для клиента SSH в Cisco IOS.

![SSH command](https://github.com/Shure0407/Network_engineer/assets/162669909/04fcc5a6-631a-4829-85b7-a838f78321f6)

- Шаг 2. Установим с коммутатора S1 соединение с маршрутизатором R1 по протоколу SSH.

Подключаемся к маршрутизатору R1 по протоколу SSH

![SSH S1 to R1](https://github.com/Shure0407/Network_engineer/assets/162669909/3ece858a-0f5d-478d-ad7e-beacbb9470aa)

Делаем переходы к S1 с помощью комбинации клавиш Ctrl+Shift+6. Отпустите клавиши Ctrl+Shift+6 и нажмите x.
И обратно к R1 нажимаем клавишу Enter в пустой строке интерфейса командной строки.

![переходы](https://github.com/Shure0407/Network_engineer/assets/162669909/32398a69-d269-4a78-ad0c-2e500c68420f)

Версии протокола SSH которые поддерживаются при использовании интерфейса командной строки

![SSH version](https://github.com/Shure0407/Network_engineer/assets/162669909/462ed3bf-2cc0-49db-883a-a170feafaa2e)

Как предоставить доступ к сетевому устройству нескольким пользователям, у каждого из которых есть собственное имя пользователz?

Доступ можно настроить командой ***username***, добавляя пользователей с различными логинами, предоставляя им различный доступ надстройкой 
***privilege*** , и устанавливая для каждого пароль ***secret***
