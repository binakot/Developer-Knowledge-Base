# Стратегия (Strategy) #

Также известен как Политика (Policy).

Паттерн Стратегия определяет семейство алгоритмов, инкапсулирует каждый из них и обеспечивает взаимозаменяемость.
Он позволяет модифицировать алгоритмы независимо от их использования на стороне клиента.

![UML](/design_patterns/behavioral/strategy_UML.gif)

* Strategy - абстрактная стратегия

* ConcreteStrategies - конкретные стратегии

* Context - контекст

[Статья на Википедии](https://ru.wikipedia.org/wiki/Стратегия_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Strategy Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            Context context;

            // Three contexts following different strategies
            context = new Context(new ConcreteStrategyA());
            context.ContextInterface();

            context = new Context(new ConcreteStrategyB());
            context.ContextInterface();

            context = new Context(new ConcreteStrategyC());
            context.ContextInterface();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Strategy' abstract class
    /// </summary>
    internal abstract class Strategy
    {
        public abstract void AlgorithmInterface();
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class ConcreteStrategyA : Strategy
    {
        public override void AlgorithmInterface()
        {
            Console.WriteLine(
                "Called ConcreteStrategyA.AlgorithmInterface()");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class ConcreteStrategyB : Strategy
    {
        public override void AlgorithmInterface()
        {
            Console.WriteLine(
                "Called ConcreteStrategyB.AlgorithmInterface()");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class ConcreteStrategyC : Strategy
    {
        public override void AlgorithmInterface()
        {
            Console.WriteLine(
                "Called ConcreteStrategyC.AlgorithmInterface()");
        }
    }

    /// <summary>
    /// The 'Context' class
    /// </summary>
    internal class Context
    {
        private Strategy strategy;

        // Constructor
        public Context(Strategy strategy)
        {
            this.strategy = strategy;
        }

        public void ContextInterface()
        {
            strategy.AlgorithmInterface();
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Strategy Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Two contexts following different strategies
            SortedList studentRecords = new SortedList();

            studentRecords.Add("Samual");
            studentRecords.Add("Jimmy");
            studentRecords.Add("Sandra");
            studentRecords.Add("Vivek");
            studentRecords.Add("Anna");

            studentRecords.SetSortStrategy(new QuickSort());
            studentRecords.Sort();

            studentRecords.SetSortStrategy(new ShellSort());
            studentRecords.Sort();

            studentRecords.SetSortStrategy(new MergeSort());
            studentRecords.Sort();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Strategy' abstract class
    /// </summary>
    internal abstract class SortStrategy
    {
        public abstract void Sort(List<string> list);
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class QuickSort : SortStrategy
    {
        public override void Sort(List<string> list)
        {
            list.Sort();  // Default is Quicksort
            Console.WriteLine("QuickSorted list ");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class ShellSort : SortStrategy
    {
        public override void Sort(List<string> list)
        {
            //list.ShellSort();  not-implemented
            Console.WriteLine("ShellSorted list ");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class MergeSort : SortStrategy
    {
        public override void Sort(List<string> list)
        {
            //list.MergeSort(); not-implemented
            Console.WriteLine("MergeSorted list ");
        }
    }

    /// <summary>
    /// The 'Context' class
    /// </summary>
    internal class SortedList
    {
        private List<string> list = new List<string>();
        private SortStrategy sortstrategy;

        public void SetSortStrategy(SortStrategy sortstrategy)
        {
            this.sortstrategy = sortstrategy;
        }

        public void Add(string name)
        {
            list.Add(name);
        }

        public void Sort()
        {
            sortstrategy.Sort(list);

            // Iterate over list and display results
            foreach (string name in list)
            {
                Console.WriteLine(" " + name);
            }
            Console.WriteLine();
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Strategy Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Two contexts following different strategies
            var studentRecords = new SortedList()
              {
                new Student{ Name = "Samual", Ssn = "154-33-2009" },
                new Student{ Name = "Jimmy", Ssn = "487-43-1665" },
                new Student{ Name = "Sandra", Ssn = "655-00-2944" },
                new Student{ Name = "Vivek", Ssn = "133-98-8399" },
                new Student{ Name = "Anna", Ssn = "760-94-9844" },
              };

            studentRecords.SortStrategy = new QuickSort();
            studentRecords.SortStudents();

            studentRecords.SortStrategy = new ShellSort();
            studentRecords.SortStudents();

            studentRecords.SortStrategy = new MergeSort();
            studentRecords.SortStudents();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Strategy' interface
    /// </summary>
    internal interface ISortStrategy
    {
        void Sort(List<Student> list);
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class QuickSort : ISortStrategy
    {
        public void Sort(List<Student> list)
        {
            // Call overloaded Sort
            Sort(list, 0, list.Count - 1);
            Console.WriteLine("QuickSorted list ");
        }

        // Recursively sort
        private void Sort(List<Student> list, int left, int right)
        {
            int lhold = left;
            int rhold = right;

            // Use a random pivot
            var random = new Random();
            int pivot = random.Next(left, right);
            Swap(list, pivot, left);
            pivot = left;
            left++;

            while (right >= left)
            {
                int compareleft = list[left].Name.CompareTo(list[pivot].Name);
                int compareright = list[right].Name.CompareTo(list[pivot].Name);

                if ((compareleft >= 0) && (compareright < 0))
                {
                    Swap(list, left, right);
                }
                else
                {
                    if (compareleft >= 0)
                    {
                        right--;
                    }
                    else
                    {
                        if (compareright < 0)
                        {
                            left++;
                        }
                        else
                        {
                            right--;
                            left++;
                        }
                    }
                }
            }
            Swap(list, pivot, right);
            pivot = right;

            if (pivot > lhold) Sort(list, lhold, pivot);
            if (rhold > pivot + 1) Sort(list, pivot + 1, rhold);
        }

        // Swap helper function
        private void Swap(List<Student> list, int left, int right)
        {
            var temp = list[right];
            list[right] = list[left];
            list[left] = temp;
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class ShellSort : ISortStrategy
    {
        public void Sort(List<Student> list)
        {
            // ShellSort();  not-implemented
            Console.WriteLine("ShellSorted list ");
        }
    }

    /// <summary>
    /// A 'ConcreteStrategy' class
    /// </summary>
    internal class MergeSort : ISortStrategy
    {
        public void Sort(List<Student> list)
        {
            // MergeSort(); not-implemented
            Console.WriteLine("MergeSorted list ");
        }
    }

    /// <summary>
    /// The 'Context' class
    /// </summary>
    internal class SortedList : List<Student>
    {
        // Sets sort strategy
        public ISortStrategy SortStrategy { get; set; }

        // Perform sort
        public void SortStudents()
        {
            SortStrategy.Sort(this);

            // Display sort results
            foreach (var student in this)
            {
                Console.WriteLine(" " + student.Name);
            }
            Console.WriteLine();
        }
    }

    /// <summary>
    /// Represents a student
    /// </summary>
    internal class Student
    {
        // Gets or sets student name
        public string Name { get; set; }

        // Gets or sets student social security number
        public string Ssn { get; set; }
    }
```

## Реализация на C# (Head First) ##

```csharp
    public class MiniDuckSimulator
    {
        private static void Main(string[] args)
        {
            Duck mallard = new MallardDuck();
            mallard.Display();
            mallard.PerformQuack();
            mallard.PerformFly();

            Console.WriteLine("");

            Duck model = new ModelDuck();
            model.Display();
            model.PerformFly();

            model.FlyBehavior = new FlyRocketPowered();
            model.PerformFly();

            // Wait for user input
            Console.ReadKey();
        }
    }

    #region Duck

    public abstract class Duck
    {
        public IFlyBehavior FlyBehavior { get; set; }
        public IQuackBehavior QuackBehavior { get; set; }

        public abstract void Display();

        public void PerformFly()
        {
            FlyBehavior.Fly();
        }

        public void PerformQuack()
        {
            QuackBehavior.Quack();
        }

        public void Swim()
        {
            Console.WriteLine("All ducks float, even decoys!");
        }
    }

    public class MallardDuck : Duck
    {
        public MallardDuck()
        {
            QuackBehavior = new LoudQuack();
            FlyBehavior = new FlyWithWings();
        }

        override public void Display()
        {
            Console.WriteLine("I'm a real Mallard duck");
        }
    }

    public class ModelDuck : Duck
    {
        public ModelDuck()
        {
            QuackBehavior = new LoudQuack();
            FlyBehavior = new FlyNoWay();
        }

        override public void Display()
        {
            Console.WriteLine("I'm a model duck");
        }
    }

    #endregion Duck

    #region FlyBehavior

    public interface IFlyBehavior
    {
        void Fly();
    }

    public class FlyWithWings : IFlyBehavior
    {
        public void Fly()
        {
            Console.WriteLine("I'm flying!!");
        }
    }

    public class FlyNoWay : IFlyBehavior
    {
        public void Fly()
        {
            Console.WriteLine("I can't fly");
        }
    }

    public class FlyRocketPowered : IFlyBehavior
    {
        public void Fly()
        {
            Console.WriteLine("I'm flying with a rocket!");
        }
    }

    #endregion FlyBehavior

    #region QuackBehavior

    public interface IQuackBehavior
    {
        void Quack();
    }

    // Name it LoadQuack to avoid conflict with method name
    public class LoudQuack : IQuackBehavior
    {
        public void Quack()
        {
            Console.WriteLine("LoudQuack");
        }
    }

    public class MuteQuack : IQuackBehavior
    {
        public void Quack()
        {
            Console.WriteLine("<< Silence >>");
        }
    }

    public class Squeak : IQuackBehavior
    {
        public void Quack()
        {
            Console.WriteLine("Squeak");
        }
    }

    #endregion QuackBehavior
```

## Реализация на JAVA ##

```java
    TODO
```