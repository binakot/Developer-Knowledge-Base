# Адаптер (Adapter) #

Паттерн Адаптер преобразует интерфейс класса к другому интерфейсу,
на который рассчитывает клиент. Адаптер обеспечивает совместную работу классов,
невозможную в обычных условиях из-за несовместимости интерфейсов.

Адаптер класса использует множественное наследование для адаптации одного интерфейса к другому,
поэтому не актуален для языков, в которых множественное наследование недоступно (C#, Java и прочие).

Адаптер объекта применяет композицию объектов.

![UML](/design_patterns/structural/adapter_UML.svg)

* Target - целевой интерфейс

* Adaptee - адаптируемый интерфейс

* Adapter - адаптер

[Статья на Википедии](https://ru.wikipedia.org/wiki/Адаптер_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Adapter Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create adapter and place a request
            Target target = new Adapter();
            target.Request();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Target' class
    /// </summary>
    internal class Target
    {
        public virtual void Request()
        {
            Console.WriteLine("Called Target Request()");
        }
    }

    /// <summary>
    /// The 'Adapter' class
    /// </summary>
    internal class Adapter : Target
    {
        private Adaptee adaptee = new Adaptee();

        public override void Request()
        {
            // Possibly do some other work
            //   and then call SpecificRequest
            adaptee.SpecificRequest();
        }
    }

    /// <summary>
    /// The 'Adaptee' class
    /// </summary>
    internal class Adaptee
    {
        public void SpecificRequest()
        {
            Console.WriteLine("Called SpecificRequest()");
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Adapter Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Non-adapted chemical compound
            Compound unknown = new Compound();
            unknown.Display();

            // Adapted chemical compounds
            Compound water = new RichCompound("Water");
            water.Display();

            Compound benzene = new RichCompound("Benzene");
            benzene.Display();

            Compound ethanol = new RichCompound("Ethanol");
            ethanol.Display();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Target' class
    /// </summary>
    internal class Compound
    {
        protected float boilingPoint;
        protected float meltingPoint;
        protected double molecularWeight;
        protected string molecularFormula;

        public virtual void Display()
        {
            Console.WriteLine("\nCompound: Unknown ------ ");
        }
    }

    /// <summary>
    /// The 'Adapter' class
    /// </summary>
    internal class RichCompound : Compound
    {
        private string chemical;
        private ChemicalDatabank bank;

        // Constructor
        public RichCompound(string chemical)
        {
            this.chemical = chemical;
        }

        public override void Display()
        {
            // The Adaptee
            bank = new ChemicalDatabank();

            boilingPoint = bank.GetCriticalPoint(chemical, "B");
            meltingPoint = bank.GetCriticalPoint(chemical, "M");
            molecularWeight = bank.GetMolecularWeight(chemical);
            molecularFormula = bank.GetMolecularStructure(chemical);

            Console.WriteLine("\nCompound: {0} ------ ", chemical);
            Console.WriteLine(" Formula: {0}", molecularFormula);
            Console.WriteLine(" Weight : {0}", molecularWeight);
            Console.WriteLine(" Melting Pt: {0}", meltingPoint);
            Console.WriteLine(" Boiling Pt: {0}", boilingPoint);
        }
    }

    /// <summary>
    /// The 'Adaptee' class
    /// </summary>
    internal class ChemicalDatabank
    {
        // The databank 'legacy API'
        public float GetCriticalPoint(string compound, string point)
        {
            // Melting Point
            if (point == "M")
            {
                switch (compound.ToLower())
                {
                    case "water": return 0.0f;
                    case "benzene": return 5.5f;
                    case "ethanol": return -114.1f;
                    default: return 0f;
                }
            }
            // Boiling Point
            else
            {
                switch (compound.ToLower())
                {
                    case "water": return 100.0f;
                    case "benzene": return 80.1f;
                    case "ethanol": return 78.3f;
                    default: return 0f;
                }
            }
        }

        public string GetMolecularStructure(string compound)
        {
            switch (compound.ToLower())
            {
                case "water": return "H20";
                case "benzene": return "C6H6";
                case "ethanol": return "C2H5OH";
                default: return "";
            }
        }

        public double GetMolecularWeight(string compound)
        {
            switch (compound.ToLower())
            {
                case "water": return 18.015;
                case "benzene": return 78.1134;
                case "ethanol": return 46.0688;
                default: return 0d;
            }
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for the .NET optimized
    /// Adapter Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Non-adapted chemical compound
            var unknown = new Compound();
            unknown.Display();

            // Adapted chemical compounds
            var water = new RichCompound(Chemical.Water);
            water.Display();

            var benzene = new RichCompound(Chemical.Benzene);
            benzene.Display();

            var ethanol = new RichCompound(Chemical.Ethanol);
            ethanol.Display();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Target' class
    /// </summary>
    internal class Compound
    {
        public Chemical Chemical { get; protected set; }
        public float BoilingPoint { get; protected set; }
        public float MeltingPoint { get; protected set; }
        public double MolecularWeight { get; protected set; }
        public string MolecularFormula { get; protected set; }

        public virtual void Display()
        {
            Console.WriteLine("\nCompound: Unknown ------ ");
        }
    }

    /// <summary>
    /// The 'Adapter' class
    /// </summary>
    internal class RichCompound : Compound
    {
        private ChemicalDatabank bank;

        // Constructor
        public RichCompound(Chemical chemical)
        {
            Chemical = chemical;

            // The Adaptee
            bank = new ChemicalDatabank();
        }

        public override void Display()
        {
            // Adaptee request methods
            BoilingPoint = bank.GetCriticalPoint(Chemical, State.Boiling);
            MeltingPoint = bank.GetCriticalPoint(Chemical, State.Melting);
            MolecularWeight = bank.GetMolecularWeight(Chemical);
            MolecularFormula = bank.GetMolecularStructure(Chemical);

            Console.WriteLine("\nCompound: {0} ------ ", Chemical);
            Console.WriteLine(" Formula: {0}", MolecularFormula);
            Console.WriteLine(" Weight : {0}", MolecularWeight);
            Console.WriteLine(" Melting Pt: {0}", MeltingPoint);
            Console.WriteLine(" Boiling Pt: {0}", BoilingPoint);
        }
    }

    /// <summary>
    /// The 'Adaptee' class
    /// </summary>
    internal class ChemicalDatabank
    {
        // The databank 'legacy API'
        public float GetCriticalPoint(Chemical compound, State point)
        {
            // Melting Point
            if (point == State.Melting)
            {
                switch (compound)
                {
                    case Chemical.Water: return 0.0f;
                    case Chemical.Benzene: return 5.5f;
                    case Chemical.Ethanol: return -114.1f;
                    default: return 0f;
                }
            }
            // Boiling Point
            else
            {
                switch (compound)
                {
                    case Chemical.Water: return 100.0f;
                    case Chemical.Benzene: return 80.1f;
                    case Chemical.Ethanol: return 78.3f;
                    default: return 0f;
                }
            }
        }

        public string GetMolecularStructure(Chemical compound)
        {
            switch (compound)
            {
                case Chemical.Water: return "H20";
                case Chemical.Benzene: return "C6H6";
                case Chemical.Ethanol: return "C2H5OH";
                default: return "";
            }
        }

        public double GetMolecularWeight(Chemical compound)
        {
            switch (compound)
            {
                case Chemical.Water: return 18.015;
                case Chemical.Benzene: return 78.1134;
                case Chemical.Ethanol: return 46.0688;
            }
            return 0d;
        }
    }

    /// <summary>
    /// Chemical enumeration
    /// </summary>
    public enum Chemical
    {
        Water,
        Benzene,
        Ethanol
    }

    /// <summary>
    /// State enumeration
    /// </summary>
    public enum State
    {
        Boiling,
        Melting
    }
```

## Реализация на C# (Head First) ##

```csharp
    internal class DuckTestDrive
    {
        private static void Main(string[] args)
        {
            // Test 1: Duck test drive

            var duck = new MallardDuck();

            var turkey = new WildTurkey();
            IDuck turkeyAdapter = new TurkeyAdapter(turkey);

            Console.WriteLine("The Turkey says...");
            turkey.Gobble();
            turkey.Fly();

            Console.WriteLine("\nThe Duck says...");
            TestDuck(duck);

            Console.WriteLine("\nThe TurkeyAdapter says...");
            TestDuck(turkeyAdapter);

            // Test 2: Turkey test drive

            ITurkey duckAdapter = new DuckAdapter(duck);

            for (int i = 0; i < 10; i++)
            {
                Console.WriteLine("The DuckAdapter says...");
                duckAdapter.Gobble();
                duckAdapter.Fly();
            }

            // Wait for user
            Console.ReadKey();
        }

        private static void TestDuck(IDuck duck)
        {
            duck.Quack();
            duck.Fly();
        }
    }

    public interface IDuck
    {
        void Quack();

        void Fly();
    }

    public interface ITurkey
    {
        void Gobble();

        void Fly();
    }

    public class MallardDuck : IDuck
    {
        public void Quack()
        {
            Console.WriteLine("Quack");
        }

        public void Fly()
        {
            Console.WriteLine("I'm flying");
        }
    }

    public class WildTurkey : ITurkey
    {
        public void Gobble()
        {
            Console.WriteLine("Gobble gobble");
        }

        public void Fly()
        {
            Console.WriteLine("I'm flying a short distance");
        }
    }

    public class DuckAdapter : ITurkey
    {
        private IDuck _duck;
        private Random _random = new Random();

        // Constructor
        public DuckAdapter(IDuck duck)
        {
            this._duck = duck;
        }

        public void Gobble()
        {
            _duck.Quack();
        }

        public void Fly()
        {
            if (_random.Next(5) == 0)
            {
                _duck.Fly();
            }
        }
    }

    public class TurkeyAdapter : IDuck
    {
        private ITurkey _turkey;

        // Constructor
        public TurkeyAdapter(ITurkey turkey)
        {
            this._turkey = turkey;
        }

        public void Quack()
        {
            _turkey.Gobble();
        }

        public void Fly()
        {
            for (int i = 0; i < 5; i++)
            {
                _turkey.Fly();
            }
        }
    }
```

## Реализация на JAVA ##

```java
    TODO
```