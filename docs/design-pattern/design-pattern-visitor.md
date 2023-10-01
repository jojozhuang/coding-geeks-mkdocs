# Visitor

The Visitor pattern represents an operation to be performed on the elements of an object structure without changing the classes on which it operates.

## Example

### Computer Part

```java
public interface ComputerPart {
   public void accept(ComputerPartVisitor computerPartVisitor);
}

public class Keyboard implements ComputerPart {

   @Override
   public void accept(ComputerPartVisitor computerPartVisitor) {
      computerPartVisitor.visit(this);
   }
}

public class Monitor implements ComputerPart {

   @Override
   public void accept(ComputerPartVisitor computerPartVisitor) {
      computerPartVisitor.visit(this);
   }
}

public class Mouse implements ComputerPart {

   @Override
   public void accept(ComputerPartVisitor computerPartVisitor) {
      computerPartVisitor.visit(this);
   }
}

public class Computer implements ComputerPart {

   ComputerPart[] parts;

   public Computer(){
      parts = new ComputerPart[] {new Mouse(), new Keyboard(), new Monitor()};  
   }

   @Override
   public void accept(ComputerPartVisitor computerPartVisitor) {
      for (int i = 0; i < parts.length; i++) {
         parts[i].accept(computerPartVisitor);
      }
      computerPartVisitor.visit(this);
   }
}
```

### Visitor class

```java
public interface ComputerPartVisitor {
    public void visit(Computer computer);
    public void visit(Mouse mouse);
    public void visit(Keyboard keyboard);
    public void visit(Monitor monitor);
}

public class ComputerPartDisplayVisitor implements ComputerPartVisitor {

   @Override
   public void visit(Computer computer) {
      System.out.println("Displaying Computer.");
   }

   @Override
   public void visit(Mouse mouse) {
      System.out.println("Displaying Mouse.");
   }

   @Override
   public void visit(Keyboard keyboard) {
      System.out.println("Displaying Keyboard.");
   }

   @Override
   public void visit(Monitor monitor) {
      System.out.println("Displaying Monitor.");
   }
}
```

### Client

```java
public class Client {
    public void run() {
        ComputerPart computer = new Computer();
        computer.accept(new ComputerPartDisplayVisitor());
    }
}
```

Output.

```raw
Displaying Mouse.
Displaying Keyboard.
Displaying Monitor.
Displaying Computer.
```

## Source files

* [Source files for Visitor Pattern on GitHub](https://github.com/jojozhuang/design-patterns-java/tree/master/design-pattern-visitor)

## References

* [Design Patterns - Visitor Pattern](https://www.tutorialspoint.com/design_pattern/visitor_pattern.htm)
* [Visitor Design Pattern](https://sourcemaking.com/design_patterns/visitor)
