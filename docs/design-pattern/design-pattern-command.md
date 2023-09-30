# Command

The Command pattern allows requests to be encapsulated as objects, thereby allowing clients to be parametrized with different requests. Command decouples the object that invokes the operation from the one that knows how to perform it.

## Example

### Command interface

```java
public interface Command {
    void execute();
}

public class Buy implements Command {
    public void execute() {
        System.out.println("Buy stock");
    }
}

public class Sell implements Command {
    public void execute() {
        System.out.println("Sell stock");
    }
}
```

### Broker

```java
public class Broker {
    private List<Command> cmdList = new ArrayList<>();

    public void acceptCommand(Command cmd){
        cmdList.add(cmd);
    }

    public void executeCommand(){
        for (Command cmd : cmdList) {
            cmd.execute();
        }
        cmdList.clear();
    }
}
```

### Client

```java
public class Client {
    public void run() {
        Buy buyStock = new Buy();
        Sell sellStock = new Sell();

        Broker broker = new Broker();
        broker.acceptCommand(buyStock);
        broker.acceptCommand(sellStock);

        broker.executeCommand();
    }
}
```

Output.

```raw
Buy stock
Sell stock
```

## Source Files

* [Source files for Command Pattern on GitHub](https://github.com/jojozhuang/design-patterns-java/tree/master/design-pattern-command)

## References

* [Design Patterns - Command Pattern](https://www.tutorialspoint.com/design_pattern/command_pattern.htm)
