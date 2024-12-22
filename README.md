# Финальный проект по спринту 1 от Яндекса по языку GO
## Что из себя представляет?
### это сервис по выполнению простых математических вычислений таких как:
1.Сложение 
2.Вычитание
3.Умножение
4.Деление
(+,-,*,/)

## Как использовать?

### Клонируем репозиторий командой 
```
git clone git@github.com:BelozubEgor/Final-task.git
```
### Переходим в нужную папку
```
cd FinalTaskFirstModule
```
### Команда для запуска приложения

```
go run ./cmd/main.go
```
для выхода используем ctrl + c
### для начала работы с приложением переходим в cmd и начинаем отправлять curl запросы

cURL команда с ответом сервиса 200:

```
 curl --location '127.0.0.1:8080/api/v1/calculate' --header 'Content-Type: application/json' --data '{
  "expression": "2+2*2"
}'
```
Ответ:

```
{"result":"6.00000000"}
```

cURL команда с ответом сервиса 400:
```
curl --location '127.0.0.1:8080/api/v1/calculate' --header 'Content-Type: application/json' --data '{
  "expression": "2+2*2
}'
```
Ответ:
```
{"error":"Bad request"}
```

cURL команда с ответом сервиса 405:
```
curl --request GET \ --url '127.0.0.1:8080/api/v1/calculate' --header 'Content-Type: application/json' --data '{
  "expression": "2+2*2"
}'
```
Ответ:
```
{"error":"You can use only POST method"}
```

cURL команда с ответом сервиса 422:
```
curl --location '127.0.0.1:8080/api/v1/calculate' --header 'Content-Type: application/json' --data '{
  "expression": "2+2*2)"
}'
```
Ответ:
```
{"error":"Expression is not valid"}
```

cURL команда с ответом сервиса 422 с делением на 0:
```
curl --location '127.0.0.1:8080/api/v1/calculate' --header 'Content-Type: application/json' --data '{
  "expression": "(2+2*2)/0"
}'
```
Ответ:
```
{"error":"division by zero"}
```

## Используемые библиотеки:
- **`net/http`**: Базовый HTTP-сервер для обработки запросов.
- **`errors`**:Библиотека для работы с ошибками.
- **`io`**:Базовые интерфейсы для работы с вводом и выводом.
- **`bytes`**:Утилиты для работы с байтовыми срезами.
- **`encoding/json`**:Кодирование и декодирование JSON.
- **`fmt`**:Форматированный ввод/вывод.
- **`net/http/httptest`**:Инструменты для тестирования HTTP-серверов и клиентов.
- **`testing`**:Предоставляет инструменты для написания и организации модульных, интеграционных и нагрузочных тестов.
- **`strings`**:Утилиты для работы со строками.
- **`strconv`**:Преобразование строк в числа, булевые значения и обратно.
- **`unicode`**:Работа с символами Unicode.
- **`os`**:Работа с операционной системой.

## Архитектура 

- **`cmd/`**
  - **`main.go`**
  
- **`application/`**
  - **`app.go/`**
  - **`app_test.go/`**
- **`pkg/`**
  - **`calc/`**
    - **`calc.go`**
    - **`err.go`**
    - **`calc_test.go`**
