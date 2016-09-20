# Прототип (Prototype) #

Паттерн Прототип используется в тех случаях, когда создание экземпляра класса требует больших затрат ресурсов или занимает много времени.

![UML](https://bitbucket.org/firstmk/pmk/wiki/design_patterns/creational/prototype_UML.gif)

* Prototype - абстрактный прототип

* ConcretePrototype - конкретный прототип

* Client - клиент

[Статья на Википедии](https://ru.wikipedia.org/wiki/Прототип_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Prototype Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create two instances and clone each

            ConcretePrototype1 p1 = new ConcretePrototype1("I");
            ConcretePrototype1 c1 = (ConcretePrototype1)p1.Clone();
            Console.WriteLine("Cloned: {0}", c1.Id);

            ConcretePrototype2 p2 = new ConcretePrototype2("II");
            ConcretePrototype2 c2 = (ConcretePrototype2)p2.Clone();
            Console.WriteLine("Cloned: {0}", c2.Id);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Prototype' abstract class
    /// </summary>
    internal abstract class Prototype
    {
        private string id;

        // Constructor
        public Prototype(string id)
        {
            this.id = id;
        }

        // Gets id
        public string Id
        {
            get { return id; }
        }

        public abstract Prototype Clone();
    }

    /// <summary>
    /// A 'ConcretePrototype' class
    /// </summary>
    internal class ConcretePrototype1 : Prototype
    {
        // Constructor
        public ConcretePrototype1(string id)
            : base(id)
        {
        }

        // Returns a shallow copy
        public override Prototype Clone()
        {
            return (Prototype)this.MemberwiseClone();
        }
    }

    /// <summary>
    /// A 'ConcretePrototype' class
    /// </summary>
    internal class ConcretePrototype2 : Prototype
    {
        // Constructor
        public ConcretePrototype2(string id)
            : base(id)
        {
        }

        // Returns a shallow copy
        public override Prototype Clone()
        {
            return (Prototype)this.MemberwiseClone();
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Prototype Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            ColorManager colormanager = new ColorManager();

            // Initialize with standard colors
            colormanager["red"] = new Color(255, 0, 0);
            colormanager["green"] = new Color(0, 255, 0);
            colormanager["blue"] = new Color(0, 0, 255);

            // User adds personalized colors
            colormanager["angry"] = new Color(255, 54, 0);
            colormanager["peace"] = new Color(128, 211, 128);
            colormanager["flame"] = new Color(211, 34, 20);

            // User clones selected colors
            Color color1 = colormanager["red"].Clone() as Color;
            Color color2 = colormanager["peace"].Clone() as Color;
            Color color3 = colormanager["flame"].Clone() as Color;

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Prototype' abstract class
    /// </summary>
    internal abstract class ColorPrototype
    {
        public abstract ColorPrototype Clone();
    }

    /// <summary>
    /// The 'ConcretePrototype' class
    /// </summary>
    internal class Color : ColorPrototype
    {
        private int red;
        private int green;
        private int blue;

        // Constructor
        public Color(int red, int green, int blue)
        {
            this.red = red;
            this.green = green;
            this.blue = blue;
        }

        // Create a shallow copy
        public override ColorPrototype Clone()
        {
            Console.WriteLine(
                "Cloning color RGB: {0,3},{1,3},{2,3}",
                red, green, blue);

            return this.MemberwiseClone() as ColorPrototype;
        }
    }

    /// <summary>
    /// Prototype manager
    /// </summary>
    internal class ColorManager
    {
        private Dictionary<string, ColorPrototype> colors =
            new Dictionary<string, ColorPrototype>();

        // Indexer
        public ColorPrototype this[string key]
        {
            get { return colors[key]; }
            set { colors.Add(key, value); }
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Prototype Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            var colormanager = new ColorManager();

            // Initialize with standard colors
            colormanager[ColorType.Red] = new Color { Red = 255, Blue = 0, Green = 0 };
            colormanager[ColorType.Green] = new Color { Red = 0, Blue = 255, Green = 0 };
            colormanager[ColorType.Blue] = new Color { Red = 0, Blue = 0, Green = 255 };

            // User adds personalized colors
            colormanager[ColorType.Angry] = new Color { Red = 255, Blue = 54, Green = 0 };
            colormanager[ColorType.Peace] = new Color { Red = 128, Blue = 211, Green = 128 };
            colormanager[ColorType.Flame] = new Color { Red = 211, Blue = 34, Green = 20 };

            // User uses selected colors
            var color1 = colormanager[ColorType.Red].Clone() as Color;
            var color2 = colormanager[ColorType.Peace].Clone() as Color;

            // Creates a "deep copy"
            var color3 = colormanager[ColorType.Flame].Clone(false) as Color;

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'ConcretePrototype' class
    /// </summary>
    [Serializable]
    internal class Color : ICloneable
    {
        // Gets or sets red value
        public byte Red { get; set; }

        // Gets or sets green value
        public byte Green { get; set; }

        // Gets or sets blue channel
        public byte Blue { get; set; }

        // Returns shallow or deep copy
        public object Clone(bool shallow)
        {
            return shallow ? Clone() : DeepCopy();
        }

        // Creates a shallow copy
        public object Clone()
        {
            Console.WriteLine(
                "Shallow copy of color RGB: {0,3},{1,3},{2,3}",
                Red, Green, Blue);

            return this.MemberwiseClone();
        }

        // Creates a deep copy
        public object DeepCopy()
        {
            var stream = new MemoryStream();
            var formatter = new BinaryFormatter();

            formatter.Serialize(stream, this);
            stream.Seek(0, SeekOrigin.Begin);

            object copy = formatter.Deserialize(stream);
            stream.Close();

            Console.WriteLine(
                "*Deep*  copy of color RGB: {0,3},{1,3},{2,3}",
                (copy as Color).Red,
                (copy as Color).Green,
                (copy as Color).Blue);

            return copy;
        }
    }

    /// <summary>
    /// Type-safe prototype manager
    /// </summary>
    internal class ColorManager
    {
        private Dictionary<ColorType, Color> colors = new Dictionary<ColorType, Color>();

        // Gets or sets color
        public Color this[ColorType type]
        {
            get { return colors[type]; }
            set { colors.Add(type, value); }
        }
    }

    /// <summary>
    /// Color type enumerations
    /// </summary>
    internal enum ColorType
    {
        Red,
        Green,
        Blue,

        Angry,
        Peace,
        Flame
    }
```

## Реализация на JAVA ##

```java
    TODO
```