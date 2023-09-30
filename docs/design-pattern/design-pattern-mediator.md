# Mediator

The Mediator pattern is used to provide a centralized communication medium between different objects in a system.

## Example

### User

```java
public class User {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public User(String name){
        this.name  = name;
    }

    public void sendMessage(String message){
        ChatRoom.showMessage(this,message);
    }
}
```

### ChatRoom

```java
public class ChatRoom {
    public static void showMessage(User user, String message){
        System.out.println(new Date().toString() + " [" + user.getName() + "] : " + message);
    }
}
```

### Client

```java
public class Client {
    public void run() {
        User robert = new User("Robert");
        User john = new User("John");

        robert.sendMessage("Hi! John!");
        john.sendMessage("Hello! Robert!");
    }
}
```

Output.

```raw
Fri Nov 30 16:08:46 PST 2018 [Robert] : Hi! John!
Fri Nov 30 16:08:46 PST 2018 [John] : Hello! Robert!
```

## Source files

* [Source files for Mediator Pattern on GitHub](https://github.com/jojozhuang/design-patterns-java/tree/master/design-pattern-mediator)

## References

* [Design Patterns - Mediator Pattern](https://www.tutorialspoint.com/design_pattern/mediator_pattern.htm)
* [Mediator Design Pattern in Java](https://www.journaldev.com/1730/mediator-design-pattern-java)
