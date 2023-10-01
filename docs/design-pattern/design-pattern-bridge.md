# Bridge

The Bridge pattern decouples an abstraction from its implementation, so that the two can vary independently.

## Example

### Workshop

```java
public interface Workshop {
    abstract public void work();
}

public class Produce implements Workshop {
    @Override
    public void work()
    {
        System.out.print("Produced");
    }
}

public class Assemble implements Workshop {
    @Override
    public void work()
    {
        System.out.print(" And");
        System.out.println(" Assembled.");
    }
}
```

### Vehicle

```java
public abstract class Vehicle {
    protected Workshop workShop1;
    protected Workshop workShop2;

    protected Vehicle(Workshop workShop1, Workshop workShop2)
    {
        this.workShop1 = workShop1;
        this.workShop2 = workShop2;
    }

    abstract public void manufacture();
}

public class Bike extends Vehicle {
    public Bike(Workshop workShop1, Workshop workShop2)
    {
        super(workShop1, workShop2);
    }

    @Override
    public void manufacture()
    {
        System.out.print("Bike ");
        workShop1.work();
        workShop2.work();
    }
}

public class Car extends Vehicle {
    public Car(Workshop workShop1, Workshop workShop2)
    {
        super(workShop1, workShop2);
    }

    @Override
    public void manufacture()
    {
        System.out.print("Car ");
        workShop1.work();
        workShop2.work();
    }
}
```

### Client

```java
public class Client {
    public void run() {
        Vehicle vehicle1 = new Car(new Produce(), new Assemble());
        vehicle1.manufacture();
        Vehicle vehicle2 = new Bike(new Produce(), new Assemble());
        vehicle2.manufacture();
    }
}
```

Output.

```raw
Car Produced And Assembled.
Bike Produced And Assembled.
```

## Source files

* [Source files for Bridge Pattern on GitHub](https://github.com/jojozhuang/design-patterns-java/tree/master/design-pattern-bridge)

## References

* [Bridge Design Pattern](https://www.geeksforgeeks.org/bridge-design-pattern/)
