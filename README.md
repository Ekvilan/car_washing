# code для схемы автомойки
    @startuml
left to right direction
actor "Ресторанный критик" as fc
rectangle оплата as ps
rectangle автомойка {
  usecase "поиск автомойки" as UC1
  usecase "Выбор даты и времени" as UC2
  usecase "Выбор услуги" as UC3
  usecase "Оплата" as UC4
  usecase "Отмена" as UC5
  usecase "" as UC6
}

fc --> UC1
fc --> UC2
fc --> UC3
fc --> UC4
fc --> UC5
ps <-- UC4
@enduml
