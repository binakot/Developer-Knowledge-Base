# Итератор (Iterator) #

Также известен как Курсор (Cursor).

Паттерн Итератор предоставляет механизм последовательного перебора элементов коллекции
без раскрытия ее внутреннего представления.

![UML](/design_patterns/behavioral/iterator_UML.svg?raw=true)

* Iterator - абстрактный итератор

* ConcreteIterator - конкретный итератор

* Aggregate - абстрактный агрегат

* ConcreteAggregate - конкретный агрегат

[Статья на Википедии](https://ru.wikipedia.org/wiki/Итератор_(шаблон_проектирования))

Пакет _java.util_ содержит интерфейс _Iterator_, который следует использовать вместо реализации своего собственного.
Если реализация метода _remove_ не требуется - инициируйте при его вызове исключение _UnsupportedOperationException_.
Метод _remove_ не является потоко-безопасным!

Если требуется более мощный интерфейс итератора, следует обратить внимание на _java.util.ListIterator_.

Также следует избегать устаревшего интерфейса итератора _java.util.Enumeration_.

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Iterator Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            ConcreteAggregate a = new ConcreteAggregate();
            a[0] = "Item A";
            a[1] = "Item B";
            a[2] = "Item C";
            a[3] = "Item D";

            // Create Iterator and provide aggregate
            ConcreteIterator i = new ConcreteIterator(a);

            Console.WriteLine("Iterating over collection:");

            object item = i.First();
            while (item != null)
            {
                Console.WriteLine(item);
                item = i.Next();
            }

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Aggregate' abstract class
    /// </summary>
    internal abstract class Aggregate
    {
        public abstract Iterator CreateIterator();
    }

    /// <summary>
    /// The 'ConcreteAggregate' class
    /// </summary>
    internal class ConcreteAggregate : Aggregate
    {
        private ArrayList items = new ArrayList();

        public override Iterator CreateIterator()
        {
            return new ConcreteIterator(this);
        }

        // Gets item count
        public int Count
        {
            get { return items.Count; }
        }

        // Indexer
        public object this[int index]
        {
            get { return items[index]; }
            set { items.Insert(index, value); }
        }
    }

    /// <summary>
    /// The 'Iterator' abstract class
    /// </summary>
    internal abstract class Iterator
    {
        public abstract object First();

        public abstract object Next();

        public abstract bool IsDone();

        public abstract object CurrentItem();
    }

    /// <summary>
    /// The 'ConcreteIterator' class
    /// </summary>
    internal class ConcreteIterator : Iterator
    {
        private ConcreteAggregate aggregate;
        private int current = 0;

        // Constructor
        public ConcreteIterator(ConcreteAggregate aggregate)
        {
            this.aggregate = aggregate;
        }

        // Gets first iteration item
        public override object First()
        {
            return aggregate[0];
        }

        // Gets next iteration item
        public override object Next()
        {
            object ret = null;
            if (current < aggregate.Count - 1)
            {
                ret = aggregate[++current];
            }

            return ret;
        }

        // Gets current iteration item
        public override object CurrentItem()
        {
            return aggregate[current];
        }

        // Gets whether iterations are complete
        public override bool IsDone()
        {
            return current >= aggregate.Count;
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Iterator Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Build a collection
            Collection collection = new Collection();
            collection[0] = new Item("Item 0");
            collection[1] = new Item("Item 1");
            collection[2] = new Item("Item 2");
            collection[3] = new Item("Item 3");
            collection[4] = new Item("Item 4");
            collection[5] = new Item("Item 5");
            collection[6] = new Item("Item 6");
            collection[7] = new Item("Item 7");
            collection[8] = new Item("Item 8");

            // Create iterator
            Iterator iterator = new Iterator(collection);

            // Skip every other item
            iterator.Step = 2;

            Console.WriteLine("Iterating over collection:");

            for (Item item = iterator.First();
                !iterator.IsDone; item = iterator.Next())
            {
                Console.WriteLine(item.Name);
            }

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// A collection item
    /// </summary>
    internal class Item
    {
        private string name;

        // Constructor
        public Item(string name)
        {
            this.name = name;
        }

        // Gets name
        public string Name
        {
            get { return name; }
        }
    }

    /// <summary>
    /// The 'Aggregate' interface
    /// </summary>
    internal interface IAbstractCollection
    {
        Iterator CreateIterator();
    }

    /// <summary>
    /// The 'ConcreteAggregate' class
    /// </summary>
    internal class Collection : IAbstractCollection
    {
        private ArrayList items = new ArrayList();

        public Iterator CreateIterator()
        {
            return new Iterator(this);
        }

        // Gets item count
        public int Count
        {
            get { return items.Count; }
        }

        // Indexer
        public object this[int index]
        {
            get { return items[index]; }
            set { items.Add(value); }
        }
    }

    /// <summary>
    /// The 'Iterator' interface
    /// </summary>
    internal interface IAbstractIterator
    {
        Item First();

        Item Next();

        bool IsDone { get; }
        Item CurrentItem { get; }
    }

    /// <summary>
    /// The 'ConcreteIterator' class
    /// </summary>
    internal class Iterator : IAbstractIterator
    {
        private Collection collection;
        private int current = 0;
        private int step = 1;

        // Constructor
        public Iterator(Collection collection)
        {
            this.collection = collection;
        }

        // Gets first item
        public Item First()
        {
            current = 0;
            return collection[current] as Item;
        }

        // Gets next item
        public Item Next()
        {
            current += step;
            if (!IsDone)
                return collection[current] as Item;
            else
                return null;
        }

        // Gets or sets stepsize
        public int Step
        {
            get { return step; }
            set { step = value; }
        }

        // Gets current iterator item
        public Item CurrentItem
        {
            get { return collection[current] as Item; }
        }

        // Gets whether iteration is complete
        public bool IsDone
        {
            get { return current >= collection.Count; }
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Iterator Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create and item collection
            var collection = new ItemCollection<Item>
              {
                new Item{ Name = "Item 0"},
                new Item{ Name = "Item 1"},
                new Item{ Name = "Item 2"},
                new Item{ Name = "Item 3"},
                new Item{ Name = "Item 4"},
                new Item{ Name = "Item 5"},
                new Item{ Name = "Item 6"},
                new Item{ Name = "Item 7"},
                new Item{ Name = "Item 8"}
              };

            Console.WriteLine("Iterate front to back");
            foreach (var item in collection)
            {
                Console.WriteLine(item.Name);
            }

            Console.WriteLine("\nIterate back to front");
            foreach (var item in collection.BackToFront)
            {
                Console.WriteLine(item.Name);
            }
            Console.WriteLine();

            // Iterate given range and step over even ones
            Console.WriteLine("\nIterate range (1-7) in steps of 2");
            foreach (var item in collection.FromToStep(1, 7, 2))
            {
                Console.WriteLine(item.Name);
            }
            Console.WriteLine();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'ConcreteAggregate' class
    /// </summary>
    /// <typeparam name="T">Collection item type</typeparam>
    internal class ItemCollection<T> : IEnumerable<T>
    {
        private List<T> items = new List<T>();

        public void Add(T t)
        {
            items.Add(t);
        }

        // The 'ConcreteIterator'
        public IEnumerator<T> GetEnumerator()
        {
            for (int i = 0; i < Count; i++)
            {
                yield return items[i];
            }
        }

        public IEnumerable<T> FrontToBack
        {
            get { return this; }
        }

        public IEnumerable<T> BackToFront
        {
            get
            {
                for (int i = Count - 1; i >= 0; i--)
                {
                    yield return items[i];
                }
            }
        }

        public IEnumerable<T> FromToStep(int from, int to, int step)
        {
            for (int i = from; i <= to; i = i + step)
            {
                yield return items[i];
            }
        }

        // Gets number of items
        public int Count
        {
            get { return items.Count; }
        }

        // System.Collections.IEnumerable member implementation
        IEnumerator IEnumerable.GetEnumerator()
        {
            return GetEnumerator();
        }
    }

    /// <summary>
    /// The collection item
    /// </summary>
    internal class Item
    {
        // Gets or sets item name
        public string Name { get; set; }
    }
```

## Реализация на C# (Head First) ##

```csharp
    internal class MenuTestDrive
    {
        private static void Main(string[] args)
        {
            var pancakeHouseMenu = new PancakeHouseMenu();
            var dinerMenu = new DinerMenu();
            var cafeMenu = new CafeMenu();

            var waitress = new Waitress(pancakeHouseMenu, dinerMenu, cafeMenu);

            waitress.PrintMenu();
            waitress.PrintVegetarianMenu();

            Console.WriteLine("\nCustomer asks, is the Hotdog vegetarian?");
            Console.Write("Waitress says: ");
            if (waitress.IsItemVegetarian("Hotdog"))
            {
                Console.WriteLine("Yes");
            }
            else
            {
                Console.WriteLine("No");
            }

            Console.WriteLine("\nCustomer asks, are the Waffles vegetarian?");
            Console.Write("Waitress says: ");
            if (waitress.IsItemVegetarian("Waffles"))
            {
                Console.WriteLine("Yes");
            }
            else
            {
                Console.WriteLine("No");
            }

            // Wait for user
            Console.ReadKey();
        }
    }

    #region Waitress

    public class Waitress
    {
        private IMenu _pancakeHouseMenu;
        private IMenu _dinerMenu;
        private IMenu _cafeMenu;

        public Waitress(IMenu pancakeHouseMenu, IMenu dinerMenu, IMenu cafeMenu)
        {
            this._pancakeHouseMenu = pancakeHouseMenu;
            this._dinerMenu = dinerMenu;
            this._cafeMenu = cafeMenu;
        }

        public void PrintMenu()
        {
            IEnumerator<MenuItem> pancakeIterator = _pancakeHouseMenu.CreateIterator();
            IEnumerator<MenuItem> dinerIterator = _dinerMenu.CreateIterator();
            IEnumerator<MenuItem> cafeIterator = _cafeMenu.CreateIterator();

            Console.WriteLine("MENU\n----\nBREAKFAST");
            PrintMenu(pancakeIterator);

            Console.WriteLine("\nLUNCH");
            PrintMenu(dinerIterator);

            Console.WriteLine("\nDINNER");
            PrintMenu(cafeIterator);
        }

        private void PrintMenu(IEnumerator<MenuItem> iterator)
        {
            while (iterator.MoveNext())
            {
                MenuItem menuItem = (MenuItem)iterator.Current;

                Console.Write(menuItem.Name + ", ");
                Console.Write(menuItem.Price + " -- ");
                Console.WriteLine(menuItem.Description);
            }
        }

        public void PrintVegetarianMenu()
        {
            Console.WriteLine("\nVEGETARIAN MENU\n---------------");
            PrintVegetarianMenu(_pancakeHouseMenu.CreateIterator());
            PrintVegetarianMenu(_dinerMenu.CreateIterator());
            PrintVegetarianMenu(_cafeMenu.CreateIterator());
        }

        public bool IsItemVegetarian(string name)
        {
            IEnumerator<MenuItem> pancakeIterator = _pancakeHouseMenu.CreateIterator();
            if (IsVegetarian(name, pancakeIterator))
            {
                return true;
            }
            IEnumerator<MenuItem> dinerIterator = _dinerMenu.CreateIterator();
            if (IsVegetarian(name, dinerIterator))
            {
                return true;
            }
            IEnumerator<MenuItem> cafeIterator = _cafeMenu.CreateIterator();
            if (IsVegetarian(name, cafeIterator))
            {
                return true;
            }
            return false;
        }

        private void PrintVegetarianMenu(IEnumerator<MenuItem> iterator)
        {
            while (iterator.MoveNext())
            {
                MenuItem menuItem = iterator.Current;
                if (menuItem.Vegetarian)
                {
                    Console.Write(menuItem.Name + ", ");
                    Console.Write(menuItem.Price + " -- ");
                    Console.WriteLine(menuItem.Description);
                }
            }
        }

        private bool IsVegetarian(string name, IEnumerator<MenuItem> iterator)
        {
            while (iterator.MoveNext())
            {
                MenuItem menuItem = iterator.Current;
                if (menuItem.Name == name)
                {
                    if (menuItem.Vegetarian)
                    {
                        return true;
                    }
                }
            }
            return false;
        }
    }

    #endregion Waitress

    #region Menu and MenuItems

    public interface IMenu
    {
        IEnumerator<MenuItem> CreateIterator();
    }

    public class MenuItem
    {
        public string Name { get; private set; }
        public string Description { get; private set; }
        public bool Vegetarian { get; private set; }
        public double Price { get; private set; }

        public MenuItem(string name, string description, bool vegetarian, double price)
        {
            this.Name = name;
            this.Description = description;
            this.Vegetarian = vegetarian;
            this.Price = price;
        }
    }

    public class PancakeHouseMenu : IMenu
    {
        private List<MenuItem> menuItems = new List<MenuItem>();

        public PancakeHouseMenu()
        {
            //menuItems = new ArrayList();

            AddItem("K&B's Pancake Breakfast",
                "Pancakes with scrambled eggs, and toast",
                true,
                2.99);

            AddItem("Regular Pancake Breakfast",
                "Pancakes with fried eggs, sausage",
                false,
                2.99);

            AddItem("Blueberry Pancakes",
                "Pancakes made with fresh blueberries, and blueberry syrup",
                true,
                3.49);

            AddItem("Waffles",
                "Waffles, with your choice of blueberries or strawberries",
                true,
                3.59);
        }

        public void AddItem(string name, string description, bool vegetarian, double price)
        {
            MenuItem menuItem = new MenuItem(name, description, vegetarian, price);
            menuItems.Add(menuItem);
        }

        public IEnumerator<MenuItem> CreateIterator()
        {
            return menuItems.GetEnumerator();
        }

        // other menu methods here
    }

    public class CafeMenu : IMenu
    {
        private Dictionary<string, MenuItem> _menuItems =
            new Dictionary<string, MenuItem>();

        public CafeMenu()
        {
            AddItem("Veggie Burger and Air Fries",
                "Veggie burger on a whole wheat bun, lettuce, tomato, and fries",
                true, 3.99);
            AddItem("Soup of the day",
                "A cup of the soup of the day, with a side salad",
                false, 3.69);
            AddItem("Burrito",
                "A large burrito, with whole pinto beans, salsa, guacamole",
                true, 4.29);
        }

        public void AddItem(String name, String description,
            bool vegetarian, double price)
        {
            MenuItem menuItem = new MenuItem(name, description, vegetarian, price);
            _menuItems.Add(menuItem.Name, menuItem);
        }

        public IEnumerator<MenuItem> CreateIterator()
        {
            return _menuItems.Values.GetEnumerator();
        }
    }

    public class DinerMenu : IMenu
    {
        private List<MenuItem> _menuItems = new List<MenuItem>();

        public DinerMenu()
        {
            AddItem("Vegetarian BLT",
                "(Fakin') Bacon with lettuce & tomato on whole wheat", true, 2.99);
            AddItem("BLT",
                "Bacon with lettuce & tomato on whole wheat", false, 2.99);
            AddItem("Soup of the day",
                "Soup of the day, with a side of potato salad", false, 3.29);
            AddItem("Hotdog",
                "A hot dog, with saurkraut, relish, onions, topped with cheese",
                false, 3.05);
            AddItem("Steamed Veggies and Brown Rice",
                "A medly of steamed vegetables over brown rice", true, 3.99);
            AddItem("Pasta",
                "Spaghetti with Marinara Sauce, and a slice of sourdough bread",
                true, 3.89);
        }

        public void AddItem(String name, String description,
            bool vegetarian, double price)
        {
            MenuItem menuItem = new MenuItem(name, description, vegetarian, price);
            _menuItems.Add(menuItem);
        }

        public IEnumerator<MenuItem> CreateIterator()
        {
            return _menuItems.GetEnumerator();
        }

        // other menu methods here
    }

    #endregion Menu and MenuItems
```

## Реализация на JAVA ##

```java
    TODO
```