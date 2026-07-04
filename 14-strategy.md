# Strategy Design Pattern

<img width="1142" height="520" alt="image" src="https://github.com/user-attachments/assets/a5ebf00f-c75c-411c-bed8-852c5b3c2966" />

# Problem with inheritence:
* code reuse
* to add a new feature a lot of change were required
* Breaking OCP

# Strategy design pattern :-

Defines a family of algorithms, put them into separate classes so that they can be changed at run time.

if we want to very algo in run time then strategy or if object creation then factory

<img width="1013" height="646" alt="image" src="https://github.com/user-attachments/assets/fa4e5e9c-995e-4c28-9768-f8ab0f501446" />

The one who use the algo are client class, strategies are like talking, walking

# Common Issues Without Strategy
* Large if-else or switch statements
* Multiple subclasses for each variation of behavior
* Tight coupling between behavior and the object
* Violations of Open/Closed Principle

```java
// --- Strategy Interface for Walk ---
interface WalkableRobot {
    void walk();
}

// --- Concrete Strategies for walk ---
class NormalWalk implements WalkableRobot {
    public void walk() {
        System.out.println("Walking normally...");
    }
}

class NoWalk implements WalkableRobot {
    public void walk() { System.out.println("Cannot walk.");}
}

interface TalkableRobot {
    void talk();
}

class NormalTalk implements TalkableRobot {
    public void talk() {System.out.println("Talking normally...");}
}

class NoTalk implements TalkableRobot {
    public void talk() {System.out.println("Cannot talk.");}
}

interface FlyableRobot {
    void fly();
}

class NormalFly implements FlyableRobot {
    public void fly() {System.out.println("Flying normally...");}
}

class NoFly implements FlyableRobot {
    public void fly() {System.out.println("Cannot fly.");}
}

// --- Robot Base Class ---
abstract class Robot {
    protected WalkableRobot walkBehavior;
    protected TalkableRobot talkBehavior;
    protected FlyableRobot flyBehavior;

    public Robot(WalkableRobot w, TalkableRobot t, FlyableRobot f) {
        this.walkBehavior = w;
        this.talkBehavior = t;
        this.flyBehavior = f;
    }

    public void walk() {
        walkBehavior.walk();
    }

    public void talk() {
        talkBehavior.talk();
    }

    public void fly() {
        flyBehavior.fly();
    }

    public abstract void projection(); // Abstract method for subclasses
}

// --- Concrete Robot Types ---
class CompanionRobot extends Robot {
    public CompanionRobot(WalkableRobot w, TalkableRobot t, FlyableRobot f) {
        super(w, t, f);
    }

    public void projection() {
        System.out.println("Displaying friendly companion features...");
    }
}

class WorkerRobot extends Robot {
    public WorkerRobot(WalkableRobot w, TalkableRobot t, FlyableRobot f) {
        super(w, t, f);
    }

    public void projection() {
        System.out.println("Displaying worker efficiency stats...");
    }
}

// --- Main Function ---
public class StrategyDesignPattern {
    public static void main(String[] args) {
        Robot robot1 = new CompanionRobot(new NormalWalk(), new NormalTalk(), new NoFly());
        robot1.walk();
        robot1.talk();
        robot1.fly();
        robot1.projection();

        System.out.println("--------------------");

        Robot robot2 = new WorkerRobot(new NoWalk(), new NoTalk(), new NormalFly());
        robot2.walk();
        robot2.talk();
        robot2.fly();
        robot2.projection();
    }
}

```
# ✅ Use when:
* You have multiple variants of an algorithm
* Behavior must change dynamically
* You want to eliminate conditional logic
* You need clean separation of concerns

# ❌ Avoid when:
* Only one algorithm exists
* Algorithms rarely change
* Added complexity isn’t justified

# Conclusion
* Encapsulate what varies & keep it separate from what remains same.
* Solution to inheritance is not more inheritance.
* Composition should be favoured over inheritance.
* Code to interface & not to concrete.
* Do NOT repeat yourself (DRY).
-------------------------------------------------------------------------------------------------------------------------
Create a payment gateway system that supports multiple payment methods like 'CreditCardPayment', 'PayPalPayment', and 'BitcoinPayment'. 

Use the Strategy pattern to dynamically switch between payment methods.

🧠 How This Uses Strategy Pattern
| Role                | Class                                                  |
| ------------------- | ------------------------------------------------------ |
| Strategy Interface  | `Payment`                                              |
| Concrete Strategies | `CreditCardPayment`, `PayPalPayment`, `BitcoinPayment` |
| Context             | `ProcessPayment`                                       |
| Client              | `App`                                                  |



