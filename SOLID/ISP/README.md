# Interface-Segregation-Principle
## Overview
Interface segregation is a principle in object-oriented design that states that clients should not be forced to depend on interfaces they do not use. This principle is closely related to the Single Responsibility Principle, which states that a class should have only one reason to change.
## Example
In this example, the IWorker interface defines three methods: Work(), Eat(), and Sleep(). The Worker class implements all three of these methods, as it is a human worker and needs to perform all three activities. However, the Robot class also implements the IWorker interface, but it does not need to eat or sleep. In this case, it would be more appropriate to create separate interfaces for each concern, such as IWorker for the Work() method and IEat for the Eat() method. This would allow the Robot class to implement only the IWorker interface and not be forced to depend on methods it does not need.
```c#
// Incorrect implementation
public interface IWorker
{
    void Work();
    void Eat();
    void Sleep();
}

public class Worker : IWorker
{
    public void Work()
    {
        // code to perform work
    }

    public void Eat()
    {
        // code to eat
    }

    public void Sleep()
    {
        // code to sleep
    }
}

public class Robot : IWorker
{
    public void Work()
    {
        // code to perform work
    }

    public void Eat()
    {
        // code to eat (not applicable to robots)
    }

    public void Sleep()
    {
        // code to sleep (not applicable to robots)
    }
}

// Corrected implementation
public interface IWorker
{
    void Work();
}

public interface IEat
{
    void Eat();
}

public interface ISleep
{
    void Sleep();
}

public class Worker : IWorker, IEat, ISleep
{
    public void Work()
    {
        // code to perform work
    }

    public void Eat()
    {
        // code to eat
    }

    public void Sleep()
    {
        // code to sleep
    }
}

public class Robot : IWorker
{
    public void Work()
    {
        // code to perform work
    }
}
```
In this refactored version of the code, the IWorker interface only contains the Work() method, the IEat interface only contains the Eat() method, and the ISleep interface only contains the Sleep() method. The Worker class still implements all three interfaces, as it needs to perform all three activities. However, the Robot class only needs to implement the IWorker interface, as it does not need to eat or sleep. This allows the Robot class to depend only on the methods that it actually needs, and makes the interfaces more focused and easier to understand and use.
