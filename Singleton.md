# Singleton

Singleton

Beschreibung:
Stellt sicher, dass eine Klasse nur eine Instanz hat, und bietet einen globalen Zugriffspunkt darauf.

C# Beispiel:
```csharp
public class Singleton
{
    private static Singleton _instance;
    private static readonly object _lock = new object();

    private Singleton() { }
    public static Singleton Instance
    {
        get
        {
            lock(_lock)
            {
                if (_instance == null)
                {
                    _instance = new Singleton();
                }
                return _instance;
            }
        }
    }
}
```