# Команда (Command) #

Также известен как Действие (Action) или Транзакция (Transaction).

Паттерн Команда инкапсулирует запрос в виде объекта,
делая возможной параметризацию клиентских объектов с другими запросами,
организацию очереди или регистрацию запросов,
а также поддержку отмены операций.

![UML](/design_patterns/behavioral/command_UML.gif)

* Command - абстрактная команда

* ConcreteCommand - конкретная команда

* Client - клиент

* Invoker - инициатор

* Receiver - получатель

[Статья на Википедии](https://ru.wikipedia.org/wiki/Команда_(шаблон_проектирования))

## Абстрактная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for Structural
    /// Command Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create receiver, command, and invoker
            Receiver receiver = new Receiver();
            Command command = new ConcreteCommand(receiver);
            Invoker invoker = new Invoker();

            // Set and execute command
            invoker.SetCommand(command);
            invoker.ExecuteCommand();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Command' abstract class
    /// </summary>
    internal abstract class Command
    {
        protected Receiver receiver;

        // Constructor
        public Command(Receiver receiver)
        {
            this.receiver = receiver;
        }

        public abstract void Execute();
    }

    /// <summary>
    /// The 'ConcreteCommand' class
    /// </summary>
    internal class ConcreteCommand : Command
    {
        // Constructor
        public ConcreteCommand(Receiver receiver) :
            base(receiver)
        {
        }

        public override void Execute()
        {
            receiver.Action();
        }
    }

    /// <summary>
    /// The 'Receiver' class
    /// </summary>
    internal class Receiver
    {
        public void Action()
        {
            Console.WriteLine("Called Receiver.Action()");
        }
    }

    /// <summary>
    /// The 'Invoker' class
    /// </summary>
    internal class Invoker
    {
        private Command command;

        public void SetCommand(Command command)
        {
            this.command = command;
        }

        public void ExecuteCommand()
        {
            command.Execute();
        }
    }
```

## Реальная реализация на C# (GoF) ##

```charp
    /// <summary>
    /// MainApp startup class for Real-World
    /// Command Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create user and let her compute
            User user = new User();

            // User presses calculator buttons
            user.Compute('+', 100);
            user.Compute('-', 50);
            user.Compute('*', 10);
            user.Compute('/', 2);

            // Undo 4 commands
            user.Undo(4);

            // Redo 3 commands
            user.Redo(3);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Command' abstract class
    /// </summary>
    internal abstract class Command
    {
        public abstract void Execute();

        public abstract void UnExecute();
    }

    /// <summary>
    /// The 'ConcreteCommand' class
    /// </summary>
    internal class CalculatorCommand : Command
    {
        private char @operator;
        private int operand;
        private Calculator calculator;

        // Constructor
        public CalculatorCommand(Calculator calculator,
            char @operator, int operand)
        {
            this.calculator = calculator;
            this.@operator = @operator;
            this.operand = operand;
        }

        // Gets operator
        public char Operator
        {
            set { @operator = value; }
        }

        // Get operand
        public int Operand
        {
            set { operand = value; }
        }

        // Execute new command
        public override void Execute()
        {
            calculator.Operation(@operator, operand);
        }

        // Unexecute last command
        public override void UnExecute()
        {
            calculator.Operation(Undo(@operator), operand);
        }

        // Returns opposite operator for given operator
        private char Undo(char @operator)
        {
            switch (@operator)
            {
                case '+': return '-';
                case '-': return '+';
                case '*': return '/';
                case '/': return '*';
                default:
                    throw new ArgumentException("@operator");
            }
        }
    }

    /// <summary>
    /// The 'Receiver' class
    /// </summary>
    internal class Calculator
    {
        private int curr = 0;

        public void Operation(char @operator, int operand)
        {
            switch (@operator)
            {
                case '+': curr += operand; break;
                case '-': curr -= operand; break;
                case '*': curr *= operand; break;
                case '/': curr /= operand; break;
            }
            Console.WriteLine(
                "Current value = {0,3} (following {1} {2})",
                curr, @operator, operand);
        }
    }

    /// <summary>
    /// The 'Invoker' class
    /// </summary>
    internal class User
    {
        // Initializers
        private Calculator calculator = new Calculator();

        private List<Command> commands = new List<Command>();
        private int current = 0;

        public void Redo(int levels)
        {
            Console.WriteLine("\n---- Redo {0} levels ", levels);
            // Perform redo operations
            for (int i = 0; i < levels; i++)
            {
                if (current < commands.Count - 1)
                {
                    Command command = commands[current++];
                    command.Execute();
                }
            }
        }

        public void Undo(int levels)
        {
            Console.WriteLine("\n---- Undo {0} levels ", levels);
            // Perform undo operations
            for (int i = 0; i < levels; i++)
            {
                if (current > 0)
                {
                    Command command = commands[--current] as Command;
                    command.UnExecute();
                }
            }
        }

        public void Compute(char @operator, int operand)
        {
            // Create command operation and execute it
            Command command = new CalculatorCommand(calculator, @operator, operand);
            command.Execute();

            // Add command to undo list
            commands.Add(command);
            current++;
        }
    }
```

## Улучшенная реальная реализация на C# (GoF) ##

```csharp
    /// <summary>
    /// MainApp startup class for .NET optimized
    /// Command Design Pattern.
    /// </summary>
    internal class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        private static void Main()
        {
            // Create user and let her compute
            var user = new User();

            // Issue several compute commands
            user.Compute('+', 100);
            user.Compute('-', 50);
            user.Compute('*', 10);
            user.Compute('/', 2);

            // Undo 4 commands
            user.Undo(4);

            // Redo 3 commands
            user.Redo(3);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Command' interface
    /// </summary>
    internal interface ICommand
    {
        void Execute();

        void UnExecute();
    }

    /// <summary>
    /// The 'ConcreteCommand' class
    /// </summary>
    internal class CalculatorCommand : ICommand
    {
        private char @operator;
        private int operand;
        private Calculator calculator;

        // Constructor
        public CalculatorCommand(Calculator calculator, char @operator, int operand)
        {
            this.calculator = calculator;
            this.@operator = @operator;
            this.operand = operand;
        }

        // Sets operator
        public char Operator
        {
            set { @operator = value; }
        }

        // Sets operand
        public int Operand
        {
            set { operand = value; }
        }

        // Execute command
        public void Execute()
        {
            calculator.Operation(@operator, operand);
        }

        // Unexecute command
        public void UnExecute()
        {
            calculator.Operation(Undo(@operator), operand);
        }

        // Return opposite operator for given operator
        private char Undo(char @operator)
        {
            switch (@operator)
            {
                case '+': return '-';
                case '-': return '+';
                case '*': return '/';
                case '/': return '*';
                default:
                    throw new ArgumentException("@operator");
            }
        }
    }

    /// <summary>
    /// The 'Receiver' class
    /// </summary>
    internal class Calculator
    {
        private int current = 0;

        // Perform operation for given operator and operand
        public void Operation(char @operator, int operand)
        {
            switch (@operator)
            {
                case '+': current += operand; break;
                case '-': current -= operand; break;
                case '*': current *= operand; break;
                case '/': current /= operand; break;
            }
            Console.WriteLine(
                "Current value = {0,3} (following {1} {2})",
                current, @operator, operand);
        }
    }

    /// <summary>
    /// The 'Invoker' class
    /// </summary>
    internal class User
    {
        private Calculator calculator = new Calculator();
        private List<ICommand> commands = new List<ICommand>();
        private int current = 0;

        // Redo original commands
        public void Redo(int levels)
        {
            Console.WriteLine("\n---- Redo {0} levels ", levels);

            // Perform redo operations
            for (int i = 0; i < levels; i++)
            {
                if (current < commands.Count - 1)
                {
                    commands[current++].Execute();
                }
            }
        }

        // Undo prior commands
        public void Undo(int levels)
        {
            Console.WriteLine("\n---- Undo {0} levels ", levels);

            // Perform undo operations
            for (int i = 0; i < levels; i++)
            {
                if (current > 0)
                {
                    commands[--current].UnExecute();
                }
            }
        }

        // Compute new value given operator and operand
        public void Compute(char @operator, int operand)
        {
            // Create command operation and execute it
            var command = new CalculatorCommand(calculator, @operator, operand);
            command.Execute();

            // Add command to undo list
            commands.Add(command);
            current++;
        }
    }
```

## Реализация на C# (Head First) ##

```csharp
    internal class RemoteLoader
    {
        private static void Main(string[] args)
        {
            var remoteControl = new RemoteControl();

            var light = new Light("Living Room");
            var tv = new TV("Living Room");
            var stereo = new Stereo("Living Room");
            var hottub = new Hottub();

            var lightOn = new LightOnCommand(light);
            var stereoOn = new StereoOnCommand(stereo);
            var tvOn = new TVOnCommand(tv);
            var hottubOn = new HottubOnCommand(hottub);
            var lightOff = new LightOffCommand(light);
            var stereoOff = new StereoOffCommand(stereo);
            var tvOff = new TVOffCommand(tv);
            var hottubOff = new HottubOffCommand(hottub);

            ICommand[] partyOn = { lightOn, stereoOn, tvOn, hottubOn };
            ICommand[] partyOff = { lightOff, stereoOff, tvOff, hottubOff };

            var partyOnMacro = new MacroCommand(partyOn);
            var partyOffMacro = new MacroCommand(partyOff);

            remoteControl.SetCommand(0, partyOnMacro, partyOffMacro);

            Console.WriteLine(remoteControl);
            Console.WriteLine("--- Pushing Macro On---");
            remoteControl.OnButtonWasPushed(0);
            Console.WriteLine("\n--- Pushing Macro Off---");
            remoteControl.OffButtonWasPushed(0);

            // Wait for user
            Console.ReadKey();
        }
    }

    #region Remote Control

    public class RemoteControl
    {
        private ICommand[] _onCommands;
        private ICommand[] _offCommands;
        private ICommand _undoCommand;

        // Constructor
        public RemoteControl()
        {
            _onCommands = new ICommand[7];
            _offCommands = new ICommand[7];

            ICommand noCommand = new NoCommand();
            for (int i = 0; i < 7; i++)
            {
                _onCommands[i] = noCommand;
                _offCommands[i] = noCommand;
            }
            _undoCommand = noCommand;
        }

        public void SetCommand(int slot, ICommand onCommand, ICommand offCommand)
        {
            _onCommands[slot] = onCommand;
            _offCommands[slot] = offCommand;
        }

        public void OnButtonWasPushed(int slot)
        {
            _onCommands[slot].Execute();
            _undoCommand = _onCommands[slot];
        }

        public void OffButtonWasPushed(int slot)
        {
            _offCommands[slot].Execute();
            _undoCommand = _offCommands[slot];
        }

        public void UndoButtonWasPushed()
        {
            _undoCommand.Undo();
        }

        public override string ToString()
        {
            StringBuilder sb = new StringBuilder();
            sb.Append("\n------ Remote Control -------\n");
            for (int i = 0; i < _onCommands.Length; i++)
            {
                sb.Append("[slot " + i + "] " + _onCommands[i].GetType().Name
                    + "    " + _offCommands[i].GetType().Name + "\n");
            }
            sb.Append("[undo] " + _undoCommand.GetType().Name + "\n");
            return sb.ToString();
        }
    }

    #endregion Remote Control

    #region Commands

    public interface ICommand
    {
        void Execute();

        void Undo();
    }

    public class NoCommand : ICommand
    {
        public void Execute()
        {
        }

        public void Undo()
        {
        }
    }

    public class MacroCommand : ICommand
    {
        private ICommand[] _commands;

        public MacroCommand(ICommand[] commands)
        {
            this._commands = commands;
        }

        public void Execute()
        {
            for (int i = 0; i < _commands.Length; i++)
            {
                _commands[i].Execute();
            }
        }

        public void Undo()
        {
            for (int i = 0; i < _commands.Length; i++)
            {
                _commands[i].Undo();
            }
        }
    }

    public class TVOnCommand : ICommand
    {
        private TV _tv;

        public TVOnCommand(TV tv)
        {
            this._tv = tv;
        }

        public void Execute()
        {
            _tv.On();
            _tv.SetInputChannel();
        }

        public void Undo()
        {
            _tv.Off();
        }
    }

    public class TVOffCommand : ICommand
    {
        private TV _tv;

        public TVOffCommand(TV tv)
        {
            this._tv = tv;
        }

        public void Execute()
        {
            _tv.Off();
        }

        public void Undo()
        {
            _tv.On();
        }
    }

    public class StereoOnCommand : ICommand
    {
        private Stereo _stereo;

        public StereoOnCommand(Stereo stereo)
        {
            this._stereo = stereo;
        }

        public void Execute()
        {
            _stereo.On();
        }

        public void Undo()
        {
            _stereo.Off();
        }
    }

    public class StereoOffCommand : ICommand
    {
        private Stereo _stereo;

        public StereoOffCommand(Stereo stereo)
        {
            this._stereo = stereo;
        }

        public void Execute()
        {
            _stereo.Off();
        }

        public void Undo()
        {
            _stereo.On();
        }
    }

    public class StereoOnWithCDCommand : ICommand
    {
        private Stereo _stereo;

        public StereoOnWithCDCommand(Stereo stereo)
        {
            this._stereo = stereo;
        }

        public void Execute()
        {
            _stereo.On();
            _stereo.SetCD();
            _stereo.SetVolume(11);
        }

        public void Undo()
        {
            _stereo.Off();
        }
    }

    public class LivingroomLightOnCommand : ICommand
    {
        private Light _light;

        public LivingroomLightOnCommand(Light light)
        {
            this._light = light;
        }

        public void Execute()
        {
            _light.On();
        }

        public void Undo()
        {
            _light.Off();
        }
    }

    public class LivingroomLightOffCommand : ICommand
    {
        private Light _light;

        public LivingroomLightOffCommand(Light light)
        {
            this._light = light;
        }

        public void Execute()
        {
            _light.Off();
        }

        public void Undo()
        {
            _light.On();
        }
    }

    public class LightOnCommand : ICommand
    {
        private Light _light;

        public LightOnCommand(Light light)
        {
            this._light = light;
        }

        public void Execute()
        {
            _light.On();
        }

        public void Undo()
        {
            _light.Off();
        }
    }

    public class LightOffCommand : ICommand
    {
        private Light _light;

        public LightOffCommand(Light light)
        {
            this._light = light;
        }

        public void Execute()
        {
            _light.Off();
        }

        public void Undo()
        {
            _light.On();
        }
    }

    public class HottubOffCommand : ICommand
    {
        private Hottub _hottub;

        public HottubOffCommand(Hottub hottub)
        {
            this._hottub = hottub;
        }

        public void Execute()
        {
            _hottub.SetTemperature(98);
            _hottub.Off();
        }

        public void Undo()
        {
            _hottub.On();
        }
    }

    public class CeilingFanOffCommand : ICommand
    {
        private CeilingFan _ceilingFan;
        private CeilingFanSpeed _prevSpeed;

        public CeilingFanOffCommand(CeilingFan ceilingFan)
        {
            this._ceilingFan = ceilingFan;
        }

        public void Execute()
        {
            _prevSpeed = _ceilingFan.Speed;
            _ceilingFan.Off();
        }

        public void Undo()
        {
            switch (_prevSpeed)
            {
                case CeilingFanSpeed.High: _ceilingFan.high(); break;
                case CeilingFanSpeed.Medium: _ceilingFan.medium(); break;
                case CeilingFanSpeed.Low: _ceilingFan.low(); break;
                case CeilingFanSpeed.Off: _ceilingFan.Off(); break;
            }
        }
    }

    public class CeilingFanMediumCommand : ICommand
    {
        private CeilingFan _ceilingFan;
        private CeilingFanSpeed _prevSpeed;

        public CeilingFanMediumCommand(CeilingFan ceilingFan)
        {
            this._ceilingFan = ceilingFan;
        }

        public void Execute()
        {
            _prevSpeed = _ceilingFan.Speed;
            _ceilingFan.medium();
        }

        public void Undo()
        {
            switch (_prevSpeed)
            {
                case CeilingFanSpeed.High: _ceilingFan.high(); break;
                case CeilingFanSpeed.Medium: _ceilingFan.medium(); break;
                case CeilingFanSpeed.Low: _ceilingFan.low(); break;
                case CeilingFanSpeed.Off: _ceilingFan.Off(); break;
            }
        }
    }

    public class CeilingFanHighCommand : ICommand
    {
        private CeilingFan _ceilingFan;
        private CeilingFanSpeed _prevSpeed;

        public CeilingFanHighCommand(CeilingFan ceilingFan)
        {
            this._ceilingFan = ceilingFan;
        }

        public void Execute()
        {
            _prevSpeed = _ceilingFan.Speed;
            _ceilingFan.high();
        }

        public void Undo()
        {
            switch (_prevSpeed)
            {
                case CeilingFanSpeed.High: _ceilingFan.high(); break;
                case CeilingFanSpeed.Medium: _ceilingFan.medium(); break;
                case CeilingFanSpeed.Low: _ceilingFan.low(); break;
                case CeilingFanSpeed.Off: _ceilingFan.Off(); break;
            }
        }
    }

    public class HottubOnCommand : ICommand
    {
        private Hottub _hottub;

        public HottubOnCommand(Hottub hottub)
        {
            this._hottub = hottub;
        }

        public void Execute()
        {
            _hottub.On();
            _hottub.SetTemperature(104);
            _hottub.Circulate();
        }

        public void Undo()
        {
            _hottub.Off();
        }
    }

    #endregion Commands

    #region TV, Tub, CeilingFan, etc

    public class Hottub
    {
        private bool _on;
        private int _temperature;

        public void On()
        {
            _on = true;
        }

        public void Off()
        {
            _on = false;
        }

        public void Circulate()
        {
            if (_on)
            {
                Console.WriteLine("Hottub is bubbling!");
            }
        }

        public void JetsOn()
        {
            if (_on)
            {
                Console.WriteLine("Hottub jets are on");
            }
        }

        public void JetsOff()
        {
            if (_on)
            {
                Console.WriteLine("Hottub jets are off");
            }
        }

        public void SetTemperature(int temperature)
        {
            if (temperature > this._temperature)
            {
                Console.WriteLine("Hottub is heating to a steaming " + temperature + " degrees");
            }
            else
            {
                Console.WriteLine("Hottub is cooling to " + temperature + " degrees");
            }
            this._temperature = temperature;
        }
    }

    public class TV
    {
        private string _location;
        private int _channel;

        public TV(string location)
        {
            this._location = location;
        }

        public void On()
        {
            Console.WriteLine(_location + " TV is on");
        }

        public void Off()
        {
            Console.WriteLine(_location + " TV is off");
        }

        public void SetInputChannel()
        {
            this._channel = 3;
            Console.WriteLine(_location + " TV channel " + _channel + " is set for DVD");
        }
    }

    public class Stereo
    {
        private string _location;

        public Stereo(string location)
        {
            this._location = location;
        }

        public void On()
        {
            Console.WriteLine(_location + " stereo is on");
        }

        public void Off()
        {
            Console.WriteLine(_location + " stereo is off");
        }

        public void SetCD()
        {
            Console.WriteLine(_location + " stereo is set for CD input");
        }

        public void setDVD()
        {
            Console.WriteLine(_location + " stereo is set for DVD input");
        }

        public void SetRadio()
        {
            Console.WriteLine(_location + " stereo is set for Radio");
        }

        public void SetVolume(int volume)
        {
            // code to set the volume
            // valid range: 1-11 (after all 11 is better than 10, right?)
            Console.WriteLine(_location + " Stereo volume set to " + volume);
        }
    }

    public class Light
    {
        private string _location;

        public Light(string location)
        {
            this._location = location;
        }

        public void On()
        {
            Level = 100;
            Console.WriteLine("Light is on");
        }

        public void Off()
        {
            Level = 0;
            Console.WriteLine("Light is off");
        }

        public void Dim(int level)
        {
            this.Level = level;
            if (Level == 0)
            {
                Off();
            }
            else
            {
                Console.WriteLine("Light is dimmed to " + level + "%");
            }
        }

        public int Level { get; private set; }
    }

    public class CeilingFan
    {
        private string _location;

        public CeilingFan(string location)
        {
            this._location = location;
        }

        public void high()
        {
            // turns the ceiling fan on to high
            Speed = CeilingFanSpeed.High;
            Console.WriteLine(_location + " ceiling fan is on high");
        }

        public void medium()
        {
            // turns the ceiling fan on to medium
            Speed = CeilingFanSpeed.Medium;
            Console.WriteLine(_location + " ceiling fan is on medium");
        }

        public void low()
        {
            // turns the ceiling fan on to low
            Speed = CeilingFanSpeed.Low;
            Console.WriteLine(_location + " ceiling fan is on low");
        }

        public void Off()
        {
            // turns the ceiling fan off
            Speed = CeilingFanSpeed.Off;
            Console.WriteLine(_location + " ceiling fan is off");
        }

        public CeilingFanSpeed Speed { get; private set; }
    }

    public enum CeilingFanSpeed
    {
        High,
        Medium,
        Low,
        Off
    }

    #endregion TV, Tub, CeilingFan, etc
```

## Реализация на JAVA ##

```java
    TODO
```