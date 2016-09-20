# Наблюдатель (Observer) #

Также известен как Подчиненные(Dependents) или Издатель-подписчик (Publish-Subscribe).

Паттерн Наблюдатель определяет отношение "один-ко-многим" между объектами таким образом,
что при изменении состояния субъекта наблюдения происходит автоматическое оповещение и обновление всех зависимых объектов-наблюдателей.

![UML](/design_patterns/behavioral/observer_UML.gif)

* Subject - абстрактный наблюдаемый субъект

* ConcreteSubject - конкретный наблюдаемый субъект

* Observer - абстрактный наблюдатель

* ConcreteObserver - конкретный наблюдатель

[Статья на Википедии](https://ru.wikipedia.org/wiki/Наблюдатель_(шаблон_проектирования))

Встроенная в JDK реализация паттерна в _java.util.Observable_ и _java.util.Observer_
(Observable - является классом, а не интерфейсом, что значительно снижает его полезность).

В SWING (и других GUI фреймворках) наблюдателями выступают Listener'ы, которые ожидают событий от UI
(нажатие на кнопку, прокрутка и другое).

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Observer Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Configure Observer pattern
            ConcreteSubject s = new ConcreteSubject();

            s.Attach(new ConcreteObserver(s, "X"));
            s.Attach(new ConcreteObserver(s, "Y"));
            s.Attach(new ConcreteObserver(s, "Z"));

            // Change subject and notify observers
            s.SubjectState = "ABC";
            s.Notify();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subject' abstract class
    /// </summary>
    internal abstract class Subject
    {
        private List<Observer> observers = new List<Observer>();

        public void Attach(Observer observer)
        {
            observers.Add(observer);
        }

        public void Detach(Observer observer)
        {
            observers.Remove(observer);
        }

        public void Notify()
        {
            foreach (Observer o in observers)
            {
                o.Update();
            }
        }
    }

    /// <summary>
    /// The 'ConcreteSubject' class
    /// </summary>
    internal class ConcreteSubject : Subject
    {
        private string subjectState;

        // Gets or sets subject state
        public string SubjectState
        {
            get { return subjectState; }
            set { subjectState = value; }
        }
    }

    /// <summary>
    /// The 'Observer' abstract class
    /// </summary>
    internal abstract class Observer
    {
        public abstract void Update();
    }

    /// <summary>
    /// The 'ConcreteObserver' class
    /// </summary>
    internal class ConcreteObserver : Observer
    {
        private string name;
        private string observerState;
        private ConcreteSubject subject;

        // Constructor
        public ConcreteObserver(
            ConcreteSubject subject, string name)
        {
            this.subject = subject;
            this.name = name;
        }

        public override void Update()
        {
            observerState = subject.SubjectState;
            Console.WriteLine("Observer {0}'s new state is {1}",
                name, observerState);
        }

        // Gets or sets subject
        public ConcreteSubject Subject
        {
            get { return subject; }
            set { subject = value; }
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Observer Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create IBM stock and attach investors
            IBM ibm = new IBM("IBM", 120.00);
            ibm.Attach(new Investor("Sorros"));
            ibm.Attach(new Investor("Berkshire"));

            // Fluctuating prices will notify investors
            ibm.Price = 120.10;
            ibm.Price = 121.00;
            ibm.Price = 120.50;
            ibm.Price = 120.75;

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subject' abstract class
    /// </summary>
    internal abstract class Stock
    {
        private string symbol;
        private double price;
        private List<IInvestor> investors = new List<IInvestor>();

        // Constructor
        public Stock(string symbol, double price)
        {
            this.symbol = symbol;
            this.price = price;
        }

        public void Attach(IInvestor investor)
        {
            investors.Add(investor);
        }

        public void Detach(IInvestor investor)
        {
            investors.Remove(investor);
        }

        public void Notify()
        {
            foreach (IInvestor investor in investors)
            {
                investor.Update(this);
            }

            Console.WriteLine("");
        }

        // Gets or sets the price
        public double Price
        {
            get { return price; }
            set
            {
                if (price != value)
                {
                    price = value;
                    Notify();
                }
            }
        }

        // Gets the symbol
        public string Symbol
        {
            get { return symbol; }
        }
    }

    /// <summary>
    /// The 'ConcreteSubject' class
    /// </summary>
    internal class IBM : Stock
    {
        // Constructor
        public IBM(string symbol, double price)
            : base(symbol, price)
        {
        }
    }

    /// <summary>
    /// The 'Observer' interface
    /// </summary>
    internal interface IInvestor
    {
        void Update(Stock stock);
    }

    /// <summary>
    /// The 'ConcreteObserver' class
    /// </summary>
    internal class Investor : IInvestor
    {
        private string name;
        private Stock stock;

        // Constructor
        public Investor(string name)
        {
            this.name = name;
        }

        public void Update(Stock stock)
        {
            Console.WriteLine("Notified {0} of {1}'s " +
                "change to {2:C}", name, stock.Symbol, stock.Price);
        }

        // Gets or sets the stock
        public Stock Stock
        {
            get { return stock; }
            set { stock = value; }
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Observer Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create IBM stock and attach investors
            var ibm = new IBM(120.00);

            // Attach 'listeners', i.e. Investors
            ibm.Attach(new Investor { Name = "Sorros" });
            ibm.Attach(new Investor { Name = "Berkshire" });

            // Fluctuating prices will notify listening investors
            ibm.Price = 120.10;
            ibm.Price = 121.00;
            ibm.Price = 120.50;
            ibm.Price = 120.75;

            // Wait for user
            Console.ReadKey();
        }
    }

    // Custom event arguments
    public class ChangeEventArgs : EventArgs
    {
        // Gets or sets symbol
        public string Symbol { get; set; }

        // Gets or sets price
        public double Price { get; set; }
    }

    /// <summary>
    /// The 'Subject' abstract class
    /// </summary>
    internal abstract class Stock
    {
        protected string symbol;
        protected double price;

        // Constructor
        public Stock(string symbol, double price)
        {
            this.symbol = symbol;
            this.price = price;
        }

        // Event
        public event EventHandler<ChangeEventArgs> Change;

        // Invoke the Change event
        public virtual void OnChange(ChangeEventArgs e)
        {
            if (Change != null)
            {
                Change(this, e);
            }
        }

        public void Attach(IInvestor investor)
        {
            Change += investor.Update;
        }

        public void Detach(IInvestor investor)
        {
            Change -= investor.Update;
        }

        // Gets or sets the price
        public double Price
        {
            get { return price; }
            set
            {
                if (price != value)
                {
                    price = value;
                    OnChange(new ChangeEventArgs { Symbol = symbol, Price = price });
                    Console.WriteLine("");
                }
            }
        }
    }

    /// <summary>
    /// The 'ConcreteSubject' class
    /// </summary>
    internal class IBM : Stock
    {
        // Constructor - symbol for IBM is always same
        public IBM(double price)
            : base("IBM", price)
        {
        }
    }

    /// <summary>
    /// The 'Observer' interface
    /// </summary>
    internal interface IInvestor
    {
        void Update(object sender, ChangeEventArgs e);
    }

    /// <summary>
    /// The 'ConcreteObserver' class
    /// </summary>
    internal class Investor : IInvestor
    {
        // Gets or sets the investor name
        public string Name { get; set; }

        // Gets or sets the stock
        public Stock Stock { get; set; }

        public void Update(object sender, ChangeEventArgs e)
        {
            Console.WriteLine("Notified {0} of {1}'s " +
                "change to {2:C}", Name, e.Symbol, e.Price);
        }
    }
```

## Реализация на C# (Head First) ##

```csharp
    internal class DotNetObserverExample
    {
        private static void Main()
        {
            // Create listeners
            var angel = new ActionListener("Angel");
            var devil = new ActionListener("Devil");

            // Create Button and attach listeners
            var button = new Button("Click Me");
            button.Attach(angel);
            button.Attach(devil);

            // Simulate clicks on button
            button.Push(1, 3);
            button.Push(5, 4);
            button.Push(8, 5);

            // Wait for user
            Console.ReadKey();
        }
    }

    #region EventArgs

    // Custom event arguments
    public class ClickEventArgs : EventArgs
    {
        public int X { get; private set; }
        public int Y { get; private set; }

        // Constructor
        public ClickEventArgs(int x, int y)
        {
            this.X = x;
            this.Y = y;
        }
    }

    #endregion EventArgs

    #region Controls

    // Base class for UI controls

    internal abstract class Control
    {
        protected string text;

        // Constructor
        public Control(string text)
        {
            this.text = text;
        }

        // Event
        public event EventHandler<ClickEventArgs> Click;

        // Invoke the Click  event
        public virtual void OnClick(ClickEventArgs e)
        {
            if (Click != null)
            {
                Click(this, e);
            }
        }

        public void Attach(ActionListener listener)
        {
            Click += listener.Update;
        }

        public void Detach(ActionListener listener)
        {
            Click -= listener.Update;
        }

        // Use this method to simulate push (click) events
        public void Push(int x, int y)
        {
            OnClick(new ClickEventArgs(x, y));
            Console.WriteLine("");
        }
    }

    // Button control

    internal class Button : Control
    {
        // Constructor
        public Button(string text)
            : base(text)
        {
        }
    }

    #endregion Controls

    #region ActionListener

    internal interface IActionListener
    {
        void Update(object sender, ClickEventArgs e);
    }

    internal class ActionListener : IActionListener
    {
        private string _name;

        // Constructor
        public ActionListener(string name)
        {
            this._name = name;
        }

        public void Update(object sender, ClickEventArgs e)
        {
            Console.WriteLine("Notified {0} of click at ({1},{2})",
                _name, e.X, e.Y);
        }
    }

    #endregion ActionListener
```

## Реализация на JAVA ##

```java
    TODO
```