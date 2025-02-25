
### **Access Modifiers in Java: `public`, `private`, and `protected`**

Access modifiers in Java **control the visibility** of classes, methods, and variables. The three primary access modifiers are:

1. **`public`** – Accessible from **anywhere** in the program.
2. **`private`** – Accessible **only within the same class**.
3. **`protected`** – Accessible **within the same package** and by **subclasses** (even in different packages).

---

### **1. `public` Access Modifier**

- A **public** class, method, or variable can be accessed **from anywhere**.
- It allows global visibility.

#### **Example:**

```java
public class PublicExample {
    public int num = 100;

    public void display() {
        System.out.println("Public Method: " + num);
    }
}

class Test {
    public static void main(String[] args) {
        PublicExample obj = new PublicExample();
        obj.display();  // ✅ Accessible
        System.out.println(obj.num);  // ✅ Accessible
    }
}
```

**Output:**

```
Public Method: 100
100
```

**Where it is Accessible:**  
✅ Same Class  
✅ Same Package  
✅ Subclass (Different Package)  
✅ Different Package

---

### **2. `private` Access Modifier**

- A **private** variable or method is accessible **only within the same class**.
- It **cannot** be accessed outside the class, not even by subclasses.

#### **Example:**

```java
class PrivateExample {
    private int num = 50;

    private void display() {
        System.out.println("Private Method: " + num);
    }

    public void show() {
        display(); // ✅ Accessible inside the class
    }
}

class Test {
    public static void main(String[] args) {
        PrivateExample obj = new PrivateExample();
        // obj.display();  // ❌ ERROR: Private method not accessible
        // System.out.println(obj.num);  // ❌ ERROR: Private variable not accessible
        obj.show(); // ✅ Can access indirectly via a public method
    }
}
```

**Output:**

```
Private Method: 50
```

**Where it is Accessible:**  
✅ Same Class  
❌ Same Package  
❌ Subclass (Different Package)  
❌ Different Package

**Why Use `private`?**

- It helps in **data hiding**.
- It prevents **direct modification** of critical data.

---

### **3. `protected` Access Modifier**

- A **protected** member is accessible:
    - ✅ **Within the same package**.
    - ✅ **In subclasses, even if they are in different packages**.
    - ❌ **Not accessible in a non-subclass outside the package**.

#### **Example:**

```java
class ProtectedExample {
    protected int num = 200;

    protected void display() {
        System.out.println("Protected Method: " + num);
    }
}

class Subclass extends ProtectedExample {
    public void show() {
        display();  // ✅ Accessible in subclass
    }
}

class Test {
    public static void main(String[] args) {
        Subclass obj = new Subclass();
        obj.show();  // ✅ Accessible via subclass method

        ProtectedExample obj2 = new ProtectedExample();
        // obj2.display();  // ❌ ERROR: Protected method not accessible outside package
    }
}
```

**Output:**

```
Protected Method: 200
```

**Where it is Accessible:**  
✅ Same Class  
✅ Same Package  
✅ Subclass (Different Package)  
❌ Different Package (if not a subclass)

---

### **Summary of Access Modifiers**

|Modifier|**Same Class**|**Same Package**|**Subclass (Different Package)**|**Other Classes (Different Package)**|
|---|---|---|---|---|
|`public`|✅ Yes|✅ Yes|✅ Yes|✅ Yes|
|`private`|✅ Yes|❌ No|❌ No|❌ No|
|`protected`|✅ Yes|✅ Yes|✅ Yes|❌ No|

---

### **When to Use Which Modifier?**

- ✅ **Use `public`** for methods and variables that **need global access**.
- ✅ **Use `private`** for **encapsulation** (hiding sensitive data).
- ✅ **Use `protected`** when you want **subclasses to inherit a method/variable** but keep it hidden from non-subclasses.

Would you like an example demonstrating all access modifiers in a single program?