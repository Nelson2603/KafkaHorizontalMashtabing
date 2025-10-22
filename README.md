# Kafka Horizontal Scaling Project

Микросервисная архитектура с горизонтальным масштабированием на основе Apache Kafka.

## Архитектура проекта

Проект состоит из следующих микросервисов:

- **OrderService1** - Сервис обработки заказов (экземпляр 1)
- **OrderService2** - Сервис обработки заказов (экземпляр 2) 
- **TransactionService1** - Сервис обработки транзакций (экземпляр 1)
- **TransactionService2** - Сервис обработки транзакций (экземпляр 2)
- **LogService** - Сервис логирования

## Технологический стек

- **Java 17+**
- **Spring Boot 3.x**
- **Apache Kafka** - для обмена сообщениями между сервисами
- **PostgreSQL** - основная база данных
- **Gradle** - система сборки

## Настройка базы данных

Все сервисы настроены для работы с PostgreSQL. Настройки базы данных находятся в файлах `application.yml` каждого сервиса.

### Требования к базе данных

- PostgreSQL 13+
- Создайте базы данных для каждого сервиса:
  - `order_service_db` - для OrderService1 и OrderService2
  - `transaction_service_db` - для TransactionService1 и TransactionService2  
 

## Запуск проекта

### Предварительные требования

1. Установите Java 17+
2. Установите PostgreSQL
3. Установите Apache Kafka

### Настройка базы данных



### Запуск сервисов

```bash
# Запуск всех сервисов
./gradlew bootRun

# Или запуск отдельных сервисов
./gradlew :OrderService1:bootRun
./gradlew :OrderService2:bootRun
./gradlew :TransactionService1:bootRun
./gradlew :TransactionService2:bootRun
./gradlew :LogService:bootRun
```

## Порты сервисов

- **OrderService1**: 8081
- **OrderService2**: 8082
- **TransactionService1**: 8083
- **TransactionService2**: 8084
- **LogService**: 8085



## Горизонтальное масштабирование

Проект поддерживает горизонтальное масштабирование через:
- Множественные экземпляры сервисов (OrderService1/2, TransactionService1/2)
- Kafka для распределения нагрузки
- Общую базу данных с разделением по сервисам

## Разработка

### Структура проекта

```
├── OrderService1/          # Сервис заказов (экземпляр 1)
├── OrderService2/          # Сервис заказов (экземпляр 2)
├── TransactionService1/    # Сервис транзакций (экземпляр 1)
├── TransactionService2/    # Сервис транзакций (экземпляр 2)
├── LogService/            # Сервис логирования
└── settings.gradle.kts    # Настройки Gradle мультипроекта
```

### Добавление новых сервисов

1. Создайте новую папку для сервиса
2. Добавьте `include("ServiceName")` в `settings.gradle.kts`
3. Создайте `build.gradle.kts` для сервиса
4. Настройте `application.yml` с портом и базой данных
