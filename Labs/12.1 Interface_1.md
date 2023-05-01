# interface

```cs
namespace InterfaceExamples
{
    class Television
    {
        public int Channel { get; set; }
        public bool Status { get; set; }
    }
    class Lamp
    {
        public bool Status { get; set; }
    }
    interface IRemoteControl
    {
        void TurnOn();
        void TurnOff();
        void ChannelUp();
        void ChannelDown();

    }
    class SonyTV : Television, IRemoteControl
    {
        public void ChannelDown()
        {
            if (Channel > 0)
                Channel--;
            Console.WriteLine("Channel = {0}", Channel);
        }

        public void ChannelUp()
        {
            Channel++;
            Console.WriteLine("Channel = {0}", Channel);
        }

        public void TurnOff()
        {
            if (Status == true)
                Status = false;
            Console.WriteLine("Turning off {0}", this.GetType().Name);
        }

        public void TurnOn()
        {
            if (Status == false)
                Status = true;
            Console.WriteLine("Turning on {0}", this.GetType().Name);
        }
    }
    class BedLamp : Lamp, IRemoteControl
    {
        public void ChannelDown()
        {
            Console.WriteLine("Sorry, Lamp cannot change channel");
        }

        public void ChannelUp()
        {
            Console.WriteLine("Sorry, Lamp cannot change channel");
        }

        public void TurnOff()
        {
            if (Status == true)
                Status = false;
            Console.WriteLine("Turning off {0}", this.GetType().Name);
        }

        public void TurnOn()
        {
            if (Status == false)
                Status = true;
            Console.WriteLine("Turning on {0}", this.GetType().Name);
        }
    }

    internal class Program
    {
        static void Main(string[] args)
        {
            var mySony = new SonyTV();
            var status = mySony.Status == true ? "Turn on" : "Turn Off";
            Console.WriteLine($"Now, my sonyTV is {status} and play channel {mySony.Channel}");
            mySony.TurnOn();
            mySony.ChannelUp();

            IRemoteControl refRemote = mySony;
            refRemote.ChannelUp();
            refRemote.ChannelUp();
            refRemote.TurnOff();

            BedLamp myLamp = new BedLamp();
            refRemote = myLamp;

            refRemote.TurnOn();
            refRemote.ChannelUp();
        }
    }
}
```


