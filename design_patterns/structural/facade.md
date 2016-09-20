# Фасад (Facade) #

Паттерн Фасад предоставляет унифицированный интерфейс к группе интерфейсов подсистемы.
Фасад определяет высокоуровневый интерфейс, упрощающий работу с подсистемой.

![UML](/design_patterns/structural/facade_UML.svg)

* Facade - фасад

* Modules - классы подсистемы

[Статья на Википедии](https://ru.wikipedia.org/wiki/Фасад_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Facade Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        public static void Main()
        {
            Facade facade = new Facade();

            facade.MethodA();
            facade.MethodB();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subsystem ClassA' class
    /// </summary>
    internal class SubSystemOne
    {
        public void MethodOne()
        {
            Console.WriteLine(" SubSystemOne Method");
        }
    }

    /// <summary>
    /// The 'Subsystem ClassB' class
    /// </summary>
    internal class SubSystemTwo
    {
        public void MethodTwo()
        {
            Console.WriteLine(" SubSystemTwo Method");
        }
    }

    /// <summary>
    /// The 'Subsystem ClassC' class
    /// </summary>
    internal class SubSystemThree
    {
        public void MethodThree()
        {
            Console.WriteLine(" SubSystemThree Method");
        }
    }

    /// <summary>
    /// The 'Subsystem ClassD' class
    /// </summary>
    internal class SubSystemFour
    {
        public void MethodFour()
        {
            Console.WriteLine(" SubSystemFour Method");
        }
    }

    /// <summary>
    /// The 'Facade' class
    /// </summary>
    internal class Facade
    {
        private SubSystemOne one;
        private SubSystemTwo two;
        private SubSystemThree three;
        private SubSystemFour four;

        public Facade()
        {
            one = new SubSystemOne();
            two = new SubSystemTwo();
            three = new SubSystemThree();
            four = new SubSystemFour();
        }

        public void MethodA()
        {
            Console.WriteLine("\nMethodA() ---- ");
            one.MethodOne();
            two.MethodTwo();
            four.MethodFour();
        }

        public void MethodB()
        {
            Console.WriteLine("\nMethodB() ---- ");
            two.MethodTwo();
            three.MethodThree();
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Facade Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Facade
            Mortgage mortgage = new Mortgage();

            // Evaluate mortgage eligibility for customer
            Customer customer = new Customer("Ann McKinsey");
            bool eligible = mortgage.IsEligible(customer, 125000);

            Console.WriteLine("\n" + customer.Name +
                    " has been " + (eligible ? "Approved" : "Rejected"));

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subsystem ClassA' class
    /// </summary>
    internal class Bank
    {
        public bool HasSufficientSavings(Customer c, int amount)
        {
            Console.WriteLine("Check bank for " + c.Name);
            return true;
        }
    }

    /// <summary>
    /// The 'Subsystem ClassB' class
    /// </summary>
    internal class Credit
    {
        public bool HasGoodCredit(Customer c)
        {
            Console.WriteLine("Check credit for " + c.Name);
            return true;
        }
    }

    /// <summary>
    /// The 'Subsystem ClassC' class
    /// </summary>
    internal class Loan
    {
        public bool HasNoBadLoans(Customer c)
        {
            Console.WriteLine("Check loans for " + c.Name);
            return true;
        }
    }

    /// <summary>
    /// Customer class
    /// </summary>
    internal class Customer
    {
        private string name;

        // Constructor
        public Customer(string name)
        {
            this.name = name;
        }

        // Gets the name
        public string Name
        {
            get { return name; }
        }
    }

    /// <summary>
    /// The 'Facade' class
    /// </summary>
    internal class Mortgage
    {
        private Bank bank = new Bank();
        private Loan loan = new Loan();
        private Credit credit = new Credit();

        public bool IsEligible(Customer cust, int amount)
        {
            Console.WriteLine("{0} applies for {1:C} loan\n",
                cust.Name, amount);

            bool eligible = true;

            // Check creditworthyness of applicant
            if (!bank.HasSufficientSavings(cust, amount))
            {
                eligible = false;
            }
            else if (!loan.HasNoBadLoans(cust))
            {
                eligible = false;
            }
            else if (!credit.HasGoodCredit(cust))
            {
                eligible = false;
            }

            return eligible;
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Facade Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Facade
            var mortgage = new Mortgage();

            // Evaluate mortgage eligibility for customer
            var customer = new Customer { Name = "Ann McKinsey" };
            bool eligible = mortgage.IsEligible(customer, 125000);

            Console.WriteLine("\n" + customer.Name +
                " has been " + (eligible ? "Approved" : "Rejected"));

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subsystem ClassA' class
    /// </summary>
    internal class Bank
    {
        public bool HasSufficientSavings(Customer c, int amount)
        {
            Console.WriteLine("Check bank for " + c.Name);
            return true;
        }
    }

    /// <summary>
    /// The 'Subsystem ClassB' class
    /// </summary>
    internal class Credit
    {
        public bool HasGoodCredit(Customer c)
        {
            Console.WriteLine("Check credit for " + c.Name);
            return true;
        }
    }

    /// <summary>
    /// The 'Subsystem ClassC' class
    /// </summary>
    internal class Loan
    {
        public bool HasNoBadLoans(Customer c)
        {
            Console.WriteLine("Check loans for " + c.Name);
            return true;
        }
    }

    /// <summary>
    /// The 'Facade' class
    /// </summary>
    internal class Mortgage
    {
        private Bank bank = new Bank();
        private Loan loan = new Loan();
        private Credit credit = new Credit();

        public bool IsEligible(Customer cust, int amount)
        {
            Console.WriteLine("{0} applies for {1:C} loan\n",
                cust.Name, amount);

            bool eligible = true;

            // Check creditworthyness of applicant
            if (!bank.HasSufficientSavings(cust, amount))
            {
                eligible = false;
            }
            else if (!loan.HasNoBadLoans(cust))
            {
                eligible = false;
            }
            else if (!credit.HasGoodCredit(cust))
            {
                eligible = false;
            }

            return eligible;
        }
    }

    /// <summary>
    /// Customer class
    /// </summary>
    internal class Customer
    {
        // Gets or sets the name
        public string Name { get; set; }
    }
```

## Реализация на C# (Head First) ##

```csharp
    internal class HomeTheaterTestDrive
    {
        private static void Main(string[] args)
        {
            var amp = new Amplifier("Top-O-Line Amplifier");
            var tuner = new Tuner("Top-O-Line AM/FM Tuner", amp);
            var dvd = new DvdPlayer("Top-O-Line DVD Player", amp);
            var cd = new CdPlayer("Top-O-Line CD Player", amp);

            var projector = new Projector("Top-O-Line Projector", dvd);
            var lights = new TheaterLights("Theater Ceiling Lights");
            var screen = new Screen("Theater Screen");
            var popper = new PopcornPopper("Popcorn Popper");

            var homeTheater =
                new HomeTheaterFacade(amp, tuner, dvd, cd,
                projector, screen, lights, popper);

            homeTheater.WatchMovie("Raiders of the Lost Ark");
            homeTheater.EndMovie();

            // Wait for user
            Console.ReadKey();
        }
    }

    #region Facade

    public class HomeTheaterFacade
    {
        private Amplifier _amp;
        private Tuner _tuner;
        private DvdPlayer _dvd;
        private CdPlayer _cd;
        private Projector _projector;
        private TheaterLights _lights;
        private Screen _screen;
        private PopcornPopper _popper;

        public HomeTheaterFacade(Amplifier amp,
            Tuner tuner,
            DvdPlayer dvd,
            CdPlayer cd,
            Projector projector,
            Screen screen,
            TheaterLights lights,
            PopcornPopper popper)
        {
            this._amp = amp;
            this._tuner = tuner;
            this._dvd = dvd;
            this._cd = cd;
            this._projector = projector;
            this._screen = screen;
            this._lights = lights;
            this._popper = popper;
        }

        public void WatchMovie(string movie)
        {
            Console.WriteLine("Get ready to watch a movie...");
            _popper.On();
            _popper.Pop();
            _lights.Dim(10);
            _screen.Down();
            _projector.On();
            _projector.WideScreenMode();
            _amp.On();
            _amp.SetDvd(_dvd);
            _amp.SetSurroundSound();
            _amp.SetVolume(5);
            _dvd.On();
            _dvd.Play(movie);
        }

        public void EndMovie()
        {
            Console.WriteLine("\nShutting movie theater down...");
            _popper.Off();
            _lights.On();
            _screen.Up();
            _projector.Off();
            _amp.Off();
            _dvd.Stop();
            _dvd.Eject();
            _dvd.Off();
        }

        public void ListenToCd(string cdTitle)
        {
            Console.WriteLine("Get ready for an audiopile experence...");
            _lights.On();
            _amp.On();
            _amp.SetVolume(5);
            _amp.SetCd(_cd);
            _amp.SetStereoSound();
            _cd.On();
            _cd.Play(cdTitle);
        }

        public void EndCd()
        {
            Console.WriteLine("Shutting down CD...");
            _amp.Off();
            _amp.SetCd(_cd);
            _cd.Eject();
            _cd.Off();
        }

        public void ListenToRadio(double frequency)
        {
            Console.WriteLine("Tuning in the airwaves...");
            _tuner.On();
            _tuner.SetFrequency(frequency);
            _amp.On();
            _amp.SetVolume(5);
            _amp.SetTuner(_tuner);
        }

        public void EndRadio()
        {
            Console.WriteLine("Shutting down the tuner...");
            _tuner.Off();
            _amp.Off();
        }
    }

    #endregion Facade

    #region Subsystem Components

    public class Tuner
    {
        private string _description;
        private Amplifier _amplifier;
        private double _frequency;

        public Tuner(string description, Amplifier amplifier)
        {
            this._description = description;
            this._amplifier = amplifier;
        }

        public void On()
        {
            Console.WriteLine(_description + " on");
        }

        public void Off()
        {
            Console.WriteLine(_description + " off");
        }

        public void SetFrequency(double frequency)
        {
            Console.WriteLine(_description + " setting frequency to " + frequency);
            this._frequency = frequency;
        }

        public void SetAm()
        {
            Console.WriteLine(_description + " setting AM mode");
        }

        public void SetFm()
        {
            Console.WriteLine(_description + " setting FM mode");
        }

        public override string ToString()
        {
            return _description;
        }
    }

    public class Amplifier
    {
        private string _description;
        private Tuner _tuner;
        private DvdPlayer _dvd;
        private CdPlayer _cd;

        public Amplifier(string description)
        {
            this._description = description;
        }

        public void On()
        {
            Console.WriteLine(_description + " on");
        }

        public void Off()
        {
            Console.WriteLine(_description + " off");
        }

        public void SetStereoSound()
        {
            Console.WriteLine(_description + " stereo mode on");
        }

        public void SetSurroundSound()
        {
            Console.WriteLine(_description + " surround sound on (5 speakers, 1 subwoofer)");
        }

        public void SetVolume(int level)
        {
            Console.WriteLine(_description + " setting volume to " + level);
        }

        public void SetTuner(Tuner tuner)
        {
            Console.WriteLine(_description + " setting tuner to " + _dvd);
            this._tuner = tuner;
        }

        public void SetDvd(DvdPlayer dvd)
        {
            Console.WriteLine(_description + " setting DVD player to " + dvd);
            this._dvd = dvd;
        }

        public void SetCd(CdPlayer cd)
        {
            Console.WriteLine(_description + " setting CD player to " + cd);
            this._cd = cd;
        }

        public override string ToString()
        {
            return _description;
        }
    }

    public class TheaterLights
    {
        private string _description;

        public TheaterLights(string description)
        {
            this._description = description;
        }

        public void On()
        {
            Console.WriteLine(_description + " on");
        }

        public void Off()
        {
            Console.WriteLine(_description + " off");
        }

        public void Dim(int level)
        {
            Console.WriteLine(_description + " dimming to " + level + "%");
        }

        public override string ToString()
        {
            return _description;
        }
    }

    public class Screen
    {
        private string _description;

        public Screen(string description)
        {
            this._description = description;
        }

        public void Up()
        {
            Console.WriteLine(_description + " going up");
        }

        public void Down()
        {
            Console.WriteLine(_description + " going down");
        }

        public override string ToString()
        {
            return _description;
        }
    }

    public class Projector
    {
        private string _description;
        private DvdPlayer _dvdPlayer;

        public Projector(string description, DvdPlayer dvdPlayer)
        {
            this._description = description;
            this._dvdPlayer = dvdPlayer;
        }

        public void On()
        {
            Console.WriteLine(_description + " on");
        }

        public void Off()
        {
            Console.WriteLine(_description + " off");
        }

        public void WideScreenMode()
        {
            Console.WriteLine(_description + " in widescreen mode (16x9 aspect ratio)");
        }

        public void TvMode()
        {
            Console.WriteLine(_description + " in tv mode (4x3 aspect ratio)");
        }

        public override string ToString()
        {
            return _description;
        }
    }

    public class PopcornPopper
    {
        private string _description;

        public PopcornPopper(string description)
        {
            this._description = description;
        }

        public void On()
        {
            Console.WriteLine(_description + " on");
        }

        public void Off()
        {
            Console.WriteLine(_description + " off");
        }

        public void Pop()
        {
            Console.WriteLine(_description + " popping popcorn!");
        }

        public override string ToString()
        {
            return _description;
        }
    }

    public class DvdPlayer
    {
        private string _description;
        private int _currentTrack;
        private Amplifier _amplifier;
        private string _movie;

        public DvdPlayer(string description, Amplifier amplifier)
        {
            this._description = description;
            this._amplifier = amplifier;
        }

        public void On()
        {
            Console.WriteLine(_description + " on");
        }

        public void Off()
        {
            Console.WriteLine(_description + " off");
        }

        public void Eject()
        {
            _movie = null;
            Console.WriteLine(_description + " eject");
        }

        public void Play(string movie)
        {
            this._movie = movie;
            _currentTrack = 0;
            Console.WriteLine(_description + " playing \"" + movie + "\"");
        }

        public void Play(int track)
        {
            if (_movie == null)
            {
                Console.WriteLine(_description + " can't play track " + track + " no dvd inserted");
            }
            else
            {
                _currentTrack = track;
                Console.WriteLine(_description + " playing track " + _currentTrack + " of \"" + _movie + "\"");
            }
        }

        public void Stop()
        {
            _currentTrack = 0;
            Console.WriteLine(_description + " stopped \"" + _movie + "\"");
        }

        public void Pause()
        {
            Console.WriteLine(_description + " paused \"" + _movie + "\"");
        }

        public void SetTwoChannelAudio()
        {
            Console.WriteLine(_description + " set two channel audio");
        }

        public void SetSurroundAudio()
        {
            Console.WriteLine(_description + " set surround audio");
        }

        public override string ToString()
        {
            return _description;
        }
    }

    public class CdPlayer
    {
        private string _description;
        private int _currentTrack;
        private Amplifier _amplifier;
        private string _title;

        public CdPlayer(string description, Amplifier amplifier)
        {
            this._description = description;
            this._amplifier = amplifier;
        }

        public void On()
        {
            Console.WriteLine(_description + " on");
        }

        public void Off()
        {
            Console.WriteLine(_description + " off");
        }

        public void Eject()
        {
            _title = null;
            Console.WriteLine(_description + " eject");
        }

        public void Play(string title)
        {
            this._title = title;
            _currentTrack = 0;
            Console.WriteLine(_description + " playing \"" + title + "\"");
        }

        public void Play(int track)
        {
            if (_title == null)
            {
                Console.WriteLine(_description + " can't play track " + _currentTrack +
                    ", no cd inserted");
            }
            else
            {
                _currentTrack = track;
                Console.WriteLine(_description + " playing track " + _currentTrack);
            }
        }

        public void Stop()
        {
            _currentTrack = 0;
            Console.WriteLine(_description + " stopped");
        }

        public void Pause()
        {
            Console.WriteLine(_description + " paused \"" + _title + "\"");
        }

        public override string ToString()
        {
            return _description;
        }
    }

    #endregion Subsystem Components
```

## Реализация на JAVA ##

```java
    TODO
```