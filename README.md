**История развития**


VoltDB — реляционная резидентная СУБД без разделяемых ресурсов (англ. shared-nothing architecture) с поддержкой SQL, разработанная под руководством Майкла Стоунбрейкера, Сэмьюэла Мэддена и Даниеля Абади в начале 2010-х годов на основе академического проекта H-Store.
Данные в кластере сегментируются, сегмент обслуживается одним аппаратным потоком. Поддерживается синхронная репликация между сегментами. Для обеспечения надежности ведётся журнал предзаписи и используются непрерывные снимки. Начиная с версии 5.1 (марте 2015) обеспечивается репликация на основе журнала предзаписи (вместо повторного применения операции).
Имеется две редакции: коммерческая (Enterprise) и общественная (Community, опубликована под лицензией GNU Affero General Public License). Среди дополнительных возможностей коммерческой версии, недоступных в общественной — обеспечение высокой доступности, поддержка экспорта данных.
VoltDB Community Edition 1.0 (май 2010) — первый выпуск, распространяющийся под лицензией GPLv3;
VoltDB 1.2 (октябрь 2010) — выпуск под двумя лицензиями: общедоступной (VoltDB Community Edition) и коммерческой (VoltDB Enterprise Edition);
VoltDB 2.0 (сентябрь 2011) — поддержка журнала выполняемых команд (только в VoltDB Enterprise Edition);
VoltOne (октябрь 2011) — одноузловая редакция VoltDB Enterprise Edition;
VoltDB 2.5 (апрель 2012) — репликация сегментов и баз, репликация и восстановление кластера внутри и между центрами обработки данных (только VoltDB Enterprise Edition);
VoltDB 3.0 (январь 2013) — ускорено выполнение запросов, предложены средства для модификации схемы данных без остановов, расширена поддержка SQL, высокопроизводительный экспорт данных (только VoltDB Enterprise Edition).;
VoltDB 4.0 (январь 2014) — расширены возможности для аналитики в оперативной памяти и поддержка множества новых SQL, значительно увеличена производительность и пропускная способность при чтении аналитики, увеличения размера работающего Кластера без блокировок, поддержка хранимых процедур на языке Groovy, утилита миграции данных из MySQL, интерактивное обучение наряду с Volt Vanguard сертификацией.
VoltDB 5.0 (январь 2015) — включены средства интеграции с экосистемой Hadoop, в том числе средства экспорта (Kafka, HDFS, HTTP, RabbitMQ) и импорта (Kafka Loader, JDBC Loader, VoltDB Hadoop OutputFormat, Vertica UDx, Apache Hive и Apache Pig); расширение поддержки SQL, VoltDB Management Center (веб-браузерная панель для мониторинга и управления конфигурацией;
VoltDB 5.1 (март 2015) — репликация на журналах предзаписи без единой точки отказа;
VoltDB 6.0 (январь 2016) — поддержка геоданных, репликация в режиме активный — активный между различными площадками.


Инструменты для взаимодействия с СУБД.


Некоторые клиентские интерфейсы разрабатываются и упаковываются как часть стандартного дистрибутива VoltDB, а другие компилируются и распространяются как отдельные клиентские наборы. На момент написания этой статьи для VoltDB доступны следующие клиентские интерфейсы:
С#
С++
Эрланг
Идти
Java (в комплекте с VoltDB)
JDBC (в комплекте с VoltDB)
JSON (в комплекте с VoltDB)
Node.js
PHP
Python (в комплекте с VoltDB)
Клиентский интерфейс JSON может представлять особый интерес, если ваш любимый язык программирования не указан выше. JSON — это формат данных, а не интерфейс программирования, и интерфейс JSON предоставляет приложениям, написанным на любом языке программирования, возможность взаимодействовать с VoltDB посредством сообщений JSON, отправляемых по стандартному протоколу HTTP.
VoltDB предоставляет клиентский интерфейс для программ, написанных на C++. Клиентский интерфейс C++ доступен в предварительно скомпилированном виде в виде отдельного комплекта на веб-сайте VoltDB или в исходном формате из репозитория VoltDB на github ( http://github.com/VoltDB/voltdb-client-cpp). В следующих разделах описывается, как писать клиентские приложения VoltDB на C++.
«Интерфейс» JSON для VoltDB на самом деле является веб-интерфейсом, который сервер базы данных VoltDB предоставляет для обработки запросов и возврата данных в формате JSON. Интерфейс JSON позволяет вызывать хранимые процедуры VoltDB и получать их результаты через HTTP-запросы. Чтобы вызвать хранимую процедуру, вы передаете VoltDB имя и параметры процедуры в виде строки запроса к HTTP-запросу, используя метод GET или POST. Хотя многие языки программирования предоставляют методы для упрощения кодирования и декодирования строк JSON, вам все равно необходимо понимать создаваемые структуры данных. 
JDBC (Java Database Connectivity) — это программный интерфейс для Java-программистов, который абстрагирует особенности базы данных от методов, используемых для доступа к данным. JDBC предоставляет стандартные методы и классы для доступа к реляционной базе данных, а поставщики затем предоставляют драйверы JDBC для реализации абстрактных методов в своем конкретном программном обеспечении. VoltDB предоставляет драйвер JDBC для тех, кто предпочитает использовать JDBC в качестве интерфейса доступа к данным. Драйвер VoltDB JDBC поддерживает специальные запросы, подготовленные операторы, вызов хранимых процедур и методы проверки метаданных, описывающих схему базы данных.


Какой database engine используется в СУБД?


VoltDB использует механизм реляционной базы данных в памяти. 
VoltDB использует архитектуру без общего доступа. Для достижения параллелизма базы данных данные и связанная с ними обработка (в виде однопоточного исполняющего «движка» VoltDB) распределяются между всеми ядрами ЦП на серверах, составляющих единый кластер VoltDB. Расширяя
его основа без общего доступа к уровню каждого ядра («виртуальные узлы»), VoltDB использует и масштабируется с помощью увеличение количества ядер на процессор на современных массовых серверах. Эта архитектура также позволяет VoltDB для простой работы в виртуализированных и облачных инфраструктурах.
В VoltDB каждый раздел хранится в основной памяти и обрабатывается связанным с ним однопоточным executive engine на скорости в памяти. Обработка в памяти устраняет ожидание диска изнутри
Транзакции VoltDB, а также потребность в накладных расходах на управление буфером


Как устроен язык запросов в вашей СУБД? Разверните БД с данными и выполните запрос.


Все участники VoltDB общаются с помощью SQL, и данные могут быть загружены в базу данных с помощью различных методов, таких как CSV-файлы или Java-программы.


Возможно ли распределение файлов БД по разным носителям?


Да, VoltDB позволяет выполнять сегментирование базы данных на разных машинах и узлах для повышения производительности и масштабируемости.
Массивно-параллельная архитектура VoltDB обеспечивает гибкую масштабируемость, работающую на недорогих обычных серверах. Это позволяет разработчикам приложений масштабировать приложения, просто добавляя серверы в кластер VoltDB вместо создания сложных, дорогостоящие слои шардинга. Соответствие VoltDB требованиям ACID гарантирует, что разработчикам никогда не придется жертвовать  согласованностью данных, чтобы получить высокую производительность и масштабируемость.
Масштабирование не требует никаких изменений в схеме базы данных или коде приложения, а также не требует замены существующих аппаратное обеспечение. Как правило, чем больше вычислительных ядер (и, следовательно, больше разделов) в кластере, тем больше транзакций VoltDB выполняет в секунду, обеспечивая простой линейный путь для соответствие широкому спектру требований к емкости и производительности


На каком языке написана СУБД.


Система написана на Java; SQL-запросы в системе компилируются в форму хранимых процедур на Java.
Какие типы индексов поддерживаются в БД? Приведите пример создания индексов.
VoltDB использует древовидные индексы (tree indexes). Они обеспечивают наилучшую общую производительность для широкого спектра операций, включая точное совпадение значений и запросы, включающие диапазон значений, таких как


В следующем примере создаются два индекса в одной таблице. Первый, по умолчанию, является неуникальным индексом, основанным на времени вылета, второй - уникальным индексом, основанным на столбцах для авиакомпании и номера рейса.

Также можно использовать функции в определении (definition) индекса. Например, ниже приведен индекс, основанный на элементе movie в столбце VARCHAR в JSON-кодировке с именем favorites и идентификатором участника.

Следующий пример демонстрирует использование частичного индекса путем включения предложения WHERE для исключения записей с нулевым столбцом.


Как строится процесс выполнения запросов в вашей СУБД?


Создание БД в VoldDB:
1. создание схемы (логическая структура БД);
2. компиляция каталога;
3. старт БД. 
В VoltDB сначала определяется схема, а потом запускается БД. Конечно потом можно изменить схему, но сперва 
нужно определить начальную схему для инициализации.

Для определения схемы используется стандартный SQL:
CREATE TABLE
CREATE INDEX
CREATE VIEW
VoltDB поддерживает 9 типов данных столбцов.
DDL в VoltDB поддерживает объявление хранимых процедур и фрагментацию таблиц и процедур (partitioning tables and procedures).

После того как схема определена, можно создавать application catalog:

$ voltdb compile myschema.sql
Для старта VoltDB нужно два файла:
 application catalog указывает логическую структуру БД;
 deployment файл указывает физическое размещение БД и специальные возможности и настройки..
Запуск VoltDB производится следующей командой:

$ voltdb create catalog catalog.jar
Взаимодействовать с запущенной БД можно посредством обычных SQL команд (SELECT, DELETE и др.).


Есть ли для вашей СУБД понятие “план запросов”? Если да, объясните, как работает данный этап.


В случае VoltDB команды конечного пользователя представляют собой планы выполнения специальных операторов SQL, выполнение планы распределенных фрагментов SQL (подробнее об этом чуть позже) и вызовов хранимых процедур. Мы ссылайтесь на цикл, который обслуживает очередь команд как на раздел.
Второй источник детерминизма, который необходимо контролировать, — это недетерминированный SQL. Это относительно редко (как правило, бизнес-логика не имеет смысла делать что-то случайное с вашими данными). Пример недетерминированного SQL выбирает две случайные строки из таблицы, например, SELECT * FROM T LIMIT 2; Просто такой запрос не приведет к расхождению реплик; однако, если следующее действие в сохраненном процедура удаления возвращаемых строк, реплики больше не будут точными копиями. VoltDB SQL планировщик идентифицирует недетерминированные операторы и предупреждает о них.

Для выполнения операторов SQL, требующих данных из нескольких разделов, планировщик SQL VoltDB разделяет планы выполнения на фрагменты. Некоторые фрагменты распределены по кластеру и выполняются на нескольких перегородки. Другие фрагменты работают с собранными результатами распределенных фрагментов.


Поддерживаются ли транзакции в вашей СУБД? Если да, то расскажите о нем. Если нет, то существует ли альтернатива?


VoltDB поддерживает большинство операторов SQL, и поддержка SQL все еще добавляется. И один оператор SQL, и хранимая процедура VoltDB поддерживают все свойства ACID транзакции, и это полная система, поддерживающая обработку транзакций. Это сильно отличается от систем «ключ-значение».
VoltDB также поддерживает JDBC, ODBC и другие интерфейсы.
СУБД VoltDB поддерживает горизонтальное масштабирование и ориентирована на обработку транзакций в реальном времени (OLTP). На недорогом кластере, собранном своими силами из обычных серверов, СУБД способна обрабатывать миллионы транзакций в секунду. VoltDB позволяет достичь уровня производительности NoSQL-систем, сохранив при этом поддержку выполнения запросов на языке SQL и гарантированную транзакционную целостность данных (ACID, атомарность и изолированность транзакций).


Какие методы восстановления поддерживаются в вашей СУБД. Расскажите о них.


Если во время выполнения хранимой процедуры возникает проблема, ожидаемая или непредвиденная, важно, чтобы транзакция откатилась. Откат означает, что любые изменения, сделанные во время транзакции, отменяются, и база данных остается в том же состоянии, в котором она была до начала транзакции.
VoltDB — это полностью транзакционная база данных, что означает, что в случае сбоя транзакции (хранимой процедуры) транзакция автоматически откатывается, и вызывающему приложению возвращается соответствующее исключение. Исключения, которые могут вызвать откат, включают следующее:
Ошибки времени выполнения в коде хранимой процедуры, такие как деление на ноль или переполнение типа данных.
Нарушение ограничений базы данных в SQL-запросах, например вставка повторяющегося значения в столбец, определенный как уникальный.
Атомарность хранимой процедуры зависит от способности VoltDB откатывать незавершенные изменения базы данных. VoltDB полагается на обработку исключений Java вне хранимой процедуры для выполнения отката. Поэтому не следует пытаться изменить какие-либо исключения, создаваемые методом voltExecuteSql. Если код вашей процедуры перехватывает исключения, возникающие в результате выполнения операторов SQL, убедитесь, что обработчик исключений повторно создает исключение, чтобы позволить VoltDB выполнить необходимые действия по откату до того, как хранимая процедура вернется в вызывающую программу.
С другой стороны, могут быть ситуации, когда в логике программы возникает исключение. Проблема может быть не связана с Java или VoltDB, но по-прежнему не существует практического способа завершения логики транзакции. В этих ситуациях вы можете принудительно выполнить откат, явно вызвав VoltA bort Exception исключение.


Расскажите про шардинг в вашей конкретной СУБД. Какие типы используются? Принцип работы.


Одной из наиболее важных функций VoltDB является секционирование.
Разделение организует содержимое таблицы базы данных в отдельные автономные единицы. Подобно сегментированию, секционирование VoltDB уникально, потому что:
VoltDB автоматически разделяет таблицы базы данных на основе указанного вами столбца разделения. Вам не нужно вручную управлять разделами.
На одном сервере может быть несколько разделов или сайтов. Другими словами, секционирование предназначено не только для масштабирования объема данных, но и для повышения производительности.
VoltDB разделяет как данные, так и обработку, которая обращается к этим данным, и именно так VoltDB использует улучшения пропускной способности, обеспечиваемые параллелизмом.
Внедрение схемы разделения данных или «сегментирования» — ручное разделение базы данных на множество небольших баз данных, работающих на разных серверах и изменяющих код приложения для координации доступа к данным между разделами

Шардинг в VoltDB включает в себя разделение базы данных на разделы и репликацию этих разделов на разных машинах. Это обеспечивает горизонтальное масштабирование и повышает производительность.

Возможно ли применить термины Data Mining, Data Warehousing и OLAP в вашей СУБД?
Чтобы помочь предприятиям, которым требуется как исключительная производительность транзакций, так и специальная отчетность, VoltDB включает функции интеграции, позволяющие экспортировать исторические данные в аналитическую базу данных для более масштабного Data Mining .
VoltDB включает подсистему интеграции экспорта, которая преобразует данные VoltDB в аналитические продукты СУБД (такие как хранилища столбчатых данных и Hadoop) для обеспечения глубокой отчетности и анализа с помощью этих инструментов.
Какие методы защиты поддерживаются вашей СУБД? Шифрование трафика, модели авторизации и т.п.
Когда приложение создает соединение с базой данных VoltDB (используя ClientFactory.clientCreate), оно передает имя пользователя и пароль как часть конфигурации клиента. Эти параметры идентифицируют клиента в базе данных и используются для аутентификации доступа. VoltDB использует хэширование, а не шифрование при передаче имени пользователя и пароля между клиентом и сервером. Клиенты Java и C++ используют хэширование SHA-2, в то время как более старые клиенты в настоящее время используют SHA-1. Пароли также хешируются в базе данных. Чтобы защитить фактическую связь между сервером и клиентом, вы можете реализовать безопасность транспортного уровня (TLS) или безопасность Kerberos.
Во время выполнения, если безопасность включена, имя пользователя и пароль, переданные клиентским приложением, проверяются сервером на соответствие пользователям, определенным в файле конфигурации. Если клиентское приложение передает допустимую пару имени пользователя и пароля для учетной записи, срок действия которой еще не истек, соединение устанавливается. Когда приложение вызывает хранимую процедуру, разрешения проверяются снова. Если схема определяет, что пользователю назначена роль, имеющая доступ к этой хранимой процедуре, процедура выполняется. В противном случае вызывающему приложению возвращается ошибка.
Чтобы включить безопасность для приложения VoltDB, нужно выполнить три шага:
Добавьте <security enabled="true"/>тег в файл конфигурации, чтобы включить аутентификацию и авторизацию.
Определите пользователей и роли, которые необходимо аутентифицировать.
Определите, какие роли имеют доступ к каждой хранимой процедуре.
По умолчанию VoltDB не выполняет аутентификацию, и клиентские приложения имеют полный доступ к базе данных. Чтобы включить аутентификацию, добавьте тег <security> в файл конфигурации. Можно включить безопасность при инициализации корневого каталога базы данных, или вы можете использовать обновление voltadmin для изменения параметра безопасности в работающей базе данных. (Или изменить настройку в интерактивном режиме через Центр управления Volt.)
Ключом к безопасности приложений VoltDB являются пользователи и роли, определенные в схеме и конфигурации. Вы определяете пользователей в файле конфигурации и роли в схеме.
Это разделение является преднамеренным, потому что оно позволяет вам определить общую структуру безопасности глобально в схеме, назначая разрешения общим ролям (таким как оператор, dbuser, приложения и т. д.). Затем определяются конкретные пользователи и им назначаются общие роли как часть конфигурации базы данных. Таким образом, вы можете создать одну конфигурацию (включая информацию о кластере и пользователях) для разработки и тестирования, а затем переместить базу данных в другую конфигурацию и другой набор пользователей для производства, изменив только один файл: файл конфигурации.
Вы определяете пользователей в теге <users> ... </users>, установленном в файле конфигурации.
<deployment>
   <users>
      <user name="user-name" 
            password="password-string"
            roles="role-name[,...]"
            [ expires="expiration-date" ]
      />
        [ ... ]
   </users>
   ...
</deployment>
VoltDB хэширует имена пользователей и пароли как на сервере базы данных, так и при передаче их по сети. Однако сама сетевая связь по умолчанию не шифруется. Вы можете включить Transport Layer Security (TLS) — рекомендуемое обновление связи Secure Socket Layer (SSL) — для HTTP-порта, который влияет на Volt Management Center и интерфейс JSON. Вы также можете распространить шифрование TLS на все внешние интерфейсы (HTTP, клиентский и административный), внутренний интерфейс и порт, используемый для репликации базы данных (DR), для большей безопасности. В следующих разделах описано, как включить TLS для серверов в кластере, в том числе:
Настройка шифрования TLS на сервере
Выбор портов для шифрования
Использование утилит командной строки VoltDB с TLS
Реализация связи TLS в клиентских приложениях Java
Настройка репликации базы данных (DR) с использованием TLS.
  

Какие сообщества развивают данную СУБД? Кто в проекте имеет права на коммит и создание дистрибутива версий? 


Расскажите об этих людях и/или компаниях.
VoltDB разработан VoltDB Inc. и имеет активное сообщество пользователей. Руководители и участники проекта перечислены на сайте VoltDB. 


Создайте свои собственные данные для демонстрации работы СУБД.


Как продолжить самостоятельное изучение языка запросов с помощью демобазы. Если демобазы нет, то создайте ее.
Примером создания данных в VoltDB может быть написание программы на Java для создания и загрузки данных в таблицу. Затем данные могут быть запрошены с помощью команд SQL.
https://github.com/VoltDB/voltdb


Где найти документацию и пройти обучение.


https://docs.voltactivedata.com/ - официальная страница VoltDB с документацией и туториалами
https://docs.voltdb.com/UsingVoltDB/ - руководство по использованию
VoltDB имеет версию с открытым исходным кодом и бесплатную пробную версию. Существует также коммерческая версия, которая содержит больше функций. Чтобы загрузить, вам необходимо перейти на официальный сайт, чтобы загрузить его самостоятельно. Например, для восстановления данных, ведения журнала команд и других функций требуется коммерческая версия. Для коммерческой версии предоставляется 30-дневная бесплатная пробная версия. Бесплатная версия распространяется под лицензией GNU Affero General Public License. Дополнительные возможности коммерческой версии VoltDB Enterprise включают в себя высокую доступность и поддержку экспорта данных.


Как быть в курсе происходящего.


Веб-сайт VoltDB и учетные записи в социальных сетях являются хорошими источниками новостей и обновлений. VoltDB также поддерживает форум сообщества для обсуждения и поддержки.
