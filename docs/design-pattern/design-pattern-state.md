---
layout: tutorial
key: programming
title: "Design Pattern - State"
index: 2928
subcategory: design-pattern
date: 2016-05-28
tags: [State Pattern]
---

> Behavioral Pattern: State Pattern.

# State

The State pattern allows an object to change its behavior when its internal state changes.

## Example

### State

```java
public interface State {
    public void doAction(Context context);
}

public class StartState implements State {

    public void doAction(Context context) {
        System.out.println("Player is in start state");
        context.setState(this);
    }

    public String toString(){
        return "Start State";
    }
}

public class StopState implements State {

    public void doAction(Context context) {
        System.out.println("Player is in stop state");
        context.setState(this);
    }

    public String toString(){
        return "Stop State";
    }
}
```

### Context

```java
public class Context {
    private State state;

    public Context(){
        state = null;
    }

    public void setState(State state){
        this.state = state;
    }

    public State getState(){
        return state;
    }
}
```

Output

```raw
Player is in start state
Start State
Player is in stop state
Stop State
```

## Source files

* [Source files for State Pattern on GitHub](https://github.com/jojozhuang/design-patterns-java/tree/master/design-pattern-state)

## References

* [Design Patterns - State Pattern](https://www.tutorialspoint.com/design_pattern/state_pattern.htm)
* [State Design Pattern](https://sourcemaking.com/design_patterns/state)
