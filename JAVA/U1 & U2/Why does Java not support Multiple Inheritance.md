
Java **does not support multiple inheritance with classes** to **avoid ambiguity, complexity, and maintain simplicity**. Instead, Java allows **multiple inheritance using interfaces**.

---

### **1. Ambiguity Problem ("Diamond Problem")**

If Java allowed multiple inheritance, a **"Diamond Problem"** could occur.

#### **Example in C++ (which supports multiple inheritance):**

```cpp
class A {
public:
    void show() { cout << "Class A" << endl; }
};

class B : public A { };

class C : public A { };

class D : public B, public C { }; // Multiple Inheritance

int main() {
    D obj;
    obj.show();  // ERROR: Ambiguous call to show()
    return 0;
}
```

**Problem:**

- `D` inherits from both `B` and `C`, which both inherit from `A`.
- When calling `obj.show()`, **the compiler is confused** whether to call `B`'s version or `C`'s version of `show()`.

Java **avoids** this issue by **not allowing multiple inheritance with classes**.

---

### **2. Complexity in Code Maintenance**

- With multiple inheritance, managing dependencies and function overriding **becomes complicated**.
- If a method exists in multiple parent classes, **the compiler has no clear way to resolve conflicts**.
- Java **favors simplicity and clarity**, so it restricts multiple inheritance.

---

### **3. Java Uses Interfaces Instead**

Although Java **does not support multiple inheritance with classes**, it allows **multiple inheritance through interfaces**.

#### **Example:**

```java
interface A {
    void show();
}

interface B {
    void display();
}

class C implements A, B {  // Multiple inheritance using interfaces
    public void show() {
        System.out.println("Show from A");
    }

    public void display() {
        System.out.println("Display from B");
    }
}

public class MultipleInheritanceExample {
    public static void main(String[] args) {
        C obj = new C();
        obj.show();    // Output: Show from A
        obj.display(); // Output: Display from B
    }
}
```

**Why does this work?**

- Interfaces **do not have implementation**, so there is **no ambiguity** in method resolution.
- The implementing class (`C`) **must provide implementations** for all interface methods, **removing conflicts**.

---

### **Conclusion**

- **Java avoids multiple inheritance with classes** to **prevent ambiguity and complexity**.
- **Instead, Java supports multiple inheritance through interfaces**, which **eliminates conflicts**.
- This design keeps Java **simple, maintainable, and error-free**.

Would you like a practical example showing how Java resolves multiple inheritance conflicts using `default` methods in interfaces?