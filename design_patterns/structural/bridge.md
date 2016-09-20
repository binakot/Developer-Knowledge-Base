# Мост (Bridge) #

Также известен как Handle/Body (Описатель/Тело).

Паттерн Мост позволяет изменять реализацию и абстракцию, для чего они размещаются в двух разных иерархиях классов.

![UML](/design_patterns/structural/bridge_UML.svg?raw=true)

* Abstraction - абстракция

* RefinedAbstraction - уточненная абстракция

* Implementor - абстрактый реализатор

* ConcreteImplementor - конкретный реализатор

[Статья на Википедии](https://ru.wikipedia.org/wiki/Мост_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Bridge Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            Abstraction ab = new RefinedAbstraction();

            // Set implementation and call
            ab.Implementor = new ConcreteImplementorA();
            ab.Operation();

            // Change implemention and call
            ab.Implementor = new ConcreteImplementorB();
            ab.Operation();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Abstraction' class
    /// </summary>
    internal class Abstraction
    {
        protected Implementor implementor;

        // Property
        public Implementor Implementor
        {
            set { implementor = value; }
        }

        public virtual void Operation()
        {
            implementor.Operation();
        }
    }

    /// <summary>
    /// The 'Implementor' abstract class
    /// </summary>
    internal abstract class Implementor
    {
        public abstract void Operation();
    }

    /// <summary>
    /// The 'RefinedAbstraction' class
    /// </summary>
    internal class RefinedAbstraction : Abstraction
    {
        public override void Operation()
        {
            implementor.Operation();
        }
    }

    /// <summary>
    /// The 'ConcreteImplementorA' class
    /// </summary>
    internal class ConcreteImplementorA : Implementor
    {
        public override void Operation()
        {
            Console.WriteLine("ConcreteImplementorA Operation");
        }
    }

    /// <summary>
    /// The 'ConcreteImplementorB' class
    /// </summary>
    internal class ConcreteImplementorB : Implementor
    {
        public override void Operation()
        {
            Console.WriteLine("ConcreteImplementorB Operation");
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Bridge Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create RefinedAbstraction
            var customers = new Customers();

            // Set ConcreteImplementor
            customers.Data = new CustomersData("Chicago");

            // Exercise the bridge
            customers.Show();
            customers.Next();
            customers.Show();
            customers.Next();
            customers.Show();
            customers.Add("Henry Velasquez");

            customers.ShowAll();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Abstraction' class
    /// </summary>
    internal class CustomersBase
    {
        private DataObject dataObject;

        public DataObject Data
        {
            set { dataObject = value; }
            get { return dataObject; }
        }

        public virtual void Next()
        {
            dataObject.NextRecord();
        }

        public virtual void Prior()
        {
            dataObject.PriorRecord();
        }

        public virtual void Add(string customer)
        {
            dataObject.AddRecord(customer);
        }

        public virtual void Delete(string customer)
        {
            dataObject.DeleteRecord(customer);
        }

        public virtual void Show()
        {
            dataObject.ShowRecord();
        }

        public virtual void ShowAll()
        {
            dataObject.ShowAllRecords();
        }
    }

    /// <summary>
    /// The 'RefinedAbstraction' class
    /// </summary>
    internal class Customers : CustomersBase
    {
        public override void ShowAll()
        {
            // Add separator lines
            Console.WriteLine();
            Console.WriteLine("------------------------");
            base.ShowAll();
            Console.WriteLine("------------------------");
        }
    }

    /// <summary>
    /// The 'Implementor' abstract class
    /// </summary>
    internal abstract class DataObject
    {
        public abstract void NextRecord();

        public abstract void PriorRecord();

        public abstract void AddRecord(string name);

        public abstract void DeleteRecord(string name);

        public abstract string GetCurrentRecord();

        public abstract void ShowRecord();

        public abstract void ShowAllRecords();
    }

    /// <summary>
    /// The 'ConcreteImplementor' class
    /// </summary>
    internal class CustomersData : DataObject
    {
        private List<string> customers = new List<string>();
        private int current = 0;

        private string city;

        public CustomersData(string city)
        {
            this.city = city;

            // Loaded from a database
            customers.Add("Jim Jones");
            customers.Add("Samual Jackson");
            customers.Add("Allen Good");
            customers.Add("Ann Stills");
            customers.Add("Lisa Giolani");
        }

        public override void NextRecord()
        {
            if (current <= customers.Count - 1)
            {
                current++;
            }
        }

        public override void PriorRecord()
        {
            if (current > 0)
            {
                current--;
            }
        }

        public override void AddRecord(string customer)
        {
            customers.Add(customer);
        }

        public override void DeleteRecord(string customer)
        {
            customers.Remove(customer);
        }

        public override string GetCurrentRecord()
        {
            return customers[current];
        }

        public override void ShowRecord()
        {
            Console.WriteLine(customers[current]);
        }

        public override void ShowAllRecords()
        {
            Console.WriteLine("Customer City: " + city);
            foreach (string customer in customers)
            {
                Console.WriteLine(" " + customer);
            }
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Bridge Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create RefinedAbstraction
            var customers = new Customers();

            // Set ConcreteImplementor
            customers.DataObject = new CustomersData { City = "Chicago" };

            // Exercise the bridge
            customers.Show();
            customers.Next();
            customers.Show();
            customers.Next();
            customers.Show();

            customers.Add("Henry Velasquez");
            customers.ShowAll();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Abstraction' class
    /// </summary>
    internal class CustomersBase
    {
        // Gets or sets data object
        public IDataObject<string> DataObject { get; set; }

        public virtual void Next()
        {
            DataObject.NextRecord();
        }

        public virtual void Prior()
        {
            DataObject.PriorRecord();
        }

        public virtual void Add(string name)
        {
            DataObject.AddRecord(name);
        }

        public virtual void Delete(string name)
        {
            DataObject.DeleteRecord(name);
        }

        public virtual void Show()
        {
            DataObject.ShowRecord();
        }

        public virtual void ShowAll()
        {
            DataObject.ShowAllRecords();
        }
    }

    /// <summary>
    /// The 'RefinedAbstraction' class
    /// </summary>
    internal class Customers : CustomersBase
    {
        public override void ShowAll()
        {
            // Add separator lines
            Console.WriteLine();
            Console.WriteLine("------------------------");
            base.ShowAll();
            Console.WriteLine("------------------------");
        }
    }

    /// <summary>
    /// The 'Implementor' interface
    /// </summary>
    internal interface IDataObject<T>
    {
        void NextRecord();

        void PriorRecord();

        void AddRecord(T t);

        void DeleteRecord(T t);

        T GetCurrentRecord();

        void ShowRecord();

        void ShowAllRecords();
    }

    /// <summary>
    /// The 'ConcreteImplementor' class
    /// </summary>
    internal class CustomersData : IDataObject<string>
    {
        // Gets or sets city
        public string City { get; set; }

        private List<string> customers;
        private int current = 0;

        // Constructor
        public CustomersData()
        {
            // Simulate loading from database
            customers = new List<string>
              { "Jim Jones", "Samual Jackson", "Allan Good",
                "Ann Stills", "Lisa Giolani" };
        }

        public void NextRecord()
        {
            if (current <= customers.Count - 1)
            {
                current++;
            }
        }

        public void PriorRecord()
        {
            if (current > 0)
            {
                current--;
            }
        }

        public void AddRecord(string customer)
        {
            customers.Add(customer);
        }

        public void DeleteRecord(string customer)
        {
            customers.Remove(customer);
        }

        public string GetCurrentRecord()
        {
            return customers[current];
        }

        public void ShowRecord()
        {
            Console.WriteLine(customers[current]);
        }

        public void ShowAllRecords()
        {
            Console.WriteLine("Customer Group: " + City);
            customers.ForEach(customer =>
                Console.WriteLine(" " + customer));
        }
    }
```

## Реализация на JAVA ##

```java
    TODO
```