# Заместитель (Proxy) #

Также известен как Суррогат (Surrogate).

Паттерн Заместитель предоставляет суррогатный объект, управляющий доступом к другому объекту.

![UML](/design_patterns/structural/proxy_UML.svg?raw=true)

* Proxy - заместитель

* Subject - абстрактный субъект замещения

* RealSubject - реальный субъект замещения

* Client - клиент

[Статья на Википедии](https://ru.wikipedia.org/wiki/Proxy_(шаблон_проектирования))

Разновидности заместителей:

* _Удаленный Заместитель_ управляет доступом к удаленному объекту из локального объекта-суррогата.

* _Виртуальный Заместитель_ управляет доступом к объекту, создание которого требует больщих затрат ресурсов.

* _Защитный Заместитель_ контролирует доступ к объекту в соответствии с системой привелегий.

* _Фильтрирующий Заместитель_ управляет доступом к группам сетевых ресурсов, защищая их от несанкционированного доступа.

* _Умная Ссылка_ обеспечивает выполнение дополнительных действий при обращении к объекту (например, счетчик обращений и т.д.).

* _Кэширующий Заместитель_ обеспечивает временное хранение результатов высокозатратных операций.
Также может обеспечивать совместный доступ к результатам для предотвращения лишних вычислений или пересылки данных по сети.

* _Синхронизирующий Заместитель_ предоставляет безопасный доступ к объекту из нескольких программных потоков.

* _Упрощающий Заместитель_ скрывает сложность и управляет доступом к сложному набору классов.
Иногда называется Фасадным Заместителем. Отличается от паттерна Фасад тем, что первый управляет доступом,
а второй только предоставляет альтернативный интерфейс.

* _Заместитель Отложенного Копирования_ задерживает фактическое копирование объекта до момента выполнения операций с копией
(разновидность Виртуального Заместителя).

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Proxy Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create proxy and request a service
            Proxy proxy = new Proxy();
            proxy.Request();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subject' abstract class
    /// </summary>
    internal abstract class Subject
    {
        public abstract void Request();
    }

    /// <summary>
    /// The 'RealSubject' class
    /// </summary>
    internal class RealSubject : Subject
    {
        public override void Request()
        {
            Console.WriteLine("Called RealSubject.Request()");
        }
    }

    /// <summary>
    /// The 'Proxy' class
    /// </summary>
    internal class Proxy : Subject
    {
        private RealSubject realSubject;

        public override void Request()
        {
            // Use 'lazy initialization'
            if (realSubject == null)
            {
                realSubject = new RealSubject();
            }

            realSubject.Request();
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Proxy Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create math proxy
            MathProxy proxy = new MathProxy();

            // Do the math
            Console.WriteLine("4 + 2 = " + proxy.Add(4, 2));
            Console.WriteLine("4 - 2 = " + proxy.Sub(4, 2));
            Console.WriteLine("4 * 2 = " + proxy.Mul(4, 2));
            Console.WriteLine("4 / 2 = " + proxy.Div(4, 2));

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subject interface
    /// </summary>
    public interface IMath
    {
        double Add(double x, double y);

        double Sub(double x, double y);

        double Mul(double x, double y);

        double Div(double x, double y);
    }

    /// <summary>
    /// The 'RealSubject' class
    /// </summary>
    internal class Math : IMath
    {
        public double Add(double x, double y)
        {
            return x + y;
        }

        public double Sub(double x, double y)
        {
            return x - y;
        }

        public double Mul(double x, double y)
        {
            return x * y;
        }

        public double Div(double x, double y)
        {
            return x / y;
        }
    }

    /// <summary>
    /// The 'Proxy Object' class
    /// </summary>
    internal class MathProxy : IMath
    {
        private Math math = new Math();

        public double Add(double x, double y)
        {
            return math.Add(x, y);
        }

        public double Sub(double x, double y)
        {
            return math.Sub(x, y);
        }

        public double Mul(double x, double y)
        {
            return math.Mul(x, y);
        }

        public double Div(double x, double y)
        {
            return math.Div(x, y);
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Proxy Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create math proxy
            var proxy = new MathProxy();

            // Do the math
            Console.WriteLine("4 + 2 = " + proxy.Add(4, 2));
            Console.WriteLine("4 - 2 = " + proxy.Sub(4, 2));
            Console.WriteLine("4 * 2 = " + proxy.Mul(4, 2));
            Console.WriteLine("4 / 2 = " + proxy.Div(4, 2));

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Subject' interface
    /// </summary>
    public interface IMath
    {
        double Add(double x, double y);

        double Sub(double x, double y);

        double Mul(double x, double y);

        double Div(double x, double y);
    }

    /// <summary>
    /// The 'RealSubject' class
    /// </summary>
    internal class Math : MarshalByRefObject, IMath
    {
        public double Add(double x, double y)
        {
            return x + y;
        }

        public double Sub(double x, double y)
        {
            return x - y;
        }

        public double Mul(double x, double y)
        {
            return x * y;
        }

        public double Div(double x, double y)
        {
            return x / y;
        }
    }

    /// <summary>
    /// The remote 'Proxy Object' class
    /// </summary>
    internal class MathProxy : IMath
    {
        private Math math;

        // Constructor
        public MathProxy()
        {
            // Create Math instance in a different AppDomain
            var ad = AppDomain.CreateDomain("MathDomain", null, null);

            var o = ad.CreateInstance(
                "DoFactory.GangOfFour.Proxy.NETOptimized",
                "DoFactory.GangOfFour.Proxy.NETOptimized.Math");
            math = (Math)o.Unwrap();
        }

        public double Add(double x, double y)
        {
            return math.Add(x, y);
        }

        public double Sub(double x, double y)
        {
            return math.Sub(x, y);
        }

        public double Mul(double x, double y)
        {
            return math.Mul(x, y);
        }

        public double Div(double x, double y)
        {
            return math.Div(x, y);
        }
    }
```

## Реализация на C# (Head First) ##

```csharp
    /// <summary>
    /// Summary description for FormVirtualProxy.
    /// </summary>
    public class FormVirtualProxy : System.Windows.Forms.Form
    {
        private System.Windows.Forms.Button buttonTestImageProxy;
        private System.Windows.Forms.PictureBox pictureBox;
        private System.Windows.Forms.Label label1;

        /// <summary>
        /// Required designer variable.
        /// </summary>
        private System.ComponentModel.Container components = null;

        public FormVirtualProxy()
        {
            //
            // Required for Windows Form Designer support
            //
            InitializeComponent();
        }

        /// <summary>
        /// Clean up any resources being used.
        /// </summary>
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                if (components != null)
                {
                    components.Dispose();
                }
            }
            base.Dispose(disposing);
        }

        #region Windows Form Designer generated code

        /// <summary>
        /// Required method for Designer support - do not modify
        /// the contents of this method with the code editor.
        /// </summary>
        private void InitializeComponent()
        {
            this.buttonTestImageProxy = new System.Windows.Forms.Button();
            this.pictureBox = new System.Windows.Forms.PictureBox();
            this.label1 = new System.Windows.Forms.Label();
            ((System.ComponentModel.ISupportInitialize)(this.pictureBox)).BeginInit();
            this.SuspendLayout();
            //
            // buttonTestImageProxy
            //
            this.buttonTestImageProxy.Location = new System.Drawing.Point(197, 25);
            this.buttonTestImageProxy.Name = "buttonTestImageProxy";
            this.buttonTestImageProxy.Size = new System.Drawing.Size(105, 23);
            this.buttonTestImageProxy.TabIndex = 0;
            this.buttonTestImageProxy.Text = "Test Image Proxy";
            this.buttonTestImageProxy.Click += new System.EventHandler(this.buttonTestImageProxy_Click);
            //
            // pictureBox
            //
            this.pictureBox.BorderStyle = System.Windows.Forms.BorderStyle.Fixed3D;
            this.pictureBox.Location = new System.Drawing.Point(31, 24);
            this.pictureBox.Name = "pictureBox";
            this.pictureBox.Size = new System.Drawing.Size(147, 159);
            this.pictureBox.TabIndex = 1;
            this.pictureBox.TabStop = false;
            this.pictureBox.Click += new System.EventHandler(this.pictureBox_Click);
            //
            // label1
            //
            this.label1.Font = new System.Drawing.Font("Microsoft Sans Serif", 8.25F, System.Drawing.FontStyle.Bold, System.Drawing.GraphicsUnit.Point, ((byte)(0)));
            this.label1.Location = new System.Drawing.Point(194, 51);
            this.label1.Name = "label1";
            this.label1.Size = new System.Drawing.Size(118, 20);
            this.label1.TabIndex = 2;
            this.label1.Text = "Click button twice";
            this.label1.Click += new System.EventHandler(this.label1_Click);
            //
            // FormVirtualProxy
            //
            this.AutoScaleBaseSize = new System.Drawing.Size(5, 13);
            this.ClientSize = new System.Drawing.Size(323, 217);
            this.Controls.Add(this.label1);
            this.Controls.Add(this.pictureBox);
            this.Controls.Add(this.buttonTestImageProxy);
            this.Name = "FormVirtualProxy";
            this.Text = "Virtual Proxy Test";
            ((System.ComponentModel.ISupportInitialize)(this.pictureBox)).EndInit();
            this.ResumeLayout(false);
        }

        #endregion Windows Form Designer generated code

        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        private static void Main()
        {
            Application.Run(new FormVirtualProxy());
        }

        private void buttonTestImageProxy_Click(object sender, System.EventArgs e)
        {
            this.pictureBox.Image = new ImageProxy().Image;
        }

        private void pictureBox_Click(object sender, System.EventArgs e)
        {
        }

        private void label1_Click(object sender, System.EventArgs e)
        {
        }

        private class ImageProxy
        {
            private static Image _image = null;
            private int _width = 133;
            private int _height = 154;
            private bool _retrieving = false;

            public int Width
            {
                get { return _image == null ? _width : _image.Width; }
            }

            public int Height
            {
                get { return _image == null ? _height : _image.Height; }
            }

            public Image Image
            {
                get
                {
                    if (_image != null)
                        return _image;
                    else
                    {
                        if (!_retrieving)
                        {
                            _retrieving = true;
                            Thread retrievalThread = new Thread(new ThreadStart(RetrieveImage));
                            retrievalThread.Start();
                        }
                        return PlaceHolderImage();
                    }
                }
            }

            public Image PlaceHolderImage()
            {
                return new Bitmap(System.Reflection.Assembly.GetExecutingAssembly().GetManifestResourceStream("DoFactory.HeadFirst.Proxy.VirtualProxy.PlaceHolder.jpg"));
            }

            public void RetrieveImage()
            {
                // Book image from amazon
                string url = "http://images.amazon.com/images/P/0596007124.01._PE34_SCMZZZZZZZ_.jpg";

                HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(url);
                HttpWebResponse response = (HttpWebResponse)request.GetResponse();
                _image = Image.FromStream(response.GetResponseStream());
            }
        }
    }
```

## Реализация на JAVA ##

```java
    TODO
```