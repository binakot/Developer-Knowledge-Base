# Компоновщик (Composite) #

Паттерн Компоновщик объединяет объекты в древовидные структуры для представления иерархий "часть/целое".
Компоновщик позволяет клиенту выполнять однородные операции с отдельными объектами и их совокупностями.

![UML](/design_patterns/structural/composite_UML.gif)

* Component - компонент

* Leaf - лист

* Composite - составной объект

[Статья на Википедии](https://ru.wikipedia.org/wiki/Компоновщик_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Composite Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create a tree structure
            Composite root = new Composite("root");
            root.Add(new Leaf("Leaf A"));
            root.Add(new Leaf("Leaf B"));

            Composite comp = new Composite("Composite X");
            comp.Add(new Leaf("Leaf XA"));
            comp.Add(new Leaf("Leaf XB"));

            root.Add(comp);
            root.Add(new Leaf("Leaf C"));

            // Add and remove a leaf
            Leaf leaf = new Leaf("Leaf D");
            root.Add(leaf);
            root.Remove(leaf);

            // Recursively display tree
            root.Display(1);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Component' abstract class
    /// </summary>
    internal abstract class Component
    {
        protected string name;

        // Constructor
        public Component(string name)
        {
            this.name = name;
        }

        public abstract void Add(Component c);

        public abstract void Remove(Component c);

        public abstract void Display(int depth);
    }

    /// <summary>
    /// The 'Composite' class
    /// </summary>
    internal class Composite : Component
    {
        private List<Component> children = new List<Component>();

        // Constructor
        public Composite(string name)
            : base(name)
        {
        }

        public override void Add(Component component)
        {
            children.Add(component);
        }

        public override void Remove(Component component)
        {
            children.Remove(component);
        }

        public override void Display(int depth)
        {
            Console.WriteLine(new String('-', depth) + name);

            // Recursively display child nodes
            foreach (Component component in children)
            {
                component.Display(depth + 2);
            }
        }
    }

    /// <summary>
    /// The 'Leaf' class
    /// </summary>
    internal class Leaf : Component
    {
        // Constructor
        public Leaf(string name)
            : base(name)
        {
        }

        public override void Add(Component c)
        {
            Console.WriteLine("Cannot add to a leaf");
        }

        public override void Remove(Component c)
        {
            Console.WriteLine("Cannot remove from a leaf");
        }

        public override void Display(int depth)
        {
            Console.WriteLine(new String('-', depth) + name);
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Composite Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create a tree structure
            CompositeElement root = new CompositeElement("Picture");
            root.Add(new PrimitiveElement("Red Line"));
            root.Add(new PrimitiveElement("Blue Circle"));
            root.Add(new PrimitiveElement("Green Box"));

            // Create a branch
            CompositeElement comp = new CompositeElement("Two Circles");
            comp.Add(new PrimitiveElement("Black Circle"));
            comp.Add(new PrimitiveElement("White Circle"));
            root.Add(comp);

            // Add and remove a PrimitiveElement
            PrimitiveElement pe = new PrimitiveElement("Yellow Line");
            root.Add(pe);
            root.Remove(pe);

            // Recursively display nodes
            root.Display(1);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Component' Treenode
    /// </summary>
    internal abstract class DrawingElement
    {
        protected string name;

        // Constructor
        public DrawingElement(string name)
        {
            this.name = name;
        }

        public abstract void Add(DrawingElement d);

        public abstract void Remove(DrawingElement d);

        public abstract void Display(int indent);
    }

    /// <summary>
    /// The 'Leaf' class
    /// </summary>
    internal class PrimitiveElement : DrawingElement
    {
        // Constructor
        public PrimitiveElement(string name)
            : base(name)
        {
        }

        public override void Add(DrawingElement c)
        {
            Console.WriteLine(
                "Cannot add to a PrimitiveElement");
        }

        public override void Remove(DrawingElement c)
        {
            Console.WriteLine(
                "Cannot remove from a PrimitiveElement");
        }

        public override void Display(int indent)
        {
            Console.WriteLine(
                new String('-', indent) + " " + name);
        }
    }

    /// <summary>
    /// The 'Composite' class
    /// </summary>
    internal class CompositeElement : DrawingElement
    {
        private List<DrawingElement> elements = new List<DrawingElement>();

        // Constructor
        public CompositeElement(string name)
            : base(name)
        {
        }

        public override void Add(DrawingElement d)
        {
            elements.Add(d);
        }

        public override void Remove(DrawingElement d)
        {
            elements.Remove(d);
        }

        public override void Display(int indent)
        {
            Console.WriteLine(new String('-', indent) +
                "+ " + name);

            // Display each child element on this node
            foreach (DrawingElement d in elements)
            {
                d.Display(indent + 2);
            }
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Composite Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Build a tree of shapes
            var root = new TreeNode<Shape> { Node = new Shape("Picture") };

            root.Add(new Shape("Red Line"));
            root.Add(new Shape("Blue Circle"));
            root.Add(new Shape("Green Box"));

            var branch = root.Add(new Shape("Two Circles"));
            branch.Add(new Shape("Black Circle"));
            branch.Add(new Shape("White Circle"));

            // Add, remove, and add a shape
            var shape = new Shape("Yellow Line");
            root.Add(shape);
            root.Remove(shape);
            root.Add(shape);

            // Display tree using static method
            TreeNode<Shape>.Display(root, 1);

            Console.ReadKey();
        }
    }

    /// <summary>
    /// Generic tree node class
    /// </summary>
    /// <typeparam name="T">Node type</typeparam>
    internal class TreeNode<T> where T : IComparable<T>
    {
        private List<TreeNode<T>> children = new List<TreeNode<T>>();

        // Add a child tree node
        public TreeNode<T> Add(T child)
        {
            var newNode = new TreeNode<T> { Node = child };
            children.Add(newNode);
            return newNode;
        }

        // Remove a child tree node
        public void Remove(T child)
        {
            foreach (var treeNode in children)
            {
                if (treeNode.Node.CompareTo(child) == 0)
                {
                    children.Remove(treeNode);
                    return;
                }
            }
        }

        // Gets or sets the node
        public T Node { get; set; }

        // Gets treenode children
        public List<TreeNode<T>> Children
        {
            get { return children; }
        }

        // Recursively displays node and its children
        public static void Display(TreeNode<T> node, int indentation)
        {
            string line = new String('-', indentation);
            Console.WriteLine(line + " " + node.Node);

            node.Children.ForEach(n => Display(n, indentation + 1));
        }
    }

    /// <summary>
    /// Shape class
    /// <remarks>
    /// Implements generic IComparable interface
    /// </remarks>
    /// </summary>

    internal class Shape : IComparable<Shape>
    {
        private string name;

        // Constructor
        public Shape(string name)
        {
            this.name = name;
        }

        public override string ToString()
        {
            return name;
        }

        // IComparable<Shape> Member
        public int CompareTo(Shape other)
        {
            return (this == other) ? 0 : -1;
        }
    }
```

## Реализация на C# (Head First) ##

```csharp
    internal class MenuTestDrive
    {
        private static void Main(string[] args)
        {
            MenuComponent pancakeHouseMenu =
                new Menu { Name = "PANCAKE HOUSE MENU", Description = "Breakfast" };
            MenuComponent dinerMenu =
                new Menu { Name = "DINER MENU", Description = "Lunch" };
            MenuComponent cafeMenu =
                new Menu { Name = "CAFE MENU", Description = "Dinner" };
            MenuComponent dessertMenu =
                new Menu { Name = "DESSERT MENU", Description = "Dessert of course!" };
            MenuComponent coffeeMenu =
                new Menu { Name = "COFFEE MENU", Description = "Stuff to go with your afternoon coffee" };

            MenuComponent allMenus = new Menu { Name = "ALL MENUS", Description = "All menus combined" };

            allMenus.Add(pancakeHouseMenu);
            allMenus.Add(dinerMenu);
            allMenus.Add(cafeMenu);

            pancakeHouseMenu.Add(new MenuItem
            {
                Name = "K&B's Pancake Breakfast",
                Description = "Pancakes with scrambled eggs, and toast",
                Vegetarian = true,
                Price = 2.99
            });
            pancakeHouseMenu.Add(new MenuItem
            {
                Name = "Regular Pancake Breakfast",
                Description = "Pancakes with fried eggs, sausage",
                Vegetarian = false,
                Price = 2.99
            });
            pancakeHouseMenu.Add(new MenuItem
            {
                Name = "Blueberry Pancakes",
                Description = "Pancakes made with fresh blueberries, and blueberry syrup",
                Vegetarian = true,
                Price = 3.49
            });
            pancakeHouseMenu.Add(new MenuItem
            {
                Name = "Waffles",
                Description = "Waffles, with your choice of blueberries or strawberries",
                Vegetarian = true,
                Price = 3.59
            });

            dinerMenu.Add(new MenuItem
            {
                Name = "Vegetarian BLT",
                Description = "(Fakin') Bacon with lettuce & tomato on whole wheat",
                Vegetarian = true,
                Price = 2.99
            }); ;
            dinerMenu.Add(new MenuItem
            {
                Name = "BLT",
                Description = "Bacon with lettuce & tomato on whole wheat",
                Vegetarian = false,
                Price = 2.99
            });
            dinerMenu.Add(new MenuItem
            {
                Name = "Soup of the day",
                Description = "A bowl of the soup of the day, with a side of potato salad",
                Vegetarian = false,
                Price = 3.29
            });
            dinerMenu.Add(new MenuItem
            {
                Name = "Hotdog",
                Description = "A hot dog, with saurkraut, relish, onions, topped with cheese",
                Vegetarian = false,
                Price = 3.05
            });
            dinerMenu.Add(new MenuItem
            {
                Name = "Steamed Veggies and Brown Rice",
                Description = "Steamed vegetables over brown rice",
                Vegetarian = true,
                Price = 3.99
            });
            dinerMenu.Add(new MenuItem
            {
                Name = "Pasta",
                Description = "Spaghetti with Marinara Sauce, and a slice of sourdough bread",
                Vegetarian = true,
                Price = 3.89
            });

            dinerMenu.Add(dessertMenu);

            dessertMenu.Add(new MenuItem
            {
                Name = "Apple Pie",
                Description = "Apple pie with a flakey crust, topped with vanilla icecream",
                Vegetarian = true,
                Price = 1.59
            });
            dessertMenu.Add(new MenuItem
            {
                Name = "Cheesecake",
                Description = "Creamy New York cheesecake, with a chocolate graham crust",
                Vegetarian = true,
                Price = 1.99
            });
            dessertMenu.Add(new MenuItem
            {
                Name = "Sorbet",
                Description = "A scoop of raspberry and a scoop of lime",
                Vegetarian = true,
                Price = 1.89
            });
            cafeMenu.Add(new MenuItem
            {
                Name = "Veggie Burger and Air Fries",
                Description = "Veggie burger on a whole wheat bun, lettuce, tomato, and fries",
                Vegetarian = true,
                Price = 3.99
            });
            cafeMenu.Add(new MenuItem
            {
                Name = "Soup of the day",
                Description = "A cup of the soup of the day, with a side salad",
                Vegetarian = false,
                Price = 3.69
            });
            cafeMenu.Add(new MenuItem
            {
                Name = "Burrito",
                Description = "A large burrito, with whole pinto beans, salsa, guacamole",
                Vegetarian = true,
                Price = 4.29
            });

            cafeMenu.Add(coffeeMenu);

            coffeeMenu.Add(new MenuItem
            {
                Name = "Coffee Cake",
                Description = "Crumbly cake topped with cinnamon and walnuts",
                Vegetarian = true,
                Price = 1.59
            });
            coffeeMenu.Add(new MenuItem
            {
                Name = "Bagel",
                Description = "Flavors include sesame, poppyseed, cinnamon raisin, pumpkin",
                Vegetarian = false,
                Price = 0.69
            });
            coffeeMenu.Add(new MenuItem
            {
                Name = "Biscotti",
                Description = "Three almond or hazelnut biscotti cookies",
                Vegetarian = true,
                Price = 0.89
            });

            Console.WriteLine("\nVEGETARIAN MENU\n----");

            var waitress = new Waitress();
            waitress.PrintVegetarianMenu(allMenus);

            // Wait for user
            Console.ReadKey();
        }
    }

    #region Waitress

    public class Waitress
    {
        public void PrintVegetarianMenu(MenuComponent menuComponent)
        {
            IEnumerator<MenuComponent> _iterator = menuComponent.CreateIterator();

            while (_iterator.MoveNext())
            {
                MenuComponent menu = _iterator.Current;
                if (menu is Menu)
                {
                    PrintVegetarianMenu(menu);
                }
                else if (menu.Vegetarian)
                {
                    menu.Print();
                }
            }
        }
    }

    #endregion Waitress

    #region Menu and MenuItems

    public abstract class MenuComponent
    {
        public virtual void Add(MenuComponent menuComponent)
        {
            throw new NotSupportedException();
        }

        public virtual void Remove(MenuComponent menuComponent)
        {
            throw new NotSupportedException();
        }

        public virtual MenuComponent GetChild(int i)
        {
            throw new NotSupportedException();
        }

        public string Name { get; set; }

        public string Description { get; set; }

        public double Price { get; set; }

        public bool Vegetarian { get; set; }

        public abstract IEnumerator<MenuComponent> CreateIterator();

        public virtual void Print()
        {
            throw new NotSupportedException();
        }
    }

    public class Menu : MenuComponent
    {
        private List<MenuComponent> _menuComponents = new List<MenuComponent>();

        public override void Add(MenuComponent menuComponent)
        {
            _menuComponents.Add(menuComponent);
        }

        public override void Remove(MenuComponent menuComponent)
        {
            _menuComponents.Remove(menuComponent);
        }

        public override MenuComponent GetChild(int i)
        {
            return _menuComponents[i];
        }

        public override void Print()
        {
            Console.Write(Name);
            Console.Write(", " + Description);
            Console.WriteLine("---------------------");

            foreach (MenuComponent mc in _menuComponents)
            {
                mc.Print();
            }
        }

        public override IEnumerator<MenuComponent> CreateIterator()
        {
            return _menuComponents.GetEnumerator();
        }
    }

    public class MenuItem : MenuComponent
    {
        public override IEnumerator<MenuComponent> CreateIterator()
        {
            return null;
        }

        public override void Print()
        {
            Console.Write("  " + Name);
            if (Vegetarian)
            {
                Console.Write("(v)");
            }
            Console.WriteLine(", " + Price);
            Console.WriteLine("     -- " + Description);
        }
    }

    #endregion Menu and MenuItems
```

## Реализация на JAVA ##

```java
    TODO
```