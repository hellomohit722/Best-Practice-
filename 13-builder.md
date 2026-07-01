# Decorators (Simple Notes)

## What is a Decorator?

A **decorator** is a design pattern or language feature that allows you
to **add new behavior to an object or function without changing its
original code**.

Think of it like adding toppings to a pizza: - Pizza = Original
object/function - Cheese, olives = Extra features - The pizza remains
the same, but gains new functionality.

------------------------------------------------------------------------

## Why Use Decorators?

-   Reuse existing code
-   Add features without modifying original code
-   Follow the **Open/Closed Principle**
-   Keep code clean and maintainable

------------------------------------------------------------------------

## Real-Life Example

Imagine a coffee shop.

-   Basic Coffee
-   Coffee + Milk
-   Coffee + Sugar
-   Coffee + Milk + Sugar

Instead of creating a new class for every combination, decorators add
features one by one.

------------------------------------------------------------------------

## Decorator Pattern Components

1.  **Component** -- Common interface
2.  **Concrete Component** -- Original implementation
3.  **Decorator** -- Wraps a component
4.  **Concrete Decorator** -- Adds extra behavior

------------------------------------------------------------------------

## Simple Java Example

``` java
interface Coffee {
    String getDescription();
}

class BasicCoffee implements Coffee {
    public String getDescription() {
        return "Basic Coffee";
    }
}

class MilkDecorator implements Coffee {
    private Coffee coffee;

    MilkDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    public String getDescription() {
        return coffee.getDescription() + " + Milk";
    }
}

public class Main {
    public static void main(String[] args) {
        Coffee coffee = new MilkDecorator(new BasicCoffee());
        System.out.println(coffee.getDescription());
    }
}
```

### Output

    Basic Coffee + Milk

------------------------------------------------------------------------

## Advantages

-   Easy to extend functionality
-   Avoids large inheritance hierarchies
-   Flexible and reusable
-   Supports the Open/Closed Principle

------------------------------------------------------------------------

## Disadvantages

-   Can create many small classes
-   Slightly harder to understand for beginners

------------------------------------------------------------------------

## When to Use

-   Adding logging
-   Authentication
-   Input validation
-   Caching
-   Compression
-   Encryption

------------------------------------------------------------------------

## Quick Revision

-   Decorator **adds functionality**
-   Original class is **not modified**
-   Works by **wrapping** another object
-   Promotes **composition over inheritance**

------------------------------------------------------------------------

# Interview Questions

### 1. What is the Decorator Pattern?

A structural design pattern that adds behavior dynamically without
modifying existing code.

### 2. Why is it better than inheritance?

It avoids creating many subclasses and allows flexible combinations of
features.

### 3. What principle does it follow?

Open/Closed Principle.

### 4. Give one real-life example.

Coffee with optional milk, sugar, or chocolate toppings.

