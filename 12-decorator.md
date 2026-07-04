## Decorator

<img width="1162" height="738" alt="image" src="https://github.com/user-attachments/assets/6968c4e5-36f5-46cb-b35a-d7faa48412ff" />


# Decorator Pattern : 
The Decorator Pattern is a structural design pattern that allows you to add new behavior to an object dynamically (at runtime) without modifying its existing code.

# Core Idea:
* Composition over inheritance
* Extend behavior without subclass explosion
* Behaviors can be combined flexibly

`is a` inheritence use to behave like them , `has a` composition relationship for changing behavoiur.

        Component
            ↑
    ConcreteComponent
            ↑
        Decorator
            ↑
     ConcreteDecorator

```java
// Component Interface: defines a common interface for Mario and all power-up decorators.
interface Character {
    String getAbilities();
}

// Concrete Component: Basic Mario character with no power-ups.
class Mario implements Character {
    public String getAbilities() {
        return "Mario";
    }
}

// Abstract Decorator: CharacterDecorator "is-a" Character and "has-a" Character.
abstract class CharacterDecorator implements Character {
    protected Character character;  // Wrapped component

    public CharacterDecorator(Character c) {
        this.character = c;
    }
}

// Concrete Decorator: Height-Increasing Power-Up.
class HeightUp extends CharacterDecorator {
    public HeightUp(Character c) {
        super(c);
    }

    public String getAbilities() {
        return character.getAbilities() + " with HeightUp";
    }
}

// Concrete Decorator: Gun Shooting Power-Up.
class GunPowerUp extends CharacterDecorator {
    public GunPowerUp(Character c) {
        super(c);
    }

    public String getAbilities() {
        return character.getAbilities() + " with Gun";
    }
}

// Concrete Decorator: Star Power-Up (temporary ability).
class StarPowerUp extends CharacterDecorator {
    public StarPowerUp(Character c) {
        super(c);
    }

    public String getAbilities() {
        return character.getAbilities() + " with Star Power (Limited Time)";
    }
}

public class DecoratorPattern {
    public static void main(String[] args) {
        // Create a basic Mario character.
        Character mario = new Mario();
        System.out.println("Basic Character: " + mario.getAbilities());

        // Decorate Mario with a HeightUp power-up.
        mario = new HeightUp(mario);
        System.out.println("After HeightUp: " + mario.getAbilities());

        // Decorate Mario further with a GunPowerUp.
        mario = new GunPowerUp(mario);
        System.out.println("After GunPowerUp: " + mario.getAbilities());

        // Finally, add a StarPowerUp decoration.
        mario = new StarPowerUp(mario);
        System.out.println("After StarPowerUp: " + mario.getAbilities());
    }
}

```

# Follows SOLID Principles
| Principle | How Decorator Helps                          |
| --------- | -------------------------------------------- |
| OCP       | Add behavior without modifying existing code |
| SRP       | Each decorator has one responsibility        |
| DIP       | Depends on abstraction (`Coffee`)            |


# ✅ Use when:
* You need to add responsibilities dynamically
* Subclassing leads to class explosion
* You want flexible feature combinations

# ❌ Avoid when:
* You need to add behavior to all objects globally
* Excessive decorators make debugging hard

# Advantages
* Open/Closed Principle
* Runtime flexibility
* Cleaner than large inheritance trees
* Behavior reuse

# Disadvantages
* Many small classes
* Harder to debug (nested objects)
* Order of decorators may matter

# Decorator vs Proxy vs Adapter (Quick Comparison)
| Pattern   | Purpose           |
| --------- | ----------------- |
| Decorator | Add behavior      |
| Proxy     | Control access    |
| Adapter   | Convert interface |

