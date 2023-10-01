# Prototype

Prototype pattern refers to creating duplicate object while keeping performance in mind. Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

## Example of Implementation

## Base Class

```java
public abstract class Shape implements Cloneable {

    private String id;
    protected String type;

    abstract void draw();

    public String getType(){
        return type;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public Object clone() {
        Object clone = null;

        try {
            clone = super.clone();

        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }

        return clone;
    }
}
```

## Classes

```java
public class Circle extends Shape {
    public Circle(){
        type = "Circle";
    }

    @Override
    public void draw() {
        System.out.println("Shape: Circle");
    }
}

public class Rectangle extends Shape {

    public Rectangle(){
        type = "Rectangle";
    }

    @Override
    public void draw() {
        System.out.println("Shape: Rectangle");
    }
}

public class Square extends Shape {

    public Square(){
        type = "Square";
    }

    @Override
    public void draw() {
        System.out.println("Shape: Square");
    }
}
```

### Usage

```java
public class ShapeCache {
    private static Map<String, Shape> mapShape = new HashMap<>();

    public static Shape getShape(String shapeId) {
        Shape cachedShape = mapShape.get(shapeId);
        return (Shape) cachedShape.clone();
    }

    public static void loadCache() {
        Circle circle = new Circle();
        circle.setId("1");
        mapShape.put(circle.getId(), circle);

        Square square = new Square();
        square.setId("2");
        mapShape.put(square.getId(), square);

        Rectangle rectangle = new Rectangle();
        rectangle.setId("3");
        mapShape.put(rectangle.getId(), rectangle);
    }
}
```

Get new object from cache without directly creating new instance.

```java
public class Client {
    public void run() {
        ShapeCache.loadCache();

        Shape clonedShape = (Shape) ShapeCache.getShape("1");
        System.out.println("Shape : " + clonedShape.getType());

        Shape clonedShape2 = (Shape) ShapeCache.getShape("2");
        System.out.println("Shape : " + clonedShape2.getType());

        Shape clonedShape3 = (Shape) ShapeCache.getShape("3");
        System.out.println("Shape : " + clonedShape3.getType());
    }
}
```

Output.

```raw
Shape : Circle
Shape : Square
Shape : Rectangle
```

## Source files

* [Source files for Prototype Pattern on GitHub](https://github.com/jojozhuang/design-patterns-java/tree/master/design-pattern-prototype)

## References

* [Design Patterns - Prototype Pattern](https://www.tutorialspoint.com/design_pattern/prototype_pattern.htm)
