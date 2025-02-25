
### **Taking Input in Java Using Different Classes**

Java provides multiple ways to take user input. Below are three common methods:

---

## **1. Using `Scanner` Class**

`Scanner` is part of `java.util` and is the most commonly used way to take input from the console.

### **Example:**

```java
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Enter your name: ");
        String name = sc.nextLine(); // Read a full line
        
        System.out.print("Enter your age: ");
        int age = sc.nextInt(); // Read an integer
        
        System.out.println("Name: " + name + ", Age: " + age);
        
        sc.close(); // Close scanner to prevent memory leaks
    }
}
```

### **Pros:**

✔ Easy to use  
✔ Supports different data types (`nextInt()`, `nextDouble()`, `nextBoolean()`, etc.)  
✔ Supports input tokenization

### **Cons:**

❌ Uses more memory compared to `BufferedReader`  
❌ Slower compared to `BufferedReader` for large inputs

---

## **2. Using `BufferedReader` Class**

`BufferedReader` is part of `java.io` and is used for reading input efficiently as a whole. It reads input as a `String` and requires manual conversion to other types.

### **Example:**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class BufferedReaderExample {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        System.out.print("Enter your name: ");
        String name = br.readLine(); // Reads a full line
        
        System.out.print("Enter your age: ");
        int age = Integer.parseInt(br.readLine()); // Converts string to integer
        
        System.out.println("Name: " + name + ", Age: " + age);
    }
}
```

### **Pros:**

✔ Faster than `Scanner` (uses buffering, reducing the number of I/O operations)  
✔ Useful for reading large amounts of data

### **Cons:**

❌ More complex (requires `try-catch` for exception handling)  
❌ Only reads `String` data, requiring manual conversion for numeric types

---

## **3. Using `BufferedReader + InputStreamReader`**

This is a combination where `InputStreamReader` converts byte input to characters, and `BufferedReader` reads data efficiently.

### **Example:**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class BufferedReaderInputStreamReaderExample {
    public static void main(String[] args) throws IOException {
        InputStreamReader isr = new InputStreamReader(System.in);
        BufferedReader br = new BufferedReader(isr);

        System.out.print("Enter your city: ");
        String city = br.readLine(); // Reads a full line

        System.out.println("City: " + city);
    }
}
```

This method is useful when you want more control over input handling.

---

## **Differences Between Scanner, BufferedReader, and BufferedReader + InputStreamReader**

|Feature|**Scanner**|**BufferedReader**|**BufferedReader + InputStreamReader**|
|---|---|---|---|
|**Package**|`java.util`|`java.io`|`java.io`|
|**Speed**|Slower|Faster|Fast|
|**Input Type**|Reads primitive types directly|Reads strings|Reads strings|
|**Exception Handling**|No `IOException` required|Requires `IOException` handling|Requires `IOException` handling|
|**Memory Usage**|More memory|Less memory|Less memory|
|**Used For**|Small programs, user inputs|Large data, file reading|Large data, file reading|
|**Additional Features**|Can tokenize input|Cannot tokenize input|Cannot tokenize input|

---

### **When to Use Which?**

✅ Use **Scanner** for user-friendly input handling when working with different data types.  
✅ Use **BufferedReader** for reading large amounts of data efficiently.  
✅ Use **BufferedReader + InputStreamReader** when handling different input streams (e.g., files, sockets).

Would you like an example of reading from a file using these methods?