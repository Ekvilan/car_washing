# code для схемы автомойки
        https://plantuml.com/ru/

   ## Esatimates aпримерные показатели
        1) Регион Сахалинская обл.
        2) кол-во людей пользуется в день(Численость региона: 500k)
             DAU: 15% от 500k = 75k
        3) RPS 75k/24/3600 ~= 1
        
# 1) user story
<table>
  <thead>
    <tr>
      <th>Область фокуса</th>
      <th>Пользовательская история</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Онлайн-бронирование</td>
      <td>Я, как клиент, хочу иметь возможность легко забронировать мойку онлайн, чтобы я мог выбрать удобное для меня время.</td>
    </tr>
        <tr>
      <td>Прозрачность цен и услуг</td>
      <td>Я, как клиент, хочу видеть список доступных услуг и их стоимость на сайте и в приложении, чтобы я мог выбрать наиболее подходящий вариант.</td>
    </tr>
      <tr>
      <td>Напоминания</td>
      <td>Я, как клиент, хочу получать уведомления о приближении времени моего бронирования, чтобы не опоздать.</td>
    </tr>
     <tr>
      <td>Дополнительные услуги</td>
      <td>Я, как клиент, хочу иметь возможность выбрать дополнительные услуги, такие как химчистка салона или полировка кузова, во время бронирования.</td>
    </tr>
      <tr>
      <td>Качество мойки</td>
       <td>Я, как клиент, хочу чтобы мой автомобиль был вымыт качественно и эффективно, чтобы он выглядел чистым и блестящим.</td>
    </tr>
     <tr>
      <td>Комфорт ожидания</td>
      <td>Я, как клиент, хочу удобную и безопасную зону ожидания, пока мой автомобиль моют.</td>
    </tr>
    <tr>
      <td>Варианты оплаты</td>
      <td>Я, как клиент, хочу иметь возможность оплачивать услуги различными способами, включая наличные, карты и электронные платежи.</td>
    </tr>
       <tr>
      <td>Программа лояльности</td>
       <td>Я, как клиент, хочу получить скидку или бонусную программу за частое посещение автомойки.</td>
    </tr>
    <tr>
      <td>Обратная связь</td>
      <td>Я, как клиент, хочу иметь возможность оставить отзыв о качестве услуг автомойки.</td>
    </tr>
       <tr>
      <td>Доступность и навигация</td>
       <td>Я, как клиент, хочу легко найти автомойку на карте и получить указания по маршруту.</td>
    </tr>

  </tbody>
</table>


 # 2) usecase
    
![image](https://github.com/user-attachments/assets/ab5561d0-a6c3-43cf-a425-5154d75e01c8)

<details>
        <summary>usercase code</summary>

                  @startuml
                left to right direction
                actor "Клиент" as fc
                rectangle автомойка {
                  usecase "UC1: поиск автомойки" as UC1
                  usecase "UC2: Выбор даты и времени" as UC2
                  usecase "UC3: Выбор услуги" as UC3
                  usecase "UC4: Оплата" as UC4
                  usecase "Платежная система" as US5
                
                }
                
                fc --> UC1
                fc --> UC2
                fc --> UC3
                fc --> UC4
                UC4 ..> US5:(include)

                
                @enduml
</details>
### функциональные требования 


#### описание
        1)usecase:
         а) uc1: найти автомойку
                 участники: 
                  пользователь приложения
                 предусловия:
                        пользователь зарегистрирован и авторизован
                 условия для запуска сценария:
                        batton: "найти мойку"
                 признак успешности:
                         Пользователь выбрал автомойку
 ##### Базовый Сценарий 1
                1) система проверяет, что user передал свою геолокацию
                        ЕСЛИ: если геолокации нет
                                 ТО: система переходит к Базовому сценарию 3
                2) система ищет ближайщие к позиции user мойки AL_01
                3) система формирует список моек
                4) система отображает экран с картой и списком моек UI_01
                5) система ожидает выбора мойки user
                6) система переходит к экрану выбора услуг
                7) Сценарий завершен
                        
                                
                    
                                
##### Базовый Сценарий 2
          б) uc2: записаться на автомойку
                1) система выводит сообщение user с прозьбой разрешить передать геолокацию
                2) если: user разрешил передачу геолокации:
                        то: переход базовый сценарий 1 шаг 2
                        иначе: система переходи к базовому сценарию 3
        
 #### Базовый сценарий 3
                1) система отоборажает поле для ввода адреса
                2) система ожидает от user  ввод адреса 
                3) система переходит на Базовый сценарий 1 на шаг 2
 ####  альтернативный сценарий
                1) AC_1: некоректный запрос пользователя
                2) AC_2: ....
                .
                .
                .
                        
 ##### Базовый сценарий 4
                г) us3: выбор услуги
                        1) Система формирует список услуг 
                        2) Система выводит список услуг на экран пользователя
                        3) пользователь выбирает услугу
                        4) Система просить подвердить выбранные услуги (да или нет)
                        5) если пользователь выбирает "да"
                                6)система переходит следующему сценарию "оплата услуг"
                        5) если пользователь выбирает "нет"
                                6)система переходит переходит началу сценария 4
                       
 ##### Базоовый сценарий 5
        д) us4: Оплата услуг
                        1) система формирует список способов оплаты
                а) оплата картой через приложения
                        2) Пользователь выбирает способ оплаты (карта, приложение, qr-код)
                        3) система выводит способ оплаты
                        4) пользователь оплачиваает
                        5) система проверяет статус платежа
                        6) система выводит на экран статус платежа
                        7) завершениия работы програмы после подверждения статуса платежа
                        8) система отображает в разделе пользователя статус ожидания пользователя на мойке
                б) оплата наличными
                        2) система записывает в базу пользотеля
                        3) система отображает пользователю сообщения " вы успешно записались на мойку"
                        4) завершениия работы програмы после подверждения 
                        5) система отображает в разделе пользователя статус ожидания пользователя на мойке
                                
                        
 ### нефункциональные требования
                необходимые функции:
                AL_01: алгоритм по адресу и геолокации 
                        1 формирует запрос к БД
                        2...
                        3...
                        4 формируем список моек
                UI_1 : система отображает экран с картой и списком мое
        
# 3) ER-диаграмма

## Сущности и их атрибуты:
        Клиент (Customer)
                ID клиента (Customer_ID)
                Имя (Name)
                Контактный номер (Phone)
                Электронная почта (Email)
                Адрес (Address)
                Автомобиль (Car)

        ID автомобиля (Car_ID)
                Марка (Make)
                Модель (Model)
                Год выпуска (Year)
                Номерной знак (License_Plate)
                Тип (Car_Type) - легковой, внедорожник и т. д.
                Клиент_ID (Customer_ID) — связь с клиентом
                Услуга (Service)

        ID услуги (Service_ID)
                Название (Service_Name) - мойка, полировка, химчистка и т. д.
                Описание (Description)
                Цена (Price)
                Запись на мойку (SingUpForACarWash)

        ID записи (CarWash_ID)
                Дата записи (Date)
                Статус записи (Status) - подтверждена, завершена, отменена и т. д.
                Клиент_ID (Customer_ID) — связь с клиентом
                Автомобиль_ID (Car_ID) — связь с автомобилем
                Работник (Employee)

        ID работника (Employee_ID)
                Имя (Name)
                Должность (Position)
                Телефон (Phone)
                Электронная почта (Email)
                Мойка (Wash)
        
        ID мойки (Wash_ID)
                Тип мойки (Wash_Type) - автоматическая, ручная, экспресс и т. д.
                Статус мойки (Wash_Status) - в процессе, завершена, отменена
                Время начала (Start_Time)
                Время окончания (End_Time)
                Работник_ID (Employee_ID) — связь с работником
                Услуга_ID (Service_ID) — связь с услугой
                Запись_ID (SingUpForACarWash_ID) — связь с записью
        Связи:
                Клиент - Автомобиль: Один клиент может иметь несколько автомобилей.(1:M)
                Автомобиль - Запись на мойку: Один автомобиль может быть связан c несколькими записями на мойку. (1:M)
                Клиент - Запись на мойку: Один клиент может записать несколько автомобилей на мойку. (1:M)
                Услуга - Мойка: Одна услуга может быть использована в нескольких мойках. (1:M)
                Работник - Мойка: Один работник может обслуживать несколько мойок. (1:M)
                Запись на мойку - Мойка: Каждая запись на мойку связана с конкретной мойкой. (1:1)


## ER-диаграмма
![image](https://github.com/user-attachments/assets/20fa00b7-1acd-4737-970c-6ad85e3746bf)

# 4) C4 model
## c1 system context
![image](https://github.com/user-attachments/assets/ddc5fd93-34eb-441e-bb61-b45bad8ef3e3)

## c2 conteners
![image](https://github.com/user-attachments/assets/50fbd17c-8610-47c4-8c12-4511e040bb24)

## 5) sequense diagram

![Untitled](https://github.com/user-attachments/assets/2e825ba8-1ad4-458e-bf59-f8e072c67ac4)


  
        @startuml
        sequenceDiagram
            participant Пользователь
            participant Приложение
            participant Сервер
        
            activate Пользователь
            Пользователь -> Приложение: Нажать "Найти мойку"
            activate Приложение
        
            alt Геолокация доступна
                Приложение -> Приложение: Проверить геолокацию
                Приложение -> Сервер: Запрос ближайших моек
                activate Сервер
                Сервер -> Приложение: Список моек
                deactivate Сервер
                Приложение -> Пользователь: Отобразить карту и список моек (UI_01)
                Пользователь -> Приложение: Выбрать мойку
                Приложение -> Приложение: Перейти к выбору услуг
                activate Приложение
                Приложение -> Пользователь: Отобразить список услуг
                Пользователь -> Приложение: Выбрать услуги
                Приложение -> Приложение: Подтвердить выбор услуг?
                Пользователь -> Приложение: Да/Нет
                alt Пользователь выбирает "Да"
                    Приложение -> Приложение: Перейти к оплате (Базовый сценарий 5)
                else Пользователь выбирает "Нет"
                    Приложение -> Приложение: Вернуться к выбору услуг
                end
            else Геолокация недоступна
                Приложение -> Пользователь: Отобразить поле для ввода адреса
                Пользователь -> Приложение: Ввести адрес
                Приложение -> Сервер: Запрос моек по адресу
                activate Сервер
                Сервер -> Приложение: Список моек
                deactivate Сервер
                Приложение -> Пользователь: Отобразить карту и список моек (UI_01)
            end
        
            alt Оплата картой
                Приложение -> Пользователь: Выбрать способ оплаты (карта)
                Пользователь -> Приложение: Ввести данные карты
                Приложение -> Сервер: Обработать платеж
                activate Сервер
                Сервер -> Приложение: Статус платежа (успешно/неуспешно)
                deactivate Сервер
                Приложение -> Пользователь: Отобразить статус платежа
            else Оплата наличными
                Приложение -> Сервер: Записать запись в базу данных
                activate Сервер
                Сервер -> Приложение: Запись успешна
                deactivate Сервер
                Приложение -> Пользователь: Сообщение "Вы успешно записались"
            end
        
            Приложение -> Пользователь: Отобразить статус ожидания
            deactivate Приложение
            deactivate Пользователь
        
        @enduml

## 6) yaml openApi

                openapi: 3.0.0
info:
  title: Car Wash Management API
  version: 1.0.0
  description: A comprehensive API for managing a car wash business.  Includes customer management, car details, service offerings, booking creation, payment processing, and wash scheduling.
  contact:
    email: api-support@example.com
  license:
    name: MIT License
    url: https://opensource.org/licenses/MIT

servers:
  - url: https://api.carwash.example.com/v1
    description: Production server
  - url: http://localhost:3000/api/v1
    description: Development server

paths:
  /customers:
    get:
      summary: Retrieve all customers.
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A list of customers.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Customer'
        '401':
          $ref: '#/components/responses/Unauthorized'

    post:
      summary: Create a new customer.
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Customer'
      responses:
        '201':
          description: Customer created successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Customer'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'

  /customers/{customerId}:
    get:
      summary: Retrieve a specific customer.
      parameters:
        - in: path
          name: customerId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A customer.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Customer'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    put:
      summary: Update a customer.
      parameters:
        - in: path
          name: customerId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Customer'
      responses:
        '200':
          description: Customer updated successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Customer'
        '400':
          $ref: '#/components/responses/BadRequest'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    delete:
      summary: Delete a customer.
      parameters:
        - in: path
          name: customerId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '204':
          description: Customer deleted successfully.
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'


  /cars:
    get:
      summary: Retrieve all cars.
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A list of cars.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Car'
        '401':
          $ref: '#/components/responses/Unauthorized'

    post:
      summary: Create a new car.
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Car'
      responses:
        '201':
          description: Car created successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Car'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'

  /cars/{carId}:
    get:
      summary: Retrieve a specific car.
      parameters:
        - in: path
          name: carId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A car.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Car'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    put:
      summary: Update a car.
      parameters:
        - in: path
          name: carId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Car'
      responses:
        '200':
          description: Car updated successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Car'
        '400':
          $ref: '#/components/responses/BadRequest'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    delete:
      summary: Delete a car.
      parameters:
        - in: path
          name: carId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '204':
          description: Car deleted successfully.
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'


  /services:
    get:
      summary: Retrieve all services.
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A list of services.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Service'
        '401':
          $ref: '#/components/responses/Unauthorized'

    post:
      summary: Create a new service.
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Service'
      responses:
        '201':
          description: Service created successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Service'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'

  /services/{serviceId}:
    get:
      summary: Retrieve a specific service.
      parameters:
        - in: path
          name: serviceId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A service.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Service'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    put:
      summary: Update a service.
      parameters:
        - in: path
          name: serviceId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Service'
      responses:
        '200':
          description: Service updated successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Service'
        '400':
          $ref: '#/components/responses/BadRequest'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    delete:
      summary: Delete a service.
      parameters:
        - in: path
          name: serviceId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '204':
          description: Service deleted successfully.
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'


  /employees:
    get:
      summary: Retrieve all employees.
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A list of employees.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Employee'
        '401':
          $ref: '#/components/responses/Unauthorized'

    post:
      summary: Create a new employee.
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Employee'
      responses:
        '201':
          description: Employee created successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Employee'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'

  /employees/{employeeId}:
    get:
      summary: Retrieve a specific employee.
      parameters:
        - in: path
          name: employeeId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: An employee.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Employee'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    put:
      summary: Update an employee.
      parameters:
        - in: path
          name: employeeId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Employee'
      responses:
        '200':
          description: Employee updated successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Employee'
        '400':
          $ref: '#/components/responses/BadRequest'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    delete:
      summary: Delete an employee.
      parameters:
        - in: path
          name: employeeId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '204':
          description: Employee deleted successfully.
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'


  /bookings:
    post:
      summary: Create a new booking.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/BookingRequest'
      responses:
        '201':
          description: Booking created successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Booking'
        '400':
          $ref: '#/components/responses/BadRequest'
        '404':
          $ref: '#/components/responses/NotFound'

  /bookings/{bookingId}:
    get:
      summary: Retrieve a specific booking.
      parameters:
        - in: path
          name: bookingId
          schema:
            type: integer
          required: true
      responses:
        '200':
          description: A booking.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Booking'
        '404':
          $ref: '#/components/responses/NotFound'
    put:
      summary: Update a booking.
      parameters:
        - in: path
          name: bookingId
          schema:
            type: integer
          required: true
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/BookingUpdateRequest'
      responses:
        '200':
          description: Booking updated successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Booking'
        '400':
          $ref: '#/components/responses/BadRequest'
        '404':
          $ref: '#/components/responses/NotFound'
    delete:
      summary: Cancel a booking.
      parameters:
        - in: path
          name: bookingId
          schema:
            type: integer
          required: true
      responses:
        '204':
          description: Booking cancelled successfully.
        '404':
          $ref: '#/components/responses/NotFound'


  /bookings/{bookingId}/pay:
    post:
      summary: Process payment for a booking.
      parameters:
        - in: path
          name: bookingId
          schema:
            type: integer
          required: true
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/PaymentRequest'
      responses:
        '200':
          description: Payment successful. Booking status updated.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Booking'
        '400':
          $ref: '#/components/responses/BadRequest'
        '404':
          $ref: '#/components/responses/NotFound'


  /washes:
    get:
      summary: Retrieve all washes.
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A list of washes.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Wash'
        '401':
          $ref: '#/components/responses/Unauthorized'

    post:
      summary: Create a new wash.
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Wash'
      responses:
        '201':
          description: Wash created successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Wash'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'

  /washes/{washId}:
    get:
      summary: Retrieve a specific wash.
      parameters:
        - in: path
          name: washId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '200':
          description: A wash.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Wash'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    put:
      summary: Update a wash.
      parameters:
        - in: path
          name: washId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Wash'
      responses:
        '200':
          description: Wash updated successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Wash'
        '400':
          $ref: '#/components/responses/BadRequest'
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'
    delete:
      summary: Delete a wash.
      parameters:
        - in: path
          name: washId
          schema:
            type: integer
          required: true
      security:
        - ApiKeyAuth: []
      responses:
        '204':
          description: Wash deleted successfully.
        '404':
          $ref: '#/components/responses/NotFound'
        '401':
          $ref: '#/components/responses/Unauthorized'



components:
  schemas:
    Customer:
      type: object
      properties:
        customerId:
          type: integer
          readOnly: true
        name:
          type: string
        phone:
          type: string
          format: phone
        email:
          type: string
          format: email
        address:
          type: string

    Car:
      type: object
      properties:
        carId:
          type: integer
          readOnly: true
        make:
          type: string
        model:
          type: string
        year:
          type: integer
        licensePlate:
          type: string
        carType:
          type: string
          enum: [sedan, suv, truck, minivan, etc.]
        customerId:
          type: integer

    Service:
      type: object
      properties:
        serviceId:
          type: integer
          readOnly: true
        serviceName:
          type: string
        description:
          type: string
        price:
          type: number
          format: float

    Employee:
      type: object
      properties:
        employeeId:
          type: integer
          readOnly: true
        name:
          type: string
        position:
          type: string
        phone:
          type: string
          format: phone
        email:
          type: string
          format: email

    BookingRequest:
      type: object
      properties:
        customerId:
          type: integer
        carId:
          type: integer
        serviceId:
          type: integer
        date:
          type: string
          format: date
        time:
          type: string
          format: time

    BookingUpdateRequest:
      type: object
      properties:
        date:
          type: string
          format: date
        time:
          type: string
          format: time
        status:
          type: string
          enum: [confirmed, completed, cancelled]

    Booking:
      type: object
      properties:
        bookingId:
          type: integer
          readOnly: true
        date:
          type: string
          format: date
        time:
          type: string
          format: time
        status:
          type: string
          enum: [confirmed, completed, cancelled, pending_payment, paid]
        customerId:
          type: integer
        carId:
          type: integer
        serviceId:
          type: integer
        employeeId:
          type: integer
        totalPrice:
          type: number
          format: float

    PaymentRequest:
      type: object
      properties:
        paymentMethod:
          type: string
          enum: [card, cash]
        cardDetails:
          type: object
          properties:
            cardNumber:
              type: string
            expiryDate:
              type: string
            cvv:
              type: string
        amount:
          type: number
          format: float

    Wash:
      type: object
      properties:
        washId:
          type: integer
          readOnly: true
        washType:
          type: string
          enum: [automatic, manual, express, detail]
        washStatus:
          type: string
          enum: [in_progress, completed, cancelled, scheduled]
        startTime:
          type: string
          format: date-time
        endTime:
          type: string
          format: date-time
        employeeId:
          type: integer
        serviceId:
          type: integer
        bookingId:
          type: integer

    Error:
      type: object
      properties:
        message:
          type: string
        code:
          type: integer
        details:
          type: array
          items:
            type: string


  responses:
    BadRequest:
      description: Bad Request.  The request is invalid or contains errors.
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
    NotFound:
      description: Not Found. The requested resource was not found.
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
    Unauthorized:
      description: Unauthorized.  Requires API key authentication.
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'

  securitySchemes:
    ApiKeyAuth:
      type: apiKey
      in: header
      name: x-api-key


