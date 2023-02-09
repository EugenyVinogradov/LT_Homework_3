# Домашнее задание к лекции 3 «Проведение нагрузочного веб-тестирования»

### Задание

1. Самостоятельно написать сценарий тестирования покупки билета и получения QR-кода.
2. Провести раунд тестирования.
3. Найти предел производительности сайта.

Сценарий:
1. Открыть [блог](http://qamidhl.x10.mx/wp/).
2. Авторизоваться под пользователем:
    qamidl1/ ******.
3. Открыть [пост](http://qamidhl.x10.mx/wp/).
4. Добавить комментарий, заполнив поле `Comment`.

### Инструменты для выполнения домашнего

## 1. Работа с `BlazeMeter`

1. Зарегистрироваться на сайте `BlazeMeter`.
2. Записать тест с помощью системы `BlazeMeter`.
3. Проиграть скрипт в системе `BlazeMeter`.
4. Прислать скриншоты получившейся нагрузки.

### Скриншот BlazeMeter:
![BlazeMeter](https://user-images.githubusercontent.com/98056528/217747333-fc740989-7613-4ed5-840a-3c9d410dedfe.png)

---
    
## 2.  Работа с `JMeter`

1. Склонировать репозиторий с сайтом кинотеатра.
    
git clone https://github.com/mshegolev/congenial-potato.git
cd congenial-potato

2. Запустить сайт кинотеатра.
    
cd cinema
docker-compose up -d

3. Убедиться, что сайт кинотеатра доступен [по ссылке](http://localhost:8000/).
4. Написать тест в JMeter по открытию [сайта](http://localhost:8000/).
5. Запустить тест для одного пользователя.
6. Сделать скриншот о выполнении сценария с помощью `View Results Tree`.
7. Сделать скриншот стандартного отчёта JMeter о проведённом тестировании.

### Скриншоты JMeter:
#### `View Results Tree`
![image](https://user-images.githubusercontent.com/98056528/217759602-8101791e-f6fa-462e-8fb7-f523afaba1cf.png)

#### `Summary Report`
![image](https://user-images.githubusercontent.com/98056528/217759221-3a497fac-b3bc-4869-9ddf-7ce2d15a8d3b.png)
---
  
## 3.  Работа с `JMeter`

1. Настроить запись метрик в систему мониторинга.
2. Запустить тест по разработанному профилю нагрузки.
3. Сделать скриншот полученных результатов из системы монитронига.

### Скриншот JMeter Thread Group:
![image](https://user-images.githubusercontent.com/98056528/217831120-703991e9-be3e-4e33-b743-bfbd611b0fed.png)

### Скриншот Grafana:
![image](https://user-images.githubusercontent.com/98056528/217855890-cca3b324-67aa-4e2a-88d7-4dd23b88df34.png)

### Файлы конфигурации:
#### prometheus.yml:
```YAML
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
# - job_name: "WMI Exporter"

#   static_configs:
#     - targets: ["localhost:9182"]    
  - job_name: "JMeter"

    static_configs:
      - targets: ["localhost:9270"]
```
#### JMeter user.properties:
```
# Sample user.properties file
#

prometheus.port = 9270
prometheus.ip = 127.0.0.1
prometheus.save.threads = true
prometheus.save.threads.name = jmeter_threads
prometheus.save.jvm = true
```

