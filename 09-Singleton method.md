# Singleton Class

A Singleton class ensures that only one object (instance) of a class is created throughout the lifetime of an application, and it provides a global point of access to that instance.

A Singleton class generally has:
1. **Private constructor** – prevents object creation using `new`
2. **Private static instance variable** – stores the single instance
3. **Public static method** – returns the instance

```java
public class SimpleSingleton {
    private static SimpleSingleton instance = null;

    private SimpleSingleton() {
        System.out.println("Singleton Constructor called");
    }

    public static SimpleSingleton getInstance() {
        if (instance == null) {
            instance = new SimpleSingleton();
        }
        return instance;
    }
}
⚠️ Problem: This version is NOT thread-safe.
```
# Thread safe

```java
public class ThreadSafeDoubleLockingSingleton {
    private static ThreadSafeDoubleLockingSingleton instance = null;

    private ThreadSafeDoubleLockingSingleton() {
        System.out.println("Singleton Constructor Called!");
    }

    // Double check locking..
    public static ThreadSafeDoubleLockingSingleton getInstance() {
        if (instance == null) { // First check (no locking)
            synchronized (ThreadSafeDoubleLockingSingleton.class) { // Lock only if needed
                if (instance == null) { // Second check (after acquiring lock)
                    instance = new ThreadSafeDoubleLockingSingleton();
                }
            }
        }
        return instance;
    }

    public static void main(String[] args) {
        ThreadSafeDoubleLockingSingleton s1 = ThreadSafeDoubleLockingSingleton.getInstance();
        ThreadSafeDoubleLockingSingleton s2 = ThreadSafeDoubleLockingSingleton.getInstance();

        System.out.println(s1 == s2);
    }
}
```

# What Is Eager Initialization?
- Instance is created at class loading time.
- JVM guarantees thread safety during class loading.
- Simple and safe.

```java
public class ThreadSafeEagerSingleton {
    private static ThreadSafeEagerSingleton instance = new ThreadSafeEagerSingleton();

    private ThreadSafeEagerSingleton() {
        System.out.println("Singleton Constructor Called!");
    }

    public static ThreadSafeEagerSingleton getInstance() {
        return instance;
    }

    public static void main(String[] args) {
        ThreadSafeEagerSingleton s1 = ThreadSafeEagerSingleton.getInstance();
        ThreadSafeEagerSingleton s2 = ThreadSafeEagerSingleton.getInstance();

        System.out.println(s1 == s2);
    }
}
```
# When to Use Eager Singleton
- When object creation is lightweight
- When instance is always required

# Bill Pugh Singleton (Best Practice)

```java
class Singleton {
    private Singleton() {}

    private static class Helper {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return Helper.INSTANCE;
    }
}

//No synchronization overhead
//JVM handles it efficiently
```

Note : All nested types of a top-level class can access each other’s private members.

| Approach       | Thread-Safe   | Lazy | Performance |
| -------------- | ------------- | ---- | ----------- |
| Lazy (basic)   | ❌           | ✅    | Fast       |
| Synchronized   | ✅           | ✅    | Slow       |
| Double-checked | ✅           | ✅    | Fast       |
| Eager          | ✅           | ❌    | Fast       |
| Bill Pugh      | ✅           | ✅    | Very Fast  |
| Enum           | ✅           | ❌    | Fast       |



