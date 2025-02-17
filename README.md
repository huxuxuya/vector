# **Vector_TechJournal.** Парсинг технологического журнала 1С (elastic)


- [Назначение](#назначение)
    - [Возможности](#возможности)
- [Реализация](#реализация)
- [Запуск](#запуск)
- [План реализации](#планы)
- [Лицензия](#лицензия)

## Назначение

Данный проект создан для того чтобы искоренить боль от использования технологического журнала.

Использование ТЖ должно свестись к трем простым действиям.
- Настроил ТЖ
- Запустил сборщик
- Приступил к анализу.

### Возможности

- Vector_TechJournal - это конфигурация Vector для разбора и трансформации файлов технологического журнала
- Предоставляет возможности чтения файлов  ТЖ
- В планах реализация разбора всех известных событий ТЖ.
- Выгрузка результатов парсинга в различных форматах
    - В файлы в различных форматах
    - В в консоль
    - В **Clickhouse**
    - В **Loki** и другие аггрегаторы логов 
- Возможность масштабирования решения в случае большего объема логов


## Реализация

Продукт представлен в виде docker-compose файла и пригоден для запуска в любой среде поддерживающей контейнеры, а так же файлов конфигурации для него.
Конфигурация обработки каждого отдельного вида событий находится в **[./config/transformations/](/config/transformations/)\<EventName>.vrl**



## Запуск

Для запуска разбора технологического журнала достаточно:

Отредактировать файл techJournal.env
    - указать необходимые события которые вы планируете хранить

Выполнить команду:
    docker-compose -f es-vector-docker-compose.yml up -d

Положить логи в ./logs

В кибане появятся записи http://localhost:5601/.

Можно настроить еще индексы [elastic set index](/elastic set index) 

Еще можно отключить сообщение секурности:
    docker exec -it <container_id> bash
    cd /usr/share/elasticsearch/config
    echo "xpack.security.enabled: false" >> elasticsearch.yml

## Планы
- Дописать разбор самых востребованых событий.
- Отладить и оптимизировать разбор.
- Добавить словари для "Очеловечивания" информации
- Реализовать фронтенд для удобного просмотра и анализа ТЖ

---

## Лицензия

Distributed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)
