## База знаний разработчика

### Разработка

+ Кодирование
    * [Именование](/development/coding/naming.md)
    * [Форматирование](/development/coding/formatting.md)
    * [Комментарии](/development/coding/comments.md)
    * [Операторы](/development/coding/operators.md)
    * [Методы](/development/coding/methods.md)
    * [Классы](/development/coding/classes.md)
    * [Обработка ошибок](/development/coding/error_handling.md)
    * [Многопоточность](/development/coding/multithreading.md)
+ Проектирование
    * [Архитектура](/development/designing/architecture.md)
    * [Тестирование](/development/designing/testing.md)
    * [Отладка](/development/designing/debugging.md)
    * [Рефакторинг](/development/designing/refactoring.md)
    * [Профилирование](/development/designing/profiling.md)
    * [Оптимизация](/development/designing/optimization.md)
    * [Интеграция](/development/designing/integration.md)

### Структуры и алгоритмы обработки данных

+ Структуры данных
    * [Массив (Array)](https://ru.wikipedia.org/wiki/Массив_(программирование))
    * [Список (List)](https://ru.wikipedia.org/wiki/Список_(информатика))
    * [Стек (Stack)](https://ru.wikipedia.org/wiki/Стек)
    * [Очередь (Queue)](https://ru.wikipedia.org/wiki/Очередь_(программирование))
    * [Граф (Graph)](https://ru.wikipedia.org/wiki/Объектный_граф)
    * [Дерево (Tree)](https://ru.wikipedia.org/wiki/Дерево_(структура_данных))

+ Алгоритмы обработки данных
    * [Сорировки](https://ru.wikipedia.org/wiki/Алгоритм_сортировки)
        * Устройчивые
            * [Сортировка пузырьком (Bubble sort) - O(n^2)](https://ru.wikipedia.org/wiki/Сортировка_пузырьком)
            * [Сортировка перемешиванием (Cocktail sort) - O(n^2)](https://ru.wikipedia.org/wiki/Сортировка_перемешиванием)
            * [Сортировка вставками (Insertion sort) - O(n^2)](https://ru.wikipedia.org/wiki/Сортировка_вставками)
            * [Сортировка слиянием (Merge sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Сортировка_слиянием)
            * [Сортировка бинарным деревом (Tree sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Сортировка_с_помощью_двоичного_дерева)
        * Неустойчивые
            * [Сортировка выбором (Selection sort) - O(n^2)](https://ru.wikipedia.org/wiki/Сортировка_выбором)
            * [Сортировка Шелла (Shell sort) - O(n*log2(n))](https://ru.wikipedia.org/wiki/Сортировка_Шелла)
            * [Пирамидальная сортировка, сортировка кучей (Heap sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Пирамидальная_сортировка)
            * [Плавная сортировка (Smooth sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Плавная_сортировка)
            * [Быстрая сортировка, сортировка Хоара (Quick sort) - O(n*log(n))](https://ru.wikipedia.org/wiki/Быстрая_сортировка)

+ Дополнительно
    * [VisuAlgo - визуализации структур данных и алгоритмов](http://visualgo.net/)

### Паттерны

+ [Базовые паттерны проектирования](https://ru.wikipedia.org/wiki/Шаблон_проектирования)
    * Порождающие (Creational)
        * [Абстрактная фабрика (Abstract factory) или Инструментарий (Kit)](/design_patterns/creational/abstract_factory.md)
        * [Строитель (Builder)](/design_patterns/creational/builder.md)
        * [Фабричный метод (Factory Method) или Виртуальный конструктор (Virtual Constructor)](/design_patterns/creational/factory_method.md)
        * [Прототип (Prototype)](/design_patterns/creational/prototype.md)
        * [Одиночка (Singleton)](/design_patterns/creational/singleton.md)
    * Структурные (Structural)
        * [Адаптер (Adapter)](/design_patterns/structural/adapter.md)
        * [Мост (Bridge), Handle (описатель) или Тело (Body)](/design_patterns/structural/bridge.md)
        * [Компоновщик (Composite)](/design_patterns/structural/composite.md)
        * [Декоратор (Decorator) или Оболочка (Wrapper)](/design_patterns/structural/decorator.md)
        * [Фасад (Facade)](/design_patterns/structural/facade.md)
        * [Приспособленец (Flyweight)](/design_patterns/structural/flyweight.md)
        * [Заместитель (Proxy) или Суррогат (Surrogate)](/design_patterns/structural/proxy.md)
    * Поведенческие (Behavioral)
        * [Цепочка обязанностей (Chain of responsibility)](/design_patterns/behavioral/chain_of_responsibility.md)
        * [Команда (Command), Действие (Action) или Транзакция (Транзакция)](/design_patterns/behavioral/command.md)
        * [Интерпретатор (Interpreter)](/design_patterns/behavioral/interpreter.md)
        * [Итератор (Iterator) или Курсор (Cursor)](/design_patterns/behavioral/iterator.md)
        * [Посредник (Mediator)](/design_patterns/behavioral/mediator.md)
        * [Хранитель (Memento)](/design_patterns/behavioral/momento.md)
        * [Наблюдатель (Observer), Опубликовать - подписаться (Publish - Subscribe) или Delegation Event Model](/design_patterns/behavioral/observer.md)
        * [Состояние (State)](/design_patterns/behavioral/state.md)
        * [Стратегия (Strategy)](/design_patterns/behavioral/strategy.md)
        * [Шаблонный метод (Template method)](/design_patterns/behavioral/template_method.md)
        * [Посетитель (Visitor)](/design_patterns/behavioral/visitor.md)

+ [Общие шаблоны распределения обязанностей (General Responsibility Assignment Software Patterns, GRASP)](https://ru.wikipedia.org/wiki/GRASP)
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

+ Составные паттерны проектирования
    * [Модель-Представление-Контроллер (MVC)](https://ru.wikipedia.org/wiki/Model-View-Controller)

+ [Архитектурные паттерны](https://en.wikipedia.org/wiki/Architectural_pattern)
    * Системные паттерны
        * Сервисно-ориентированная архитектура
        * Вертикальное масштабирование
        * Горизонтальное масштабирование
        * Отложенные вычисления
        * Асинхронная обработка
        * Конвейерная обработка
        * Использование толстого клиента
        * Кеширование
        * Функциональное разделение
        * Шардинг
        * Виртуальные шарды
        * Центральный диспетчер
        * Репликация
        * Партиционирование
        * Кластеризация
        * Денормализация
        * Введение избыточности
        * Параллельное выполнение
    * Структурные паттерны
        * Репозиторий
        * Клиент/сервер
        * Обьектно - ориентированный, Модель предметной области (Domain Model), модуль таблицы (Data Mapper)
        * Многоуровневая система (Layers) или абстрактная машина
        * Потоки данных (конвейер или фильтр)
    * Паттерны управления
        * Паттерны централизованного управления
            * Вызов - возврат (сценарий транзакции - частный случай)
            * Диспетчер
        * Паттерны управления, основанные на событиях
            * Передача сообщений
            * Управляемый прерываниями
        * Паттерны, обеспечивающие взаимодействие с базой данных
            * Активная запись (Active Record)
            * Единица работы (Unit Of Work)
            * Загрузка по требованию (Lazy Load)
            * Коллекция обьектов (Identity Map)
            * Множество записей (Record Set)
            * Наследование с одной таблицей (Single Table Inheritance)
            * Наследование с таблицами для каждого класса (Class Table Inheritance)
            * Оптимистическая автономная блокировка (Optimistic Offline Lock)
            * Отображение с помощью внешних ключей
            * Отображение с помощью таблицы ассоциаций (Association Table Mapping)
            * Пессимистическая автономная блокировка (Pessimistic Offline Lock)
            * Поле идентификации (Identity Field)
            * Преобразователь данных (Data Mapper)
            * Cохранение сеанса на стороне клиента (Client Session State)
            * Cохранение сеанса на стороне сервера (Server Session State)
            * Шлюз записи данных (Row Data Gateway)
            * Шлюз таблицы данных (Table Data Gateway)

+ [J2EE паттерны](https://ru.wikipedia.org/wiki/Шаблоны_J2EE)

+ [Паттерны игрового программирования](http://gameprogrammingpatterns.com/)

### Парадигмы, принципы, стандарты и т.д.

+ Парадигмы
    * [Абстракция](https://ru.wikipedia.org/wiki/Абстракция_данных)
    * [Инкапсуляция](https://ru.wikipedia.org/wiki/Инкапсуляция_(программирование))
    * [Наследование](https://ru.wikipedia.org/wiki/Наследование_(программирование))
    * [Полиморфизм](https://ru.wikipedia.org/wiki/Полиморфизм_(информатика))

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

### Технологии

+ Стек .NET
    * Платформы
        * [Платформа .NET Framework](https://ru.wikipedia.org/wiki/.NET_Framework)
            * [Common Language Infrastructure (CLI)](https://ru.wikipedia.org/wiki/Common_Language_Infrastructure)
            * [Common Language Runtime (CLR)](https://ru.wikipedia.org/wiki/Common_Language_Runtime)
            * [Common Intermediate Language (CIL)](https://ru.wikipedia.org/wiki/Common_Intermediate_Language)
            * [Base Class Library (BCL)](https://ru.wikipedia.org/wiki/Base_Class_Library)
            * [Component Object Model (COM)](https://ru.wikipedia.org/wiki/Component_Object_Model)
            * [Windows Runtime (WinRT)](https://ru.wikipedia.org/wiki/Windows_Runtime)
            * [Windows Communication Foundation (WCF)](https://ru.wikipedia.org/wiki/Windows_Communication_Foundation)
            * [Windows Workflow Foundation (WF)](https://ru.wikipedia.org/wiki/Windows_Workflow_Foundation)
            * [Службы Windows (Windows Services)](https://ru.wikipedia.org/wiki/Службы_Windows)
            * [C# (CSharp)](https://ru.wikipedia.org/wiki/C_Sharp)
            * [Language Integrated Query (LINQ)](https://ru.wikipedia.org/wiki/Language_Integrated_Query)
            * [ActiveX Data Object для .NET (ADO.NET)](https://ru.wikipedia.org/wiki/ADO.NET)
            * [ADO.NET Entity Framework (EF)](https://ru.wikipedia.org/wiki/ADO.NET_Entity_Framework)
            * [Transact-SQL (T-SQL)](https://ru.wikipedia.org/wiki/Transact-SQL)
            * [Active Server Pages для .NET (ASP.NET)](https://ru.wikipedia.org/wiki/ASP.NET)
            * [ASP.NET MVC Framework](https://ru.wikipedia.org/wiki/ASP.NET_MVC_Framework)
            * [Windows Forms](https://ru.wikipedia.org/wiki/Windows_Forms)
            * [Windows Presentation Foundation (WPF)](https://ru.wikipedia.org/wiki/Windows_Presentation_Foundation)
            * [Microsoft Silverlight](https://ru.wikipedia.org/wiki/Microsoft_Silverlight)
            * [Internet Information Services (IIS)](https://ru.wikipedia.org/wiki/Internet_Information_Services)
            * [Microsoft Azure](https://ru.wikipedia.org/wiki/Microsoft_Azure)
            * [Microsoft Message Queuing (MSMQ)](https://en.wikipedia.org/wiki/Microsoft_Message_Queuing)
        * [Платформа Mono](https://ru.wikipedia.org/wiki/Mono)
        * [Платформа Portable.NET](https://ru.wikipedia.org/wiki/Portable.NET)
    * Библиотеки и прочее
        * [Awesome .NET - A collection of Awesome .NET libraries, tools & frameworks](https://dotnet.libhunt.com/)

+ Стек Java
    * Платформы
        * [Java SE - Java Platform, Standard Edition](http://www.oracle.com/technetwork/java/javase/tech/index.html)
        * [Java EE - Java Platform, Enterprise Edition](http://www.oracle.com/technetwork/java/javaee/tech/index.html)
        * [Java ME - Java Platform, Micro Edition](http://www.oracle.com/technetwork/java/embedded/javame/index.html)
        * [JavaFX](http://www.oracle.com/technetwork/java/javafx/overview/index.html)
        * [Java Card](http://www.oracle.com/technetwork/java/embedded/javacard/overview/index.html)
    * Библиотеки и прочее
        * [Better Java](https://github.com/cxxr/better-java)
        * [Design patterns implemented in Java](http://java-design-patterns.com/patterns/)
        * [Modern Java - A Guide to Java 8](https://github.com/winterbe/java8-tutorial)
        * [Awesome Java - A curated list of awesome Java frameworks, libraries and software](https://java.libhunt.com/)
        * [Список полезных ссылок для Java программиста](https://github.com/Vedenin/useful-java-links/tree/master/link-rus)
        * [Java EE 7 Samples](https://github.com/javaee-samples/javaee7-samples)
        * [Java EE 7 Examples](https://github.com/glassfish/javaee7-examples)

+ Системы управления базами данных
    * PostgreSQL
        * [PostgreSQL - официальный сайт](https://www.postgresql.org/)
        * [Postgres Professional - российский вендор PostgreSQL](https://postgrespro.ru/)
        * [Постгресмен - группа разработчиков PostgreSQL](http://postgresmen.ru/)

+ Системы управления версиями
    * Git
        * [Список команд](/technologies/version_control_systems/git/git_commands.md)

### Литература

+ Разработка
    * [Совершенный код - Стив Макконнелл](http://www.ozon.ru/context/detail/id/5508646/)
    * [Чистый код - Роберт К. Мартин](http://www.ozon.ru/context/detail/id/5011068/)

+ Структуры и алгоритмы обработки данных
    * [Абстракция данных и решение задач на С++. Стены и зеркала - Фрэнк М. Каррано, Джанет Дж. Причард](http://www.ozon.ru/context/detail/id/1435484/)
    * [Алгоритмы. Построение и анализ - Томас Х. Кормен, Чарльз И. Лейзерсон](https://www.ozon.ru/context/detail/id/33769775/)
    * [Алгоритмы на C++ - Роберт Седжвик](http://www.ozon.ru/context/detail/id/31924296/)

+ Паттерны
    * [Паттерны проектирования - "Банда четырех" (Gang of Four, GoF)](http://www.ozon.ru/context/detail/id/2457392/)
    * [Паттерны проектирования - Элизабет Фримен, Эрик Фримен, Кэти Сиерра, Берт Бейтс](https://www.ozon.ru/context/detail/id/20216992/)
    * [Шаблоны корпоративных приложений - Мартин Фаулер, Дейвид Райс](http://www.ozon.ru/context/detail/id/4884925/)
    * [Рефакторинг с использованием шаблонов - Джошуа Кериевски](http://www.ozon.ru/context/detail/id/2909721/)

+ C#
    * [CLR via C#. Программирование на платформе Microsoft.NET Framework 4.5 на языке C# - Джеффри Рихтер](https://www.ozon.ru/context/detail/id/21236101/)
    * [Язык программирования C# 5.0 и платформа .NET 4.5 - Эндрю Троелсен](http://www.ozon.ru/context/detail/id/19916784/)
    * [WPF: Windows Presentation Foundation в .NET 4.5 с примерами на C# 5.0 для профессионалов - Мэтью Макдональд](https://www.ozon.ru/context/detail/id/21462174/)

+ Java
    * Общее
        * [Философия Java - Брюс Эккель](https://www.ozon.ru/context/detail/id/30425811/)
    * Многопоточное программирование
    	* [Java Concurrency in Practice - Дуг Ли, Брайан Готц, Тим Пайерлс, Джошуа Блох, Джозеф Боубир, Дэвид Холмс](http://www.ozon.ru/context/detail/id/3174887/)
    * Java EE
        * [Изучаем Java EE 7 - Энтони Гонсалвес](https://www.ozon.ru/context/detail/id/27663406/)
        * [Java EE 7 и сервер приложений GlassFish 4 - Дэвид Хеффельфингер](http://www.ozon.ru/context/detail/id/33686213/)
        * [Core J2EE Patterns: Best Practices and Design Strategies](http://www.corej2eepatterns.com/)
        * [Java EE. Паттерны проектирования для профессионалов - Мурат Йенер, Алекс Фидом](https://www.ozon.ru/context/detail/id/34187042/)

+ Android
    * [Android 4. Программирование приложений для планшетных компьютеров и смартфонов - Рето Майер](http://www.ozon.ru/context/detail/id/21469100/)

+ Web
    * [Создаем динамические веб-сайты с помощью PHP, MySQL, JavaScript, CSS и HTML5 - Робин Никсон](http://www.ozon.ru/context/detail/id/136593716/)

+ Системы управления базами данных
    * PostgreSQL
        * [Работа с PostgreSQL: настройка и масштабирование](http://postgresql.leopard.in.ua/)
        * [Администрирование PostgreSQL 9. Книга рецептов - Саймон Ригс, Ханну Кросинг](https://www.ozon.ru/context/detail/id/19133383/)

+ Системы управления версиями
    * [Git для профессионального программиста - Скотт Чакон, Бен Штрауб](http://www.ozon.ru/context/detail/id/33575056/)

### Полезное

+ [Вопросы на собеседование Junior Java Developer и ответы на них](https://jsehelper.blogspot.ru/2016/01/blog-post.html)
+ [Статья "Java: Русские буквы и не только..."](http://www.javaportal.ru/java/articles/ruschars/ruschars.html)