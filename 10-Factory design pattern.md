# Factory Design Pattern

The **Factory Design Pattern** provides a way to create objects without exposing the instantiation logic to the client.

### Goals

- Encapsulate object creation
- Follow **Open/Closed Principle**
- Object creation and business logic should be **separate**, which is why we use a factory class.
- The main goal is to **decouple the client** from the application internals.

## Types of Factory Patterns

Factories are generally categorized into **three types**.

### 1. Simple Factory (**not an official GoF pattern**):

A **simple factory class** is responsible for creating objects based on input parameters (usually using `if` / `switch`).

```java
// --- Burger Interface ---
interface Burger {
    void prepare();
}

// --- Concrete Burger Implementations ---
class BasicBurger implements Burger {
    @Override
    public void prepare() {
        System.out.println("Preparing Basic Burger with bun, patty, and ketchup!");
    }
}

class StandardBurger implements Burger {
    @Override
    public void prepare() {
        System.out.println("Preparing Standard Burger with bun, patty, cheese, and lettuce!");
    }
}

class PremiumBurger implements Burger {
    @Override
    public void prepare() {
        System.out.println("Preparing Premium Burger with gourmet bun, premium patty, cheese, lettuce, and secret sauce!");
    }
}

// --- Burger Factory ---
class BurgerFactory {
    public Burger createBurger(String type) {
        if (type.equalsIgnoreCase("basic")) {
            return new BasicBurger();
        } else if (type.equalsIgnoreCase("standard")) {
            return new StandardBurger();
        } else if (type.equalsIgnoreCase("premium")) {
            return new PremiumBurger();
        } else {
            System.out.println("Invalid burger type!");
            return null;
        }
    }
}

// --- Main Class ---
public class SimpleFactory {
    public static void main(String[] args) {
        String type = "standard";

        BurgerFactory myBurgerFactory = new BurgerFactory();

        Burger burger = myBurgerFactory.createBurger(type);

        if (burger != null) {
            burger.prepare();
        }
    }
}

```

### Advantages
- Simple and easy to understand
- Centralized object creation logic

### Disadvantages
- Violates Open/Closed Principle
- Factory class becomes large as new types are added

### Use Case
- Small applications
- Limited number of object types


### 2. factory method :

Defines an interface or abstract class for creating an object, but allows subclasses to decide which class to instantiate.

```java
// Product Interface and subclasses
interface Burger {
    void prepare();
}

//---------------------Tasty burger----------------------->
//BasicBurger
//StandardBurger
//PremiumBurger
//----------------------Healthy burger-------------------->
//BasicWheatBurger
//StandardWheatBurger
//PremiumWheatBurger

// Factory Interface and Concrete Factories
interface BurgerFactory {
    Burger createBurger(String type);
}

class SinghBurger implements BurgerFactory {
    public Burger createBurger(String type) {
        if (type.equalsIgnoreCase("basic")) {
            return new BasicBurger();
        } else if (type.equalsIgnoreCase("standard")) {
            return new StandardBurger();
        } else if (type.equalsIgnoreCase("premium")) {
            return new PremiumBurger();
        } else {
            System.out.println("Invalid burger type!");
            return null;
        }
    }
}

class KingBurger implements BurgerFactory {
    public Burger createBurger(String type) {
        if (type.equalsIgnoreCase("basic")) {
            return new BasicWheatBurger();
        } else if (type.equalsIgnoreCase("standard")) {
            return new StandardWheatBurger();
        } else if (type.equalsIgnoreCase("premium")) {
            return new PremiumWheatBurger();
        } else {
            System.out.println("Invalid burger type!");
            return null;
        }
    }
}

// Main Class
public class FactoryMethod {
    public static void main(String[] args) {
        String type = "basic";

        BurgerFactory myFactory = new SinghBurger();
        Burger burger = myFactory.createBurger(type);

        if (burger != null) {
            burger.prepare();
        }
    }
}

```
### Advantages
- Follows Open/Closed Principle
- Eliminates conditional logic

### Disadvantages
- Increases number of classes
- Slightly more complex design

### Use Case
- Frameworks and libraries
- When object creation logic varies by subclass


### 3. abstract factory method :

Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

```java
// --- Product 1 --> Burger ---
interface Burger {
    void prepare();
}

//BasicBurger
//StandardBurger
//PremiumBurger
//BasicWheatBurger
//StandardWheatBurger
//PremiumWheatBurger

// --- Product 2 --> GarlicBread ---
interface GarlicBread {
    void prepare();
}

//BasicGarlicBread
//CheeseGarlicBread
//BasicWheatGarlicBread
//CheeseWheatGarlicBread

// --- Abstract Factory ---
interface MealFactory {
    Burger createBurger(String type);
    GarlicBread createGarlicBread(String type);
}

// --- Concrete Factory 1 ---
class SinghBurger implements MealFactory {
    public Burger createBurger(String type) {
        if (type.equalsIgnoreCase("basic")) {
            return new BasicBurger();
        } else if (type.equalsIgnoreCase("standard")) {
            return new StandardBurger();
        } else if (type.equalsIgnoreCase("premium")) {
            return new PremiumBurger();
        } else {
            System.out.println("Invalid burger type!");
            return null;
        }
    }

    public GarlicBread createGarlicBread(String type) {
        if (type.equalsIgnoreCase("basic")) {
            return new BasicGarlicBread();
        } else if (type.equalsIgnoreCase("cheese")) {
            return new CheeseGarlicBread();
        } else {
            System.out.println("Invalid Garlic bread type!");
            return null;
        }
    }
}

// --- Concrete Factory 2 ---
class KingBurger implements MealFactory {
    public Burger createBurger(String type) {
        if (type.equalsIgnoreCase("basic")) {
            return new BasicWheatBurger();
        } else if (type.equalsIgnoreCase("standard")) {
            return new StandardWheatBurger();
        } else if (type.equalsIgnoreCase("premium")) {
            return new PremiumWheatBurger();
        } else {
            System.out.println("Invalid burger type!");
            return null;
        }
    }

    public GarlicBread createGarlicBread(String type) {
        if (type.equalsIgnoreCase("basic")) {
            return new BasicWheatGarlicBread();
        } else if (type.equalsIgnoreCase("cheese")) {
            return new CheeseWheatGarlicBread();
        } else {
            System.out.println("Invalid Garlic bread type!");
            return null;
        }
    }
}

// --- Main Class ---
public class AbstractFactory {
    public static void main(String[] args) {
        String burgerType = "basic";
        String garlicBreadType = "cheese";

        MealFactory mealFactory = new SinghBurger();

        Burger burger = mealFactory.createBurger(burgerType);
        GarlicBread garlicBread = mealFactory.createGarlicBread(garlicBreadType);

        if (burger != null) burger.prepare();
        if (garlicBread != null) garlicBread.prepare();
    }
}

```

### Advantages
- Ensures consistency among related objects
- Strong abstraction

### Disadvantages
- Hard to add new product types
- High complexity

### Use Case
- UI toolkits
- Cross-platform applications
