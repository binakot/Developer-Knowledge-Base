# Одиночка (Singleton) #

Паттерн Одиночка гарантирует, что класс имеет только один экземпляр,
и предоставляет глобальную точку доступа к этому экзепляру.

![UML](/design_patterns/creational/singleton_UML.svg?raw=true)

* Singleton - одиночка

[Статья на Википедии](https://ru.wikipedia.org/wiki/Одиночка_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Singleton Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Constructor is protected -- cannot use new
            Singleton s1 = Singleton.Instance();
            Singleton s2 = Singleton.Instance();

            // Test for same instance
            if (s1 == s2)
            {
                Console.WriteLine("Objects are the same instance");
            }

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Singleton' class
    /// </summary>
    internal class Singleton
    {
        private static Singleton instance;

        // Constructor is 'protected'
        protected Singleton()
        {
        }

        public static Singleton Instance()
        {
            // Uses lazy initialization.
            // Note: this is not thread safe.
            if (instance == null)
            {
                instance = new Singleton();
            }

            return instance;
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Singleton Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            LoadBalancer b1 = LoadBalancer.GetLoadBalancer();
            LoadBalancer b2 = LoadBalancer.GetLoadBalancer();
            LoadBalancer b3 = LoadBalancer.GetLoadBalancer();
            LoadBalancer b4 = LoadBalancer.GetLoadBalancer();

            // Same instance?
            if (b1 == b2 && b2 == b3 && b3 == b4)
            {
                Console.WriteLine("Same instance\n");
            }

            // Load balance 15 server requests
            LoadBalancer balancer = LoadBalancer.GetLoadBalancer();
            for (int i = 0; i < 15; i++)
            {
                string server = balancer.Server;
                Console.WriteLine("Dispatch Request to: " + server);
            }

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Singleton' class
    /// </summary>
    internal class LoadBalancer
    {
        private static LoadBalancer instance;
        private List<string> servers = new List<string>();
        private Random random = new Random();

        // Lock synchronization object
        private static object locker = new object();

        // Constructor (protected)
        protected LoadBalancer()
        {
            // List of available servers
            servers.Add("ServerI");
            servers.Add("ServerII");
            servers.Add("ServerIII");
            servers.Add("ServerIV");
            servers.Add("ServerV");
        }

        public static LoadBalancer GetLoadBalancer()
        {
            // Support multithreaded applications through
            // 'Double checked locking' pattern which (once
            // the instance exists) avoids locking each
            // time the method is invoked
            if (instance == null)
            {
                lock (locker)
                {
                    if (instance == null)
                    {
                        instance = new LoadBalancer();
                    }
                }
            }

            return instance;
        }

        // Simple, but effective random load balancer
        public string Server
        {
            get
            {
                int r = random.Next(servers.Count);
                return servers[r].ToString();
            }
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Singleton Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            var b1 = LoadBalancer.GetLoadBalancer();
            var b2 = LoadBalancer.GetLoadBalancer();
            var b3 = LoadBalancer.GetLoadBalancer();
            var b4 = LoadBalancer.GetLoadBalancer();

            // Confirm these are the same instance
            if (b1 == b2 && b2 == b3 && b3 == b4)
            {
                Console.WriteLine("Same instance\n");
            }

            // Next, load balance 15 requests for a server
            var balancer = LoadBalancer.GetLoadBalancer();
            for (int i = 0; i < 15; i++)
            {
                string serverName = balancer.NextServer.Name;
                Console.WriteLine("Dispatch request to: " + serverName);
            }

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Singleton' class
    /// </summary>
    internal sealed class LoadBalancer
    {
        // Static members are 'eagerly initialized', that is,
        // immediately when class is loaded for the first time.
        // .NET guarantees thread safety for static initialization
        private static readonly LoadBalancer instance = new LoadBalancer();

        // Type-safe generic list of servers
        private List<Server> servers;

        private Random random = new Random();

        // Note: constructor is 'private'
        private LoadBalancer()
        {
            // Load list of available servers
            servers = new List<Server>
                {
                  new Server{ Name = "ServerI", IP = "120.14.220.18" },
                  new Server{ Name = "ServerII", IP = "120.14.220.19" },
                  new Server{ Name = "ServerIII", IP = "120.14.220.20" },
                  new Server{ Name = "ServerIV", IP = "120.14.220.21" },
                  new Server{ Name = "ServerV", IP = "120.14.220.22" },
                };
        }

        public static LoadBalancer GetLoadBalancer()
        {
            return instance;
        }

        // Simple, but effective load balancer
        public Server NextServer
        {
            get
            {
                int r = random.Next(servers.Count);
                return servers[r];
            }
        }
    }

    /// <summary>
    /// Represents a server machine
    /// </summary>
    internal class Server
    {
        // Gets or sets server name
        public string Name { get; set; }

        // Gets or sets server IP address
        public string IP { get; set; }
    }
```

## Реализация на C# (Head First) ##

```csharp
    internal class SingletonClient
    {
        private static void Main(string[] args)
        {
            var singleton = Singleton.getInstance();
            singleton.SaySomething();

            // .NET singleton threadsafe example.

            var es1 = EagerSingleton.GetInstance();
            var es2 = EagerSingleton.GetInstance();
            var es3 = EagerSingleton.GetInstance();

            if (es1 == es2 && es2 == es3)
            {
                Console.WriteLine("Same instance");
            }

            // Wait for user
            Console.ReadKey();
        }
    }

    #region Singleton

    public class Singleton
    {
        private static Singleton _uniqueInstance;
        private static readonly object _syncLock = new Object();

        // other useful instance variables here

        private Singleton()
        {
        }

        public static Singleton getInstance()
        {
            // Lock entire body of method
            lock (_syncLock)
            {
                if (_uniqueInstance == null)
                {
                    _uniqueInstance = new Singleton();
                }
                return _uniqueInstance;
            }
        }

        // other useful methods here
        public void SaySomething()
        {
            Console.WriteLine("I run, therefore I am");
        }
    }

    internal sealed class EagerSingleton
    {
        // CLR eagerly initializes static member when class is first used
        // CLR guarantees thread safety for static initialisation
        private static readonly EagerSingleton _instance = new EagerSingleton();

        // Note: constructor is private
        private EagerSingleton()
        {
        }

        public static EagerSingleton GetInstance()
        {
            return _instance;
        }
    }

    #endregion Singleton
```

## Реализация на JAVA ##

```java
    /**
     * Singleton class. Eagerly initialized static instance guarantees thread safety.
     */
    public final class EagerlyInitializedSingleton {

        private static final EagerlyInitializedSingleton INSTANCE = new EagerlyInitializedSingleton();

        private EagerlyInitializedSingleton() {}

        public static EagerlyInitializedSingleton getInstance() {
            return INSTANCE;
        }
    }

    /**
     * The Initialize-on-demand-holder idiom is a secure way of creating a lazy initialized singleton
     * object in Java.
     *
     * The technique is as lazy as possible and works in all known versions of Java. It takes advantage
     * of language guarantees about class initialization, and will therefore work correctly in all
     * Java-compliant compilers and virtual machines.
     *
     * The inner class is referenced no earlier (and therefore loaded no earlier by the class loader) than
     * the moment that getInstance() is called. Thus, this solution is thread-safe without requiring special
     * language constructs (i.e. volatile or synchronized).
     */
    public final class InitializingOnDemandSingleton {

        private InitializingOnDemandSingleton() {}

        public static InitializingOnDemandSingleton getInstance() {
            return HelperHolder.INSTANCE;
        }

        private static class HelperHolder {
            private static final InitializingOnDemandSingleton INSTANCE =
                new InitializingOnDemandSingleton();
        }
    }

    /**
     * Thread-safe Singleton class.
     *
     * The instance is lazily initialized and thus needs synchronization mechanism.
     *
     * Note: if created by reflection then a singleton will not be created but multiple options in the same classloader.
     */
    public final class ThreadSafeLazyLoadedSingleton {

        private static ThreadSafeLazyLoadedSingleton instance;

        private ThreadSafeLazyLoadedSingleton() {}

        public static synchronized ThreadSafeLazyLoadedSingleton getInstance() {
            if (instance == null) {
                instance = new ThreadSafeLazyLoadedSingleton();
            }
            return instance;
        }
    }

     /**
      * Double check locking
      *
      * http://www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html
      *
      * Broken under Java 1.4.
      */
     public final class ThreadSafeDoubleCheckLockingSingleton {

        private static volatile ThreadSafeDoubleCheckLockingSingleton instance;

        private ThreadSafeDoubleCheckLockingSingleton() {
            // to prevent instantiating by Reflection call
            if (instance != null) {
                throw new IllegalStateException("Already initialized.");
            }
        }

        public static ThreadSafeDoubleCheckLockingSingleton getInstance() {
            // local variable increases performance by 25 percent
            // Joshua Bloch "Effective Java, Second Edition", p. 283-284

            ThreadSafeDoubleCheckLockingSingleton result = instance;
            // Check if singleton instance is initialized. If it is initialized then we can return the instance.
            if (result == null) {
                // It is not initialized but we cannot be sure because some other thread might have initialized it
                // in the meanwhile. So to make sure we need to lock on an object to get mutual exclusion.
                synchronized (ThreadSafeDoubleCheckLockingSingleton.class) {
                    // Again assign the instance to local variable to check if it was initialized by some other thread
                    // while current thread was blocked to enter the locked zone. If it was initialized then we can
                    // return the previously created instance just like the previous null check.
                    result = instance;
                    if (result == null) {
                        // The instance is still not initialized so we can safely (no other thread can enter this zone)
                        // create an instance and make it our singleton instance.
                        instance = result = new ThreadSafeDoubleCheckLockingSingleton();
                    }
                }
            }
            return result;
        }
    }

    /**
     * Enum based singleton implementation.
     *
     * Effective Java 2nd Edition (Joshua Bloch) p. 18
     */
    public enum EnumSingleton {

        INSTANCE;

        @Override
        public String toString() {
            return getDeclaringClass().getCanonicalName() + "@" + hashCode();
        }
    }
```