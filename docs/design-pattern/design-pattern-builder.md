# Builder

The Builder pattern separates the construction of a complex object from its representation so that the same construction process can create different representations.

## Example

### Pizza

```java
public class Pizza {
    private String dough = "";
    private String sauce = "";
    private String topping = "";

    public void setDough(String dough) {
        this.dough = dough;
    }

    public void setSauce(String sauce) {
        this.sauce = sauce;
    }

    public void setTopping(String topping) {
        this.topping = topping;
    }

    @Override
    public String toString() {
        return "Dough: " + dough + ",Sauce: " + sauce + ",Topping: " + topping;
    }
}
```

### Pizza Builder

```java
public abstract class PizzaBuilder {
    protected Pizza pizza;

    public Pizza getPizza() {
        return pizza;
    }

    public void createPizza() {
        pizza = new Pizza();
    }

    public abstract void buildDough();
    public abstract void buildSauce();
    public abstract void buildTopping();
}

public class CheesePizzaBuilder extends PizzaBuilder {
    public void buildDough() {
        pizza.setDough("cross");
    }

    public void buildSauce() {
        pizza.setSauce("tomato");
    }

    public void buildTopping() {
        pizza.setTopping("cheese");
    }
}

public class PepperoniPizzaBuilder extends PizzaBuilder {
    public void buildDough() {
        pizza.setDough("pan baked");
    }

    public void buildSauce() {
        pizza.setSauce("hot");
    }

    public void buildTopping() {
        pizza.setTopping("pepperoni + salami");
    }
}
```

### Waiter

```java
public class Waiter {
    private PizzaBuilder pizzaBuilder;

    public void setPizzaBuilder(PizzaBuilder pb) {
        pizzaBuilder = pb;
    }

    public Pizza getPizza() {
        return pizzaBuilder.getPizza();
    }

    public void constructPizza() {
        pizzaBuilder.createPizza();
        pizzaBuilder.buildDough();
        pizzaBuilder.buildSauce();
        pizzaBuilder.buildTopping();
    }
}
```

### Client

```java
public class Client {
    public void run() {
        Waiter waiter = new Waiter();
        PizzaBuilder cheesePizzaBuilder = new CheesePizzaBuilder();
        PizzaBuilder pepperoniPizzaBuilder = new PepperoniPizzaBuilder();

        waiter.setPizzaBuilder( pepperoniPizzaBuilder );
        waiter.constructPizza();

        Pizza pizza = waiter.getPizza();
        System.out.println(pizza);
    }
}
```

Output

```raw
Dough: pan baked,Sauce: hot,Topping: pepperoni + salami
```

## Source files

* [Source files for Builder Pattern on GitHub](https://github.com/jojozhuang/design-patterns-java/tree/master/design-pattern-builder)

## References

* [Builder Design Pattern](https://sourcemaking.com/design_patterns/builder)
* [Builder in Java](https://sourcemaking.com/design_patterns/builder/java/2)
