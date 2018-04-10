# HTTP 

**HTTP** -  текстовый протокол прикладного уровня. Сессия в HTTP - запрос/ответ.

**Telnet** — сетевой протокол для реализации текстового интерфейса по сети (в современной форме — при помощи транспорта TCP). 30 секундный интервал - после которого закрывается соединение.

**cURL** — (распространяемая по лицензии MIT), кроссплатформенная служебная программа командной строки, позволяющая взаимодействовать с множеством различных серверов по множеству различных протоколов с синтаксисом URL.

## HTTP 1.0

```telnet google.com 80``` - установка связи с сервером

Запрос:

```ping google.com``` 

Ответ:

```PING google.com (64.233.164.101): 56 data bytes``` 

Запрос:

* Request line

```HEAD / HTTP/1.0```

* Заголовки, отделяются переводом строки

```user-agent: Mozilla/<version> <platform> <extensions>```

* Два перевода строки - конец запроса

Ответ:

```HTTP/1.0 200 OK```

## HTTP 1.1

HTTP/1.1 - добавляет виртуальные хосты (много сайтов на одном IP адресе) и keep alive (соединение tcp не закрывается после ответа)

* Request line должен включать ```host```

```
HEAD / HTTP/1.1
host: anysite.ru
```

* Закрыть соединение
```connection: close```

## Тело HTTP запроса

```content-length: 165``` - записывается количество байт

При указании заголовка выше, два перевода строки не приведут к отправке запроса/ответа

```content-type: text/plain``` - также необходимо указывать тип контента

## Отправка форм

```content-type: application/x-www-form-urlencoded```

```login=user&password=87485```

## Transfer encoding 

```Transfer encoding: chuncked```

**Chunked transfer encoding** — механизм передачи данных в протоколе передачи гипертекста (HTTP), позволяющий надёжно доставлять данные от сервера клиенту (чаще всего клиентскому web-браузеру) без необходимости заранее знать точный размер всего тела HTTP-сообщения.

Для отделения записей размеров блоков (частей) от их содержания используется разделитель CRLF (как строка: «\r\n»; как байты в формате HEX: 0x0D, 0x0A). Длина блока — это размер содержания блока, разделители CRLF не учитываются.

Схематическое представление: <длина блока в HEX><CRLF><содержание блока><CRLF>

Последний блок строится по той же схеме, потому имеет следующий вид по причине отсутствия содержания: 0<CRLF><CRLF>

Завершающий чанк нулевой длинны и после него два перевода строки.

## Передача данных query string

```GET /?key=value HTTP/1.1```

Query string 255 символов
Не имеет отношения к GET

## Basic access authentication

```Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l``` username:password в base64

## Cookie 

HTTP - stateless протокол (каждый запрос/ответ не связан с предыдущим запросом/ответом)

Запрос:

```cookie: key=value;``` - параметры не отправляются 

Ответ:

Без параметров - сессионная кука. Уничтожается при закрытии браузера.

```set-cookie: key=value; parameter=value;``` - персистентная кука.


```expires``` - параметр, дата удаления куки

```max-age``` - секунды до удаления куки

```domain```, ```path``` - на что распространяется кука, не может отличатся от текущего имени сайта

