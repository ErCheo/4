
### Esatimates (Примерные показатели)

Регион: Сахалинская область  
Численность региона: 500К человек  
DAU: 15% от 500К = 75К  
RPS: 75K / 24 / 3600 ~= 1  


### Функциональные требования

#### User Story
1. Как клиент автомойки, я хочу выбрать тип мойки автомобиля (ручная, автоматическая, экспресс), чтобы обслуживать свою машину в соответствии с предпочтениями и временем.
2. Как клиент автомойки, я хочу записаться на мойку через мобильное приложение или сайт, чтобы выбрать удобное время и избежать очереди.
3. Как клиент автомойки, я хочу получить уведомление о готовности автомобиля после мойки, чтобы точно знать, когда можно забрать машину.
4. Как клиент автомойки, я хочу иметь возможность оплатить услуги онлайн через приложение или сайт, чтобы избежать очередей и не тратить время на оплату на месте.
5. Как клиент автомойки, я хочу получать скидки или бонусы за постоянное использование услуг, чтобы экономить на дальнейших визитах.
6. Как клиент автомойки, я хочу видеть отзывы других клиентов о качестве работы, чтобы быть уверенным в высоком уровне обслуживания.
7. Как клиент автомойки, я хочу, чтобы мой автомобиль был помыт в течение оговоренного времени, чтобы не тратить лишнее время.
8. Как клиент автомойки, я хочу видеть фотографии или видео процесса мойки и ухода за моим автомобилем, чтобы убедиться в высоком качестве услуг и уровне обслуживания.
9. Как клиент автомойки, я хочу, чтобы персонал автомойки предложил рекомендации по уходу за кузовом или салоном машины, чтобы поддерживать её в хорошем состоянии.
10. Как клиент автомойки, я хочу, чтобы на автомойке была зона отдыха с кофе или напитками, чтобы я мог комфортно подождать, пока мой автомобиль моется.

#### Use Cases  
![Картинка](https://github.com/user-attachments/assets/1584a754-ac12-405b-9388-c4564a8c7f25)

```
left to right direction
actor "Клиент" as client
actor "Платёжная штука" as plata
rectangle ВсеМойки.ру {
usecase "Управление своим профилем" as UC1
usecase "Управлять своим авто" as UC2
usecase "Выбрать город" as UC3
usecase "Выбрать мойку" as UC4
usecase "Дата время" as UC5
usecase "Способ оплаты" as UC6
usecase "Оплатить" as UC7
usecase "Отменить запись" as UC8
}

client --> UC1
client --> UC2
client --> UC3
client --> UC4
client --> UC5
client --> UC6
client --> UC7
client --> UC8
UC7 --> plata

@enduml
```

### Сценарии использования:  
- UC_01: Найти и выбрать автомойку
  - Участники:
    - Пользователь приложения
  - Предусловия:
    - Пользователь зарегестрирован и авторизован
  - Условие для запуска сценария:
    - Пользователь нажимает кнопку "Найти мойку" 
  - Признак успешности:
    - Пользователь выбрал автомойку 

#### Базовый сценарий

1. Система проверяет, что клиент передал свою геолокацию
   ЕСЛИ: Геолокации нет,
   ТО: Система переходит в "Базовый сценарий 3"
3. Система ищет ближайшие к позиции клиента мойки | АЛ_01: Алгоритм поиска моек по адресу или геолокации
4. Система формирует список моек
5. Система отображает экран с картой и списком моек | UI_01
6. Система ожидает выбора мойки клиентом
7. Система переходит к экрану выбора услуг
8. Сценарий завершен

UI_01: Экран с картой и списком моек

#### Базовый сценарий 2

1. Система выводит сообщение клиента с просьбой разрешить передачу геолокации
2. ЕСЛИ: клиент разрешил передачу геолокации   
   ТО: Система переходит в "Базовый сценарий шаг 2"   
   ИНАЧЕ: Перейти в "Базовый сценарий 3"

#### Базовый сценарий 3

1. Система отображает поле для ввода адреса
2. Система ожидает от клиента ввод адреса
3. Система переходит в "Базовый сценарий шаг 2" 

АЛ_01: Алгоритм поиска моек по адресу или геолокации
1. Система формирует запрос к БД
2. ...
3. ...
4. Возвращает список моек

### Альтернативный сценарий 
АС_1: Некорректный запрос пользователя

### Нефункциональные требования



### ER-диаграмма

#### Сущности и их атрибуты:

- Клиент (Customer)
  - ID клиента (Customer_ID)
  - Имя (Name)
  - Контактный номер (Phone)
  - Электронная почта (Email)
  - Адрес (Address)

- Автомобиль (Car)
  - ID автомобиля (Car_ID)
  - Марка (Make)
  - Модель (Model)
  - Год выпуска (Year)
  - Номерной знак (License_Plate)
  - Тип (Car_Type) - легковой, внедорожник и т. д.
  - Клиент_ID (Customer_ID) — связь с клиентом

- Услуга (Service)
  - ID услуги (Service_ID)
  - Название (Service_Name) - мойка, полировка, химчистка и т. д.
  - Описание (Description)
  - Цена (Price)

- Запись на мойку (SingUpForACarWash)
  - ID записи (SingUpForACarWash_ID)
  - Дата записи (Date)
  - Статус записи (Status) - подтверждена, завершена, отменена и т. д.
  - Клиент_ID (Customer_ID) — связь с клиентом
  - Автомобиль_ID (Car_ID) — связь с автомобилем

- Работник (Employee)
  - ID работника (Employee_ID)
  - Имя (Name)
  - Должность (Position)
  - Телефон (Phone)
  - Электронная почта (Email)

- Мойка (Wash)
  - ID мойки (Wash_ID)
  - Тип мойки (Wash_Type) - автоматическая, ручная, экспресс и т. д.
  - Статус мойки (Wash_Status) - в процессе, завершена, отменена
  - Время начала (Start_Time)
  - Время окончания (End_Time)
  - Работник_ID (Employee_ID) — связь с работником
  - Услуга_ID (Service_ID) — связь с услугой
  - Запись_ID (SingUpForACarWash_ID) — связь с записью

#### Связи:
- Клиент - Автомобиль: Один клиент может иметь несколько автомобилей. (1:M)
- Автомобиль - Запись на мойку: Один автомобиль может быть связан с несколькими записями на мойку. (1:M)
- Клиент - Запись на мойку: Один клиент может записать несколько автомобилей на мойку. (1:M)
- Услуга - Мойка: Одна услуга может быть использована в нескольких мойках. (1:M)
- Работник - Мойка: Один работник может обслуживать несколько мойок. (1:M)
- Запись на мойку - Мойка: Каждая запись на мойку связана с конкретной мойкой. (1:1)

#### ER-диаграмма

![bLJHIXj15Fs2-OV1bpuKVw1F5glWSv4-XaNNTY79okvQaAPWiWyY1fHMQ94ejOBFgoPraut9BzpvevwPsJ6Pp8huiCFElNVkFUVClRCI9rwKx3NgZBtXT4bJSK03wkChy3rIJWCksY8LHzXCyDU1USZyPX8a-to9pX6NoqZHMU9Up5VtuYHi-17_nZX_QtQrZG_y7G-QYJJIRngB4-pZ90gQdvNfd2Oo1MKqmleeZcbOamLf](https://github.com/user-attachments/assets/440e5d41-d43a-42e5-a264-efdeeedfc486)

```
@startuml

' Определение сущностей
entity "Клиент" as Customer {
  +Customer_ID : int
  +Имя : string
  +Контактный_номер : string
  +Адрес : string
  +Email : string
}

entity "Автомобиль" as Car {
  +Car_ID : int
  +Марка : string
  +Модель : string
  +Год_выпуска : int
  +Номерной_знак : string
  +Тип : string
  +Customer_ID : int
}

entity "Запись на мойку" as SingUpForACarWash {
  +SingUpForACarWash_ID : int
  +Дата_записи : date
  +Статус : string
  +Customer_ID : int
  +Car_ID : int
}

entity "Услуга" as Service {
  +Service_ID : int
  +Название : string
  +Описание : string
  +Цена : float
}

entity "Мойка" as Wash {
  +Wash_ID : int
  +Тип : string
  +Статус : string
  +Время_начала : date
  +Время_окончания : date
  +Employee_ID : int
  +Service_ID : int
  + SingUpForACarWash_ID : int
}

entity "Работник" as Employee {
  +Employee_ID : int
  +Имя : string
  +Должность : string
  +Контактный_номер : string
  +Email : string
}

' Связи между сущностями
Customer ||--o| Car 
Car ||--o| SingUpForACarWash 
Customer ||--o| SingUpForACarWash
Service ||--o| Wash 
Employee||--o| Wash
SingUpForACarWash ||--|| Wash 

@enduml
```



























