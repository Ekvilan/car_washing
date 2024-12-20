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
    
![image](https://github.com/user-attachments/assets/33369949-f9c6-4ea9-8516-e0df8f7508d4)

<details>
        <summary>usercase code</summary>
        
        @startuml
        left to right direction
        actor "Клиент" as fc
        rectangle "Система оплаты" as r1
        rectangle "Автомойка" {
            usecase "UC1: Поиск автомойки" as UC1
            usecase "UC2: Выбор автомойки" as UC2
            usecase "UC3: Выбор даты и времени" as UC3
            usecase "UC4: Выбор услуги" as UC4
            usecase "UC5: Просмотр доступных услуг" as UC5
            usecase "UC6: Оплата" as UC6
            usecase "UC7: Просмотр истории заказов" as UC7
            usecase "UC8: Управление профилем" as UC8
            usecase "UC9: Поддержка клиентов" as UC9
            usecase "Платежная система" as US1  
        }
          
        fc --> UC1
        UC1 ..> UC2 : (include)
        fc --> UC3
        fc --> UC4
        UC4 ..> UC5: (include)
        fc --> UC6
        UC6 ..> US1 : (include)
        US1 --> r1
        fc --> UC7
        fc --> UC8
        fc --> UC9
        
</details>

### функциональные требования 
1) usecase: UC1: Найти автомойку
   
                Участники: Пользователь приложения
                Предусловия: Пользователь зарегистрирован и авторизован
                Условия для запуска сценария: Пользователь нажимает кнопку “Найти мойку”
                Признак успешности: Пользователь выбрал автомойку
   
Базовый Сценарий 1:

        Система проверяет, что пользователь передал свою геолокацию.
        ЕСЛИ: Геолокации нет.
        ТО: Система переходит к Альтернативному Сценарию 1.
        Система ищет ближайшие к позиции пользователя мойки AL_01.
        Система формирует список моек.
        Система отображает экран с картой и списком моек UI_01.
        Система ожидает выбора мойки пользователем.
        Система переходит к экрану выбора услуг.
        Сценарий завершен.
        
Альтернативный Сценарий 1: Нет геолокации
        
        Система выводит сообщение об ошибке “Не удалось получить геолокацию”.
        Система предлагает пользователю ввести адрес вручную.
        ЕСЛИ: Пользователь вводит адрес.
        ТО: Система переходит к базовому сценарию 1 (с использованием введенного адреса).
        ЕСЛИ: Пользователь не вводит адрес.
        ТО: Система выводит сообщение «Пожалуйста, укажите геолокацию или адрес».
        Система переходит к экрану выбора услуг.
        Сценарий завершен.
        
2) usecase: UC2: Выбор автомойки

        Участники: Пользователь приложения
        Предварительные условия: Пользователь просматривает экран со списком моек (UI_01).
        Условия для запуска сценария: пользователь выбирает конкретную автомойку из списка.
        Признак успешности: пользователь перешел к экрану выбора даты и времени (UI_02).
        Базовый Сценарий:
        Система отображает экран с подробной информацией о выбранной мойке (UI_02) (адрес, рейтинг, список услуг и т. д.).
        Система ожидает подтверждения выбора мойки пользователем.
        После подтверждения система переходит к экрану выбора даты и времени (UI_03).
        Сценарий завершен.
   
3) usecase: UC3: Выбор даты и времени

        Участники: Пользователь приложения
        Предварительные условия: пользователь выбрал автомойку и перешел на экран выбора даты и времени (UI_03).
        Условия для запуска сценария: пользователь взаимодействует с элементами управления выбором даты и времени.
        Признак успешности: Пользователь выбрал дату и время посещения автомойки.
        Базовый Сценарий:
        Система отображает календарь и расписание доступных временных слотов для выбранной автомойки.
        Система ожидает выбора пользователем даты и времени.
        Система проверяет доступность выбранного времени.
        ЕСЛИ: Выбранное время недоступно. * ТО: Система выводит сообщение об ошибке «Выбранное время недоступно».
        ТО: Система предлагает выбрать другое время.
        После выбора доступного времени система переходит к экрану выбора услуг (UI_04).
        Сценарий завершен.
   
4) usecase: UC4: Выбор услуги

        Участники: Пользователь приложения
        Предварительные условия: Пользователь выбрал автомойку, а также дату и время.
        Условия для запуска сценария: Пользователь взаимодействует с элементами управления выбором услуги.
        Признак успешности: Пользователь выбрал услугу.
        Базовый Сценарий:
        Система отображает экран со списком услуг, доступных для выбранной автомойки (UI_04).
        Система ожидает выбора услуги пользователем.
        Система добавляет выбранную услугу в корзину.
        Система отображает общую стоимость заказа.
        Система переходит к экрану оплаты (UI_05).
        Сценарий завершен.
   
5) usecase: UC5: Просмотр доступных услуг

        Участники: Пользователь приложения
        Предусловия: Пользователь находится на экране выбора услуги (UI_04).
        Условия для запуска сценария: Пользователь открывает страницу просмотра услуг.
        Признак успешности: Пользователь просматривает доступные услуги.
        Базовый Сценарий:
        Система отображает список услуг, доступных в выбранной автомойке.
        Для каждой услуги система отображает цену и краткое описание.
        Система ожидает, когда пользователь закончит просмотр услуг.
        Система закрывает страницу просмотра услуг и возвращается к UI_04.
        Сценарий завершен.
   
6) usecase: UC6: Оплата

        Участники: Пользователь приложения
        Предусловия: Пользователь выбрал услугу.
        Условия для запуска сценария: Пользователь нажимает кнопку “Оплатить”.
        Признак успешности: Оплата успешно произведена.
        Базовый Сценарий:
        Система отображает экран выбора способа оплаты (UI_05).
        Пользователь выбирает способ оплаты и вводит необходимые данные.
        Система перенаправляет пользователя в платежную систему.
        Платежная система обрабатывает оплату.
        ЕСЛИ: Оплата прошла успешно.
        ТО: Система перенаправляет пользователя на экран подтверждения оплаты UI_06.
        ЕСЛИ: Оплата не прошла.
        ТО: Система выводит сообщение об ошибке.
        ТО: Система предлагает повторить оплату.
        Сценарий завершен.
   
7) usecase: UC7: Просмотр истории заказов

        Участники: Пользователь приложения
        Предусловия: Пользователь авторизован.
        Условия для запуска сценария: Пользователь нажимает кнопку “История заказов”.
        Признак успешности: Пользователь просматривает список своих прошлых заказов.
        Базовый Сценарий:
        Система загружает список прошлых заказов пользователя из базы данных.
        Система отображает список заказов на экране (UI_07).
        Для каждого заказа система отображает дату, время, автомойку, список услуг и стоимость.
        Система ожидает, пока пользователь не завершит просмотр истории.
        Сценарий завершен.
   
8) usecase: UC8: Управление профилем

        Участники: Пользователь приложения
        Предусловия: Пользователь авторизован.
        Условия для запуска сценария: пользователь нажимает кнопку «Профиль» или «Настройки профиля».
        Признак успешности: пользователь может просматривать и изменять личную информацию, настройки аккаунта.
        Базовый Сценарий:
        Система отображает экран с данными профиля пользователя (UI_08).
        Система предоставляет возможность изменить личную информацию, например, имя, email, телефон.
        Система предоставляет возможность изменить пароль.
        Система позволяет сохранять внесенные изменения.
        ЕСЛИ: Сохранение прошло успешно.
        ТО: Система выводит сообщение “Изменения успешно сохранены”.
        ЕСЛИ: Сохранение не прошло.
        ТО: Система выводит сообщение об ошибке.
        Система переходит к предыдущему экрану.
        Сценарий завершен.
   
9) usecase: UC9: Поддержка клиентов

        Участники: Пользователь приложения
        Предусловия: Пользователь авторизован.
        Условия для запуска сценария: пользователь нажимает кнопку «Поддержка» или «Связаться с нами».
        Признак успешности: пользователь получает доступ к форме обратной связи или информации о поддержке.
        Базовый Сценарий:
        Система отображает экран с формой обратной связи или информацией о контактах поддержки (UI_09).
        Система позволяет пользователю отправить сообщение в службу поддержки.
        ЕСЛИ: Сообщение отправлено успешно.
        ТО: Система выводит сообщение “Ваше сообщение отправлено”.
        Система переходит на предыдущий экран.
        Сценарий завершен.
        
# 3) ER-диаграмма

## Сущности и их атрибуты:

      ' Стиль
        skinparam classAttributeIconSize 0
        skinparam class {
            BackgroundColor White
            BorderColor Black
            ArrowColor Black
        }
        
        ' Сущности
        class Customer {
            {field} Customer_ID: int
            {field} Name: string
            {field} Phone: string
            {field} Email: string
            {field} Address: string
        }
        
        class Car {
            {field} Car_ID: int
            {field} Make: string
            {field} Model: string
            {field} Year: int
            {field} License_Plate: string
            {field} Car_Type: string
            {field} Customer_ID: int
        }
        
        class Service {
            {field} Service_ID: int
            {field} Service_Name: string
            {field} Description: string
            {field} Price: float
        }
        
        class SingUpForACarWash {
             {field} CarWash_ID: int
            {field} Date: date
            {field} Status: string
            {field} Customer_ID: int
             {field} Car_ID: int
            {field} Employee_ID: int
        
        }
        
        class Employee {
            {field} Employee_ID: int
            {field} Name: string
            {field} Position: string
            {field} Phone: string
             {field} Email: string
        }
        
        class Wash {
            {field} Wash_ID: int
            {field} Wash_Type: string
            {field} Wash_Status: string
            {field} Start_Time: time
            {field} End_Time: time
            {field} Employee_ID: int
            {field} Service_ID: int
             {field} SingUpForACarWash_ID: int
        }
        
        ' Связи
        Customer "1" -- "0..*" Car : has >
        Car "1" -- "0..*" SingUpForACarWash : has >
        Customer "1" -- "0..*" SingUpForACarWash : has >
        Service "1" -- "0..*" Wash : has >
        Employee "1" -- "0..*" Wash : has >
        SingUpForACarWash "1" -- "1" Wash : has >


## ER-диаграмма
![image](https://github.com/user-attachments/assets/39d86b11-ac5a-420a-8c0b-29d6dbd3f5d3)

# 4) C4 model
## c1 system context
![393165618-cc2e2f8b-06e3-4b8f-9303-5be7e35c8dd2](https://github.com/user-attachments/assets/a9862816-3ec1-428c-82ec-429451909ea2)

## c2 conteners
![393170179-b3ff8dc0-3aa8-432c-b65b-852f5980ed96](https://github.com/user-attachments/assets/07d817a1-dddb-4ab9-8956-a92208123a2b)

## 5) sequense diagram
пользователь ищет автомойку

![image](https://github.com/user-attachments/assets/27d3b633-15a2-4232-b671-ad7fa00a438f)



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


