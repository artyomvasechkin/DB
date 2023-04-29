Подключаемся к Redis (после возникновения проблем с подключением через colab, перешел в VS Code)
![](screen6.jpg)
![](screen7.jpg)
![](screen1.jpg)

С помощью команд set, hset, zcard и lpush разобьем исходный json на структуры строка, hset, zset, list
Сначала разобьем на строки и hset
![](screen2.jpg)

Теперь на zset:
![](screen4.jpg)

И наконец list:
![](screen5.jpg)


Протестируем скорости сохранения и чтения
Для hset:
![](screen6.jpg)

ыскуут3.jpg
Для zset:
![](screen4.jpg)

Для list:
![](screen5.jpg)



Настроим Redis Cluster на нодах:
Для этого создадим репозитории с файлами конфигурации в них и запустим их одновременно. После этого напишем следущий код:
![](screen8.jpg)

По аналогии с Redis:
![](screen9.jpg)

Пример работы команды:
![](screen10.jpg)
