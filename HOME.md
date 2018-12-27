# База знаний разработчика

## Разработка

+ Кодирование
    * [Именование](https://ru.hexlet.io/blog/posts/naming-in-programming)
    * [Форматирование](https://habr.com/company/geekbrains/blog/270001)
    * [Комментарии](https://habr.com/post/178653)
    * [Операторы](https://ru.wikipedia.org/wiki/Оператор_(программирование))
    * [Методы](https://ru.wikipedia.org/wiki/Метод_(программирование))
    * [Классы](https://ru.wikipedia.org/wiki/Класс_(программирование))
    * [Обработка ошибок](https://ru.wikipedia.org/wiki/Обработка_исключений)
    * [Многопоточность](https://ru.wikipedia.org/wiki/Многопоточность)
    
+ Проектирование
    * [Архитектура](https://ru.wikipedia.org/wiki/Архитектура_программного_обеспечения)
    * [Тестирование](https://habr.com/post/279535)
    * [Отладка](https://ru.wikipedia.org/wiki/Отладка_программы)
    * [Рефакторинг](https://refactoring.guru/ru)
    * [Профилирование](https://ru.wikipedia.org/wiki/Профилирование_(информатика))
    * [Оптимизация](https://ru.wikipedia.org/wiki/Оптимизация_(информатика))
    * [Интеграция](https://habr.com/company/trinion/blog/245615)

---

## Структуры и алгоритмы обработки данных

+ Структуры данных
    * [Массив (Array)](https://ru.wikipedia.org/wiki/Массив_(программирование))
    * [Список (List)](https://ru.wikipedia.org/wiki/Список_(информатика))
    * [Стек (Stack)](https://ru.wikipedia.org/wiki/Стек)
    * [Очередь (Queue)](https://ru.wikipedia.org/wiki/Очередь_(программирование))
    * [Граф (Graph)](https://ru.wikipedia.org/wiki/Объектный_граф)
    * [Дерево (Tree)](https://ru.wikipedia.org/wiki/Дерево_(структура_данных))
    * [Хеш-таблица (Hash map)](https://ru.wikipedia.org/wiki/Хеш-таблица)

+ Алгоритмы обработки данных
    * [Сортировки](https://ru.wikipedia.org/wiki/Алгоритм_сортировки)
        * Устойчивые
            * [Сортировка пузырьком (Bubble sort) - O(n^2)](https://ru.wikipedia.org/wiki/Сортировка_пузырьком)
            * [Сортировка вставками (Insertion sort) - O(n^2)](https://ru.wikipedia.org/wiki/Сортировка_вставками)
            * [Сортировка слиянием (Merge sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Сортировка_слиянием)
            * [Сортировка с помощью двоичного дерева (Tree sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Сортировка_с_помощью_двоичного_дерева)
            * [Сортировка Timsort - O(n*log(n))](https://ru.wikipedia.org/wiki/Timsort)
            * [Блочная сортировка (Bucket sort) - O(n)](https://ru.wikipedia.org/wiki/Блочная_сортировка)
        * Неустойчивые
            * [Сортировка выбором (Selection sort) - O(n^2)](https://ru.wikipedia.org/wiki/Сортировка_выбором)
            * [Сортировка Шелла (Shell sort) - O(n*log2(n))](https://ru.wikipedia.org/wiki/Сортировка_Шелла)
            * [Пирамидальная сортировка (Heap sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Пирамидальная_сортировка)
            * [Плавная сортировка (Smooth sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Плавная_сортировка)
            * [Быстрая сортировка, сортировка Хоара (Quick sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Быстрая_сортировка)

+ [Сложность алгоритмов](https://ru.wikipedia.org/wiki/Временная_сложность_алгоритма)
    * O(1) - константная
    * O(n) — линейная
    * O(log(n) — логарифмическая
    * O(n*log(n)) - линеарифметический
    * O(n^2) — квадратичная

+ Дополнительно
    * [AlgoList - алгоритмы и методы](http://algolist.manual.ru)
    * [VisuAlgo - визуализации структур данных и алгоритмов](https://visualgo.net/ru)
    * [Know Thy Complexities! - сложности основных структур данных и алгоритмов](http://bigocheatsheet.com)

+ Литература
    * [Алгоритмы. Построение и анализ - Томас Х. Кормен, Чарльз И. Лейзерсон, Рональд Л. Ривест, Клиффорд Штайн](https://www.ozon.ru/context/detail/id/33769775)
    * [Абстракция данных и решение задач на С++. Стены и зеркала - Фрэнк М. Каррано, Джанет Дж. Причард](http://www.ozon.ru/context/detail/id/1435484)    
    * [Алгоритмы на C++ - Роберт Седжвик](http://www.ozon.ru/context/detail/id/31924296)
    * [Алгоритмы на Java - Роберт Седжвик, Кевин Уэйн](https://www.ozon.ru/context/detail/id/18319699)
    * [Структуры данных и алгоритмы в Java - Роберт Лафоре](https://www.ozon.ru/context/detail/id/23529814)
    * [Грокаем алгоритмы. Иллюстрированное пособие для программистов и любопытствующих - Адитья Бхаргава](https://www.ozon.ru/context/detail/id/139296295)

+ Видео
    * [Алгоритмы и структуры данных на Python 3 - Тимофей Хирьянов](https://www.youtube.com/playlist?list=PLRDzFCPr95fK7tr47883DFUbm4GeOjjc0)

---

## Паттерны

+ [Общие паттерны распределения обязанностей (General Responsibility Assignment Software Patterns, GRASP)](https://ru.wikipedia.org/wiki/GRASP)
    * Порождающие (Creational)
        * Создатель экземпляров класса (Creator)
    * Структурные (Structural)
        * Информационный эксперт (Information Expert)
        * Низкая связанность (Low Coupling)
        * Устойчивый к изменениям (Protected Variations)
    * Поведенческие (Behavioral)
        * Не разговаривайте с неизвестными (Don't talk to strangers)
        * Высокое зацепление (High Cohesion)
        * Контроллер (Controller)
        * Полиморфизм (Polymorphism)
        * Искусственный (Pure Fabrication)
        * Перенаправление (Indirection)

+ [Базовые паттерны проектирования (Gang of Four)](https://ru.wikipedia.org/wiki/Шаблон_проектирования)
    * Порождающие (Creational)
        * [Абстрактная фабрика (Abstract factory) или Инструментарий (Kit)](/design_patterns/creational/abstract_factory.md)
        * [Строитель (Builder)](/design_patterns/creational/builder.md)
        * [Фабричный метод (Factory Method) или Виртуальный конструктор (Virtual Constructor)](/design_patterns/creational/factory_method.md)
        * [Прототип (Prototype)](/design_patterns/creational/prototype.md)
        * [Одиночка (Singleton)](/design_patterns/creational/singleton.md)
    * Структурные (Structural)
        * [Адаптер (Adapter)](/design_patterns/structural/adapter.md)
        * [Мост (Bridge) или Описатель (Handle) / Тело (Body)](/design_patterns/structural/bridge.md)
        * [Компоновщик (Composite)](/design_patterns/structural/composite.md)
        * [Декоратор (Decorator) или Оболочка (Wrapper)](/design_patterns/structural/decorator.md)
        * [Фасад (Facade)](/design_patterns/structural/facade.md)
        * [Приспособленец (Flyweight)](/design_patterns/structural/flyweight.md)
        * [Заместитель (Proxy) или Суррогат (Surrogate)](/design_patterns/structural/proxy.md)
    * Поведенческие (Behavioral)
        * [Цепочка обязанностей (Chain of responsibility)](/design_patterns/behavioral/chain_of_responsibility.md)
        * [Команда (Command), Действие (Action) или Транзакция (Transaction)](/design_patterns/behavioral/command.md)
        * [Интерпретатор (Interpreter)](/design_patterns/behavioral/interpreter.md)
        * [Итератор (Iterator) или Курсор (Cursor)](/design_patterns/behavioral/iterator.md)
        * [Посредник (Mediator)](/design_patterns/behavioral/mediator.md)
        * [Хранитель (Memento)](/design_patterns/behavioral/momento.md)
        * [Наблюдатель (Observer), Опубликовать / подписаться (Publish - Subscribe) или Delegation Event Model](/design_patterns/behavioral/observer.md)
        * [Состояние (State)](/design_patterns/behavioral/state.md)
        * [Стратегия (Strategy)](/design_patterns/behavioral/strategy.md)
        * [Шаблонный метод (Template method)](/design_patterns/behavioral/template_method.md)
        * [Посетитель (Visitor)](/design_patterns/behavioral/visitor.md)

+ [Паттерны представления](https://manojjaggavarapu.wordpress.com/2012/05/02/presentation-patterns-mvc-mvp-pm-mvvm)
    * [Model-View-Controller (MVC)](https://ru.wikipedia.org/wiki/Model-View-Controller)
    * [Model-View-Presenter (MVP)](https://ru.wikipedia.org/wiki/Model-View-Presenter)
    * [Model-View-ViewModel (MVVM)](https://ru.wikipedia.org/wiki/Model-View-ViewModel)
    * [Presentation-Model (PM)](https://martinfowler.com/eaaDev/PresentationModel.html)
    * [MobX](https://mobx.js.org)
    * [Flux](http://fluxxor.com/what-is-flux.html)
    * [Redux](https://redux.js.org)
    * [VIPER for iOS Apps](https://www.objc.io/issues/13-architecture/viper)

+ [Архитектурные системные паттерны](https://en.wikipedia.org/wiki/Architectural_pattern)
    * Системные паттерны
        * [Сервисно-ориентированная архитектура (SOA)](https://ru.wikipedia.org/wiki/Сервис-ориентированная_архитектура)
        * Вертикальное масштабирование (Vertical scaling)
        * Горизонтальное масштабирование (Horizontal scaling)
        * Отложенные вычисления (Deferred calculations)
        * Асинхронная обработка (Asynchronous processing)
        * Конвейерная обработка (Pipeline processing)
        * Кэширование (Caching)
        * Функциональное разделение (Functional separation)
        * Шардинг (Sharding)
        * Виртуальные шарды (Virtual shards)
        * Центральный диспетчер (Central dispatcher)
        * Репликация (Replication)
        * Партиционирование (Partitioning)
        * Кластеризация (Clustering)
        * Денормализация (Denormalization)
        * Избыточность (Redundancy)
        * Параллельное выполнение (Parallel execution)
    * Структурные паттерны
        * Репозиторий (Repository)
        * Клиент/сервер (Client/server)
        * Модель предметной области (Domain model) 
        * Модуль таблицы (Data mapper)
        * Многоуровневая система или абстрактная машина (Layers)
        * Потоки данных (конвейер или фильтр)
    * Паттерны управления
        * Паттерны централизованного управления
            * Вызов - возврат
            * Диспетчер (Dispatcher)
        * Паттерны управления, основанные на событиях
            * Передача сообщений (Messaging)
            * Управляемый прерываниями (Interrupt driven)
        * Паттерны, обеспечивающие взаимодействие с базой данных
            * Активная запись (Active record)
            * Единица работы (Unit of work)
            * Загрузка по требованию (Lazy load)
            * Коллекция объектов (Identity map)
            * Множество записей (Record set)
            * Наследование с одной таблицей (Single table inheritance)
            * Наследование с таблицами для каждого класса (Class table inheritance)
            * Оптимистическая автономная блокировка (Optimistic offline lock)
            * Отображение с помощью внешних ключей (Foreign key mapping)
            * Отображение с помощью таблицы ассоциаций (Association table mapping)
            * Пессимистическая автономная блокировка (Pessimistic offline lock)
            * Поле идентификации (Identity field)
            * Преобразователь данных (Data mapper)
            * Сохранение сеанса на стороне клиента (Client session state)
            * Сохранение сеанса на стороне сервера (Server session state)
            * Шлюз записи данных (Row data gateway)
            * Шлюз таблицы данных (Table data gateway)

+ [Java паттерны](https://java-design-patterns.com/patterns)

+ [J2EE паттерны](https://ru.wikipedia.org/wiki/Шаблоны_J2EE)

+ [Паттерны игрового программирования](http://gameprogrammingpatterns.com)

+ Дополнительно
    * [Обзор паттернов проектирования - Ольга Дубина](http://citforum.ru/SE/project/pattern)

+ Литература
    * [Паттерны проектирования - "Банда четырех" (Gang of Four, GoF)](http://www.ozon.ru/context/detail/id/2457392)
    * [Паттерны проектирования - Элизабет Фримен, Эрик Фримен, Кэти Сиерра, Берт Бейтс](https://www.ozon.ru/context/detail/id/20216992)
    * [Шаблоны корпоративных приложений - Мартин Фаулер, Дейвид Райс](http://www.ozon.ru/context/detail/id/4884925)
    * [Рефакторинг с использованием шаблонов - Джошуа Кериевски](http://www.ozon.ru/context/detail/id/2909721)

---

## Парадигмы, принципы, стандарты

+ [Парадигмы программирования](https://ru.wikipedia.org/wiki/Парадигма_программирования)
    * [Императивная](https://ru.wikipedia.org/wiki/Императивное_программирование)
        * [Процедурная](https://ru.wikipedia.org/wiki/Процедурное_программирование)
        * [Аспектно-ориентированная](https://ru.wikipedia.org/wiki/Аспектно-ориентированное_программирование)
        * [Объектно-ориентированная](https://ru.wikipedia.org/wiki/ориентированное_программирование)
            * [Абстракция](https://ru.wikipedia.org/wiki/Абстракция_данных)
            * [Инкапсуляция](https://ru.wikipedia.org/wiki/Инкапсуляция_(программирование))
            * [Наследование](https://ru.wikipedia.org/wiki/Наследование_(программирование))
            * [Полиморфизм](https://ru.wikipedia.org/wiki/Полиморфизм_(информатика))
    * [Декларативная](https://ru.wikipedia.org/wiki/Декларативное_программирование)
        * [Функциональная](https://ru.wikipedia.org/wiki/Функциональное_программирование)

+ [Принципы](http://java-design-patterns.com/principles/)
    * [SOLID - 5 основных принципов ООП](https://ru.wikipedia.org/wiki/SOLID_(объектно-ориентированное_программирование))
        * [SRP - Принцип единственной ответственности](https://ru.wikipedia.org/wiki/Принцип_единственной_обязанности)
        * [OCP - Принцип открытости/закрытости](https://ru.wikipedia.org/wiki/Принцип_открытости/закрытости)
        * [LSP - Принцип подстановки Барбары Лисков](https://ru.wikipedia.org/wiki/Принцип_подстановки_Барбары_Лисков)
        * [ISP - Принцип разделения интерфейса](https://ru.wikipedia.org/wiki/Принцип_разделения_интерфейса)
        * [DIP - Принцип инверсии зависимостей](https://ru.wikipedia.org/wiki/Принцип_инверсии_зависимостей)
    * Low in [coupling](https://en.wikipedia.org/wiki/Coupling_(computer_programming)) and high in [cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)) - низкая связанность и высокая связность
    * [DRY - Принцип "Не повторяйся"](https://ru.wikipedia.org/wiki/Don%E2%80%99t_repeat_yourself)
    * [KISS - Принцип "Делай проще, дурачок"](https://ru.wikipedia.org/wiki/KISS_(принцип))
    * [YAGNI - Принцип «Тебе это не понадобится»](https://ru.wikipedia.org/wiki/YAGNI)
    * [Принцип «Подделай, пока не сделаешь» (при разработке через тестирование)](https://ru.wikipedia.org/wiki/Fake_it_till_you_make_it)
    * [WYSIWYG - Принцип «Что видишь, то и получишь»](https://ru.wikipedia.org/wiki/WYSIWYG)
    * [LoD - Закон Деметры](https://ru.wikipedia.org/wiki/Закон_Деметры)
    * [Правило бойскаута (из "Чистого кода" Роберта Мартина)](http://programmer.97things.oreilly.com/wiki/index.php/The_Boy_Scout_Rule)
    * [Правило одной операции (из "Чистого кода" Роберта Мартина)](https://en.wikipedia.org/wiki/Single_responsibility_principle)

+ Стандарты
    * [Coding Style Conventions and Standards](https://github.com/SalGnt/cscs)
    * [Венгерская нотация](https://ru.wikipedia.org/wiki/Венгерская_нотация)

+ Методики
    * [UML - Унифицированный язык моделирования](https://ru.wikipedia.org/wiki/UML)
    * [TDD - Разработка через тестирование](https://ru.wikipedia.org/wiki/Разработка_через_тестирование)
    * [BDD - Разработка через поведение](https://ru.wikipedia.org/wiki/BDD_(программирование))

+ Другое
    * [Code smell - "дурно пахнущий" код](https://ru.wikipedia.org/wiki/Код_с_запашком)
    * [CRUD - «создать, прочесть, обновить, удалить»](https://ru.wikipedia.org/wiki/CRUD)
    * [F.I.R.S.T. - 5 характеристик тестов](https://pragprog.com/magazines/2012-01/unit-tests-are-first)

+ Литература
    * [Совершенный код - Стив Макконнелл](http://www.ozon.ru/context/detail/id/5508646)
    * [Чистый код: создание, анализ и рефакторинг - Роберт К. Мартин](http://www.ozon.ru/context/detail/id/5011068)
    * [Чистая архитектура. Искусство разработки программного обеспечения - Роберт Мартин](https://www.ozon.ru/context/detail/id/144499396)
    * [Идеальный программист. Как стать профессионалом разработки ПО - 	Роберт Мартин](https://www.ozon.ru/context/detail/id/135465064)
    * [Разработка требования к программному обеспечению - Карл И. Вигерс, Джой Битти](https://www.ozon.ru/context/detail/id/27995134)
    * [Идеальная разработка ПО. Рецепты лучших программистов - Энди Орам, Грег Уилсон](https://www.ozon.ru/context/detail/id/7248898)

---

## Технологии

+ Платформы
    * .NET
        * Языки
            * C#
            * F#
        * Платформы
            * .NET Framework
            * .NET Core
        * Фреймворки, библиотеки
            * WinForms
            * WPF
            * UWP
            * Xamarin
        * Литература
            * [CLR via C#. Программирование на платформе Microsoft.NET Framework 4.5 на языке C# - Джеффри Рихтер](https://www.ozon.ru/context/detail/id/21236101)
            * [Язык программирования C# 5.0 и платформа .NET 4.5 - Эндрю Троелсен](http://www.ozon.ru/context/detail/id/19916784)
            * [WPF: Windows Presentation Foundation в .NET 4.5 с примерами на C# 5.0 для профессионалов - Мэтью Макдональд](https://www.ozon.ru/context/detail/id/21462174)
    * JDK
        * Языки
            * Java
            * Groovy
            * Kotlin
            * Scala
        * Платформы
            * Java SE
            * Java EE
            * Java ME
        * Фреймворки, библиотеки
            * Spring
            * Spring Boot
            * Spring Cloud
            * Netty
        * Литература
            * [Философия Java - Брюс Эккель](https://www.ozon.ru/context/detail/id/30425811)
            * [Java. Эффективное программирование - Джошуа Блох](https://www.ozon.ru/context/detail/id/1259354)
            * [Java Concurrency in Practice - Дуг Ли, Брайан Готц, Тим Пайерлс, Джошуа Блох, Джозеф Боубир, Дэвид Холмс](http://www.ozon.ru/context/detail/id/3174887)

+ Хранилища данных
    * SQL
        * [SQLite](https://www.sqlite.org)
        * [MySQL](https://www.mysql.com)
        * [PostgreSQL](https://www.postgresql.org)
            * [Документация от Postgres Professional](https://postgrespro.ru)
            * [Работа с PostgreSQL: настройка и масштабирование](http://postgresql.leopard.in.ua)
            * [Администрирование PostgreSQL 9. Книга рецептов - Саймон Ригс, Ханну Кросинг](https://www.ozon.ru/context/detail/id/19133383)
    * NoSQL
        * [Memcached](https://memcached.org)
        * [Redis](https://redis.io)
        * [MongoDB](https://www.mongodb.com)

+ Очереди и брокеры сообщений
    * [RabbitMQ](https://www.rabbitmq.com)
    * [Kafka](https://kafka.apache.org)

+ Управление кластером
    * [Docker Swarm](https://docs.docker.com/engine/swarm)
    * [Kubernetes](https://kubernetes.io)
    * [Marathon](https://mesosphere.github.io/marathon)
    * [Mesos](http://mesos.apache.org)

+ Метрики и логирование
    * [Elasticsearch + Logstash + Kibana (ELK)](https://www.elastic.co/elk-stack)
    * [Prometheus](https://prometheus.io)
    * [Grafana](https://grafana.com)

+ Непрерывная интеграции и доставка (CI/CD)
    * [Jenkins](https://jenkins.io)
    * [Travis](https://travis-ci.org)

+ API документация
    * [Swagger](https://swagger.io)
    * [AsciiDoc](http://asciidoc.org)

+ Системы управления версиями
    * [Git](https://git-scm.com)
        * [Git для профессионального программиста - Скотт Чакон, Бен Штрауб](http://www.ozon.ru/context/detail/id/33575056)
    * [Mercurial](https://www.mercurial-scm.org)

+ Системы управления репозиториями
    * [GitHub](https://github.com)
    * [BitBucket](https://bitbucket.org)
    * [GitLab](https://gitlab.com)

+ Системы управления проектами
    * [RedMine](https://www.redmine.org)
    * [Jira](https://ru.atlassian.com/software/jira)

+ Средства сборки проектов и управления зависимостями
    * [Make](https://www.gnu.org/software/make)
    * [Ant](https://ant.apache.org)
    * [Maven](https://maven.apache.org)
    * [Gradle](https://gradle.org)
    * [NuGet](https://www.nuget.org)

+ Бинарные репозитории и хранилища артефактов
    * [Nexus](https://www.sonatype.com/nexus-repository-sonatype)
    * [Artifactory](https://jfrog.com/artifactory)
    
+ Анализаторы кода
    * [PVS-Studio](https://www.viva64.com/ru/pvs-studio)
    * [SonarQube](https://www.sonarqube.org)
    * [Gradle quality plugin](http://xvik.github.io/gradle-quality-plugin)
    
+ Виртуализация и контейнеризация
    * [VirtualBox](https://www.virtualbox.org)
    * [VMWare](https://www.vmware.com/ru.html)
    * [Docker](https://www.docker.com)
    
