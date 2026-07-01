
# Builder Pattern in Java

## What is Builder?

The **Builder Pattern** is a creational design pattern used to create objects **step by step**.

It is mainly used when:
- A class has many fields.
- Some fields are optional.
- Constructors become too long and confusing.

---

# Problem Without Builder

Suppose we have a `Student` class.

```java
class Student {
    String name;
    int age;
    String city;
    String college;
    String phone;

    Student(String name, int age, String city, String college, String phone) {
        this.name = name;
        this.age = age;
        this.city = city;
        this.college = college;
        this.phone = phone;
    }
}
```

Creating an object:

```java
Student s = new Student(
    "Mohit",
    22,
    "Delhi",
    "ABC College",
    "9876543210"
);
```

### Problems

- Constructor becomes very long.
- Hard to remember parameter order.
- Easy to pass wrong values.
- Optional fields must also be passed.

---

# Solution: Builder Pattern

Instead of passing everything to the constructor, we build the object step by step.

```java
Student s = new Student.Builder()
        .setName("Mohit")
        .setAge(22)
        .setCity("Delhi")
        .setCollege("ABC College")
        .setPhone("9876543210")
        .build();
```

Much easier to read.

---

# How Builder Works

```
Builder Object
      │
      ▼
Set values one by one
      │
      ▼
build()
      │
      ▼
Final Student Object
```

---

# Simple Implementation

## Student Class

```java
class Student {

    private String name;
    private int age;
    private String city;

    private Student(Builder builder) {
        this.name = builder.name;
        this.age = builder.age;
        this.city = builder.city;
    }

    static class Builder {

        private String name;
        private int age;
        private String city;

        Builder setName(String name) {
            this.name = name;
            return this;
        }

        Builder setAge(int age) {
            this.age = age;
            return this;
        }

        Builder setCity(String city) {
            this.city = city;
            return this;
        }

        Student build() {
            return new Student(this);
        }
    }
}
```

---

# Creating Object

```java
Student student = new Student.Builder()
        .setName("Mohit")
        .setAge(22)
        .setCity("Delhi")
        .build();
```

---

# Why `return this`?

Example:

```java
Builder setName(String name) {
    this.name = name;
    return this;
}
```

`return this` returns the current Builder object.

Because of this, we can chain methods.

```java
new Builder()
    .setName("Mohit")
    .setAge(22)
    .setCity("Delhi");
```

Without `return this`, chaining is not possible.

---

# What does `build()` do?

```java
Student build() {
    return new Student(this);
}
```

`build()` creates the final object using all the values stored in the Builder.

Example:

```
Builder
-------
name = Mohit
age = 22
city = Delhi

↓

build()

↓

Student Object
```

---

# Why Constructor is Private?

```java
private Student(Builder builder)
```

The private constructor prevents users from creating objects directly.

Wrong:

```java
Student s = new Student();
```

Correct:

```java
Student s = new Student.Builder()
        .setName("Mohit")
        .build();
```

This forces everyone to use the Builder.

---

# Real-Life Example

Imagine ordering a pizza.

You choose:

- Size
- Cheese
- Toppings
- Extra Sauce
- Mushrooms

After selecting everything, the chef prepares the pizza.

Builder works the same way.

```
Choose options
      │
      ▼
Builder stores them
      │
      ▼
build()
      │
      ▼
Ready Object
```

---

# Advantages

- Easy to read.
- Supports method chaining.
- Handles optional parameters.
- Avoids long constructors.
- Less chance of passing wrong arguments.
- Makes objects easier to create.

---

# Disadvantages

- More code.
- Requires an extra Builder class.
- Slightly more complex for very small classes.

---

# Constructor vs Builder

| Constructor | Builder |
|-------------|----------|
| Parameters passed together | Values set one by one |
| Hard to read | Easy to read |
| Order matters | Order doesn't matter |
| Not good for many parameters | Best for many parameters |
| No method chaining | Supports method chaining |

---

# Interview Questions

### 1. What is Builder Pattern?

A design pattern used to create complex objects step by step.

---

### 2. Why use Builder?

To avoid long constructors and improve readability.

---

### 3. Why does every setter return `this`?

To enable method chaining.

---

### 4. What does `build()` do?

It creates and returns the final object.

---

### 5. Why is the constructor private?

To force object creation through the Builder.

---

### 6. When should Builder Pattern be used?

- Many constructor parameters
- Optional fields
- Immutable objects
- Better readable object creation

---

# Flow Diagram

```
new Builder()
      │
      ▼
setName()
      │
      ▼
setAge()
      │
      ▼
setCity()
      │
      ▼
build()
      │
      ▼
Student Object
```

---

# Key Points to Remember

- Builder creates objects step by step.
- `return this` enables method chaining.
- `build()` returns the final object.
- Constructor is usually private.
- Best for classes with many optional fields.
- Improves readability and maintainability.
