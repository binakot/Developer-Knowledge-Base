# Хранитель (Memento) #

Также известен как Лексема (Token).

Паттерн Хранитель используется для реализации возврата к одному из предыдущих состояний.

Классическая структура паттерна Хранитель:

![UML](https://bitbucket.org/firstmk/pmk/wiki/design_patterns/behavioral/momento_UML.gif)

Нестандартная структура паттерна Хранитель:

![UML2](https://bitbucket.org/firstmk/pmk/wiki/design_patterns/behavioral/momento_UML_2.png)

* Memento - Хранитель

* Originator - Хозяин, Создатель

* Caretaker - Посыльный, Опекун

[Статья на Википедии](https://ru.wikipedia.org/wiki/Хранитель_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Memento Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            Originator o = new Originator();
            o.State = "On";

            // Store internal state
            Caretaker c = new Caretaker();
            c.Memento = o.CreateMemento();

            // Continue changing originator
            o.State = "Off";

            // Restore saved state
            o.SetMemento(c.Memento);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Originator' class
    /// </summary>
    internal class Originator
    {
        private string state;

        // Property
        public string State
        {
            get { return state; }
            set
            {
                state = value;
                Console.WriteLine("State = " + state);
            }
        }

        // Creates memento
        public Memento CreateMemento()
        {
            return (new Memento(state));
        }

        // Restores original state
        public void SetMemento(Memento memento)
        {
            Console.WriteLine("Restoring state...");
            State = memento.State;
        }
    }

    /// <summary>
    /// The 'Memento' class
    /// </summary>
    internal class Memento
    {
        private string state;

        // Constructor
        public Memento(string state)
        {
            this.state = state;
        }

        // Gets or sets state
        public string State
        {
            get { return state; }
        }
    }

    /// <summary>
    /// The 'Caretaker' class
    /// </summary>
    internal class Caretaker
    {
        private Memento memento;

        // Gets or sets memento
        public Memento Memento
        {
            set { memento = value; }
            get { return memento; }
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Memento Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            SalesProspect s = new SalesProspect();
            s.Name = "Noel van Halen";
            s.Phone = "(412) 256-0990";
            s.Budget = 25000.0;

            // Store internal state
            ProspectMemory m = new ProspectMemory();
            m.Memento = s.SaveMemento();

            // Continue changing originator
            s.Name = "Leo Welch";
            s.Phone = "(310) 209-7111";
            s.Budget = 1000000.0;

            // Restore saved state
            s.RestoreMemento(m.Memento);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Originator' class
    /// </summary>
    internal class SalesProspect
    {
        private string name;
        private string phone;
        private double budget;

        // Gets or sets name
        public string Name
        {
            get { return name; }
            set
            {
                name = value;
                Console.WriteLine("Name:   " + name);
            }
        }

        // Gets or sets phone
        public string Phone
        {
            get { return phone; }
            set
            {
                phone = value;
                Console.WriteLine("Phone:  " + phone);
            }
        }

        // Gets or sets budget
        public double Budget
        {
            get { return budget; }
            set
            {
                budget = value;
                Console.WriteLine("Budget: " + budget);
            }
        }

        // Stores memento
        public Memento SaveMemento()
        {
            Console.WriteLine("\nSaving state --\n");
            return new Memento(name, phone, budget);
        }

        // Restores memento
        public void RestoreMemento(Memento memento)
        {
            Console.WriteLine("\nRestoring state --\n");
            this.Name = memento.Name;
            this.Phone = memento.Phone;
            this.Budget = memento.Budget;
        }
    }

    /// <summary>
    /// The 'Memento' class
    /// </summary>
    internal class Memento
    {
        private string name;
        private string phone;
        private double budget;

        // Constructor
        public Memento(string name, string phone, double budget)
        {
            this.name = name;
            this.phone = phone;
            this.budget = budget;
        }

        // Gets or sets name
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        // Gets or set phone
        public string Phone
        {
            get { return phone; }
            set { phone = value; }
        }

        // Gets or sets budget
        public double Budget
        {
            get { return budget; }
            set { budget = value; }
        }
    }

    /// <summary>
    /// The 'Caretaker' class
    /// </summary>
    internal class ProspectMemory
    {
        private Memento memento;

        // Property
        public Memento Memento
        {
            set { memento = value; }
            get { return memento; }
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Memento Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Init sales prospect through object initialization
            var s = new SalesProspect
            {
                Name = "Joel van Halen",
                Phone = "(412) 256-0990",
                Budget = 25000.0
            };

            // Store internal state
            var m = new ProspectMemory();
            m.Memento = s.SaveMemento();

            // Change originator
            s.Name = "Leo Welch";
            s.Phone = "(310) 209-7111";
            s.Budget = 1000000.0;

            // Restore saved state
            s.RestoreMemento(m.Memento);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Originator' class
    /// </summary>
    [Serializable]
    internal class SalesProspect
    {
        private string name;
        private string phone;
        private double budget;

        // Gets or sets name
        public string Name
        {
            get { return name; }
            set
            {
                name = value;
                Console.WriteLine("Name:   " + name);
            }
        }

        // Gets or sets phone
        public string Phone
        {
            get { return phone; }
            set
            {
                phone = value;
                Console.WriteLine("Phone:  " + phone);
            }
        }

        // Gets or sets budget
        public double Budget
        {
            get { return budget; }
            set
            {
                budget = value;
                Console.WriteLine("Budget: " + budget);
            }
        }

        // Stores (serializes) memento
        public Memento SaveMemento()
        {
            Console.WriteLine("\nSaving state --\n");

            var memento = new Memento();
            return memento.Serialize(this);
        }

        // Restores (deserializes) memento
        public void RestoreMemento(Memento memento)
        {
            Console.WriteLine("\nRestoring state --\n");

            var s = (SalesProspect)memento.Deserialize();
            this.Name = s.Name;
            this.Phone = s.Phone;
            this.Budget = s.Budget;
        }
    }

    /// <summary>
    /// The 'Memento' class
    /// </summary>
    internal class Memento
    {
        private MemoryStream stream = new MemoryStream();
        private SoapFormatter formatter = new SoapFormatter();

        public Memento Serialize(object o)
        {
            formatter.Serialize(stream, o);
            return this;
        }

        public object Deserialize()
        {
            stream.Seek(0, SeekOrigin.Begin);
            object o = formatter.Deserialize(stream);
            stream.Close();

            return o;
        }
    }

    /// <summary>
    /// The 'Caretaker' class
    /// </summary>
    internal class ProspectMemory
    {
        public Memento Memento { get; set; }
    }
```

## Реализация на JAVA ##

```java
    TODO
```