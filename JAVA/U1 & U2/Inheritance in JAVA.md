
Inheritance is one of the **core concepts** of Object-Oriented Programming (OOP) that allows a class (**child class**) to **acquire the properties and behaviors** of another class (**parent class**).

### **1. Why Use Inheritance?**

- **Code Reusability** – Avoids code duplication.
- **Method Overriding** – Allows modifying inherited methods.
- **Hierarchy Representation** – Represents relationships between objects.

### **2. Types of Inheritance in Java**

Java supports:

- **Single Inheritance**
- **Multi-Level Inheritance**
- **Hierarchical Inheritance**

⚠️ **Java does not support Multiple Inheritance with classes** to avoid ambiguity (but it supports it with interfaces).

---

## **1. Using the `super` Keyword in Inheritance**

The `super` keyword is used in a **child class** to:

1. **Call the parent class constructor**.
2. **Call a parent class method** (if overridden).
3. **Access a parent class field** (if hidden by a child class variable).

### **Example 1: `super` Calling Parent Constructor**

```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    Child() {
        super();  // Calls Parent() constructor (automatically done if not written)
        System.out.println("Child Constructor");
    }
}

public class SuperExample {
    public static void main(String[] args) {
        Child obj = new Child();
    }
}
```

**Output:**

```
Parent Constructor
Child Constructor
```

---

### **Example 2: `super` Calling Parent Method**

```java
class Parent {
    void display() {
        System.out.println("Parent Method");
    }
}

class Child extends Parent {
    void display() {
        super.display();  // Calls parent method
        System.out.println("Child Method");
    }
}

public class SuperMethodExample {
    public static void main(String[] args) {
        Child obj = new Child();
        obj.display();
    }
}
```

**Output:**

```
Parent Method
Child Method
```

---

### **Example 3: `super` Accessing Parent Field**

```java
class Parent {
    String name = "Parent";
}

class Child extends Parent {
    String name = "Child";

    void show() {
        System.out.println("Child Name: " + name);
        System.out.println("Parent Name: " + super.name);  // Access parent field
    }
}

public class SuperFieldExample {
    public static void main(String[] args) {
        Child obj = new Child();
        obj.show();
    }
}
```

**Output:**

```
Child Name: Child
Parent Name: Parent
```

---

## **2. Restricting Method Overriding in Child Class**

To prevent a child class from overriding a method, use the **`final`** keyword.

### **Example: Using `final` to Restrict Overriding**

```java
class Parent {
    final void show() {
        System.out.println("Final method in Parent");
    }
}

class Child extends Parent {
    // void show() {  // ❌ ERROR: Cannot override final method
    //     System.out.println("Trying to override");
    // }
}

public class FinalMethodExample {
    public static void main(String[] args) {
        Child obj = new Child();
        obj.show();
    }
}
```

**Key Points:**

- A method declared **`final`** in a parent class **cannot be overridden** in a child class.
- If a child class tries to override it, a **compilation error** occurs.

---

## **3. Multi-Level Inheritance**

In **Multi-Level Inheritance**, a class inherits from another class, which in turn inherits from another class.

### **Example: Multi-Level Inheritance**

```java
class Grandparent {
    void grandparentMethod() {
        System.out.println("Grandparent Method");
    }
}

class Parent extends Grandparent {
    void parentMethod() {
        System.out.println("Parent Method");
    }
}

class Child extends Parent {
    void childMethod() {
        System.out.println("Child Method");
    }
}

public class MultiLevelInheritance {
    public static void main(String[] args) {
        Child obj = new Child();
        obj.grandparentMethod();  // Inherited from Grandparent
        obj.parentMethod();       // Inherited from Parent
        obj.childMethod();        // Defined in Child
    }
}
```

**Output:**

```
Grandparent Method
Parent Method
Child Method
```

---

## **4. Hierarchical Inheritance**

In **Hierarchical Inheritance**, **multiple child classes** inherit from a **single parent class**.

### **Example: Hierarchical Inheritance**

```java
class Parent {
    void parentMethod() {
        System.out.println("Parent Method");
    }
}

class Child1 extends Parent {
    void child1Method() {
        System.out.println("Child1 Method");
    }
}

class Child2 extends Parent {
    void child2Method() {
        System.out.println("Child2 Method");
    }
}

public class HierarchicalInheritance {
    public static void main(String[] args) {
        Child1 obj1 = new Child1();
        obj1.parentMethod();
        obj1.child1Method();

        Child2 obj2 = new Child2();
        obj2.parentMethod();
        obj2.child2Method();
    }
}
```

**Output:**

```
Parent Method
Child1 Method
Parent Method
Child2 Method
```

**Key Points:**

- `Child1` and `Child2` inherit from `Parent`, but they **do not inherit from each other**.
- Each child class can **use the parent’s methods** but **define its own methods separately**.

---

## **Summary Table: Types of Inheritance in Java**

|Inheritance Type|Description|
|---|---|
|**Single**|One child class inherits from one parent class.|
|**Multi-Level**|A child inherits from a parent, which itself inherits from another class.|
|**Hierarchical**|Multiple child classes inherit from a single parent.|
|**Multiple**|❌ Not supported with classes, but possible using interfaces.|

---

## **Conclusion**

- Java **supports inheritance** but avoids **multiple inheritance with classes** to prevent ambiguity.
- The **`super`** keyword helps access parent class constructors, methods, and fields.
- **`final`** is used to **prevent method overriding**.
- Java provides **Multi-Level and Hierarchical Inheritance** for structuring relationships between classes.

Would you like an example where a method is overridden in **Multi-Level Inheritance** using `super`?