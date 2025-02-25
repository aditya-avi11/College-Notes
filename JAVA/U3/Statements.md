
In JDBC, **Statement**, **PreparedStatement**, and **CallableStatement** are interfaces used to execute SQL queries. Each serves a different purpose and provides varying levels of security, performance, and flexibility.

---

## **1️⃣ Statement**

- **Used for executing simple SQL queries (without parameters).**
- **Vulnerable to SQL Injection** if user input is concatenated directly.
- **Query is compiled every time** it runs, making it slower than `PreparedStatement`.

### **Syntax & Example:**

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM users";
ResultSet rs = stmt.executeQuery(sql);
```

📌 **Best for:** Running **static queries** where input does not change dynamically.

---

## **2️⃣ PreparedStatement** (✅ **Recommended for Queries with Parameters**)

- **Used for executing parameterized SQL queries**.
- **Precompiled for better performance** (faster than `Statement` for repeated execution).
- **Prevents SQL Injection** by using `?` placeholders.

### **Syntax & Example:**

```java
String sql = "SELECT * FROM users WHERE age > ?";
PreparedStatement pstmt = conn.prepareStatement(sql);
pstmt.setInt(1, 25);
ResultSet rs = pstmt.executeQuery();
```

📌 **Best for:** Queries that require **input parameters**, **executed multiple times**, or need **SQL Injection protection**.

---

### **What does `pstmt.setInt(1, 25);` do in JDBC?**

This line of code is used in **`PreparedStatement`** to set the value of a parameter (`?`) in a SQL query.

### **Breaking it Down:**

```java
String sql = "SELECT * FROM users WHERE age > ?";
PreparedStatement pstmt = conn.prepareStatement(sql);
pstmt.setInt(1, 25);
ResultSet rs = pstmt.executeQuery();
```

#### **Explanation:**

1. **`?` is a placeholder** in the SQL query (`"SELECT * FROM users WHERE age > ?"`).
2. **`pstmt.setInt(1, 25);` replaces the first `?`** with `25`.
    - `1` → Refers to the **first parameter position** (JDBC parameters are **1-based**).
    - `25` → The **integer value** being assigned to the placeholder.
3. The query executed becomes:
    
    ```sql
    SELECT * FROM users WHERE age > 25;
    ```
    

### **Why Use `PreparedStatement` Instead of String Concatenation?**

❌ **Bad Approach (Using `Statement`)** - **Vulnerable to SQL Injection**

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM users WHERE age > " + userInput;
ResultSet rs = stmt.executeQuery(sql);
```

- If `userInput = "25 OR 1=1"`, it becomes:
    
    ```sql
    SELECT * FROM users WHERE age > 25 OR 1=1;
    ```
    
- This returns **all rows** instead of filtering by age. **SQL Injection Attack!** 🚨

✅ **Good Approach (Using `PreparedStatement`)**

```java
String sql = "SELECT * FROM users WHERE age > ?";
PreparedStatement pstmt = conn.prepareStatement(sql);
pstmt.setInt(1, userInput);
ResultSet rs = pstmt.executeQuery();
```

- The database treats `?` as **data, not code**, making it **secure**.

### **Conclusion**

- `pstmt.setInt(1, 25);` ensures safe **dynamic query execution**.
- **Prevents SQL injection attacks**.
- **Improves performance** for repeated executions. 🚀

Would you like more examples on using **different data types (String, Date, etc.)** in `PreparedStatement`?


<hr><hr>

## **3️⃣ CallableStatement** (✅ **For Stored Procedures**)

- **Used to call stored procedures in the database**.
- **Can handle both input and output parameters**.
- Useful for **complex business logic** at the database level.

### **Syntax & Example:**

```java
CallableStatement cstmt = conn.prepareCall("{call getUserById(?)}");
cstmt.setInt(1, 101);
ResultSet rs = cstmt.executeQuery();
```

📌 **Best for:** **Stored Procedures** that return **complex results or perform transactions**.

---

## **🔍 Comparison Table**

|Feature|`Statement`|`PreparedStatement`|`CallableStatement`|
|---|---|---|---|
|**Query Type**|Static|Parameterized|Stored Procedures|
|**Performance**|Slower (compiles every time)|Faster (precompiled)|Best for complex logic|
|**SQL Injection Protection**|❌ No|✅ Yes|✅ Yes|
|**Use Case**|Simple queries|Repeated queries with params|Stored Procedures|


### **What does `pstmt.setInt(1, 25);` do in JDBC?**

This line of code is used in **`PreparedStatement`** to set the value of a parameter (`?`) in a SQL query.

### **Breaking it Down:**

```java
String sql = "SELECT * FROM users WHERE age > ?";
PreparedStatement pstmt = conn.prepareStatement(sql);
pstmt.setInt(1, 25);
ResultSet rs = pstmt.executeQuery();
```

#### **Explanation:**

1. **`?` is a placeholder** in the SQL query (`"SELECT * FROM users WHERE age > ?"`).
2. **`pstmt.setInt(1, 25);` replaces the first `?`** with `25`.
    - `1` → Refers to the **first parameter position** (JDBC parameters are **1-based**).
    - `25` → The **integer value** being assigned to the placeholder.
3. The query executed becomes:
    
    ```sql
    SELECT * FROM users WHERE age > 25;
    ```
    

### **Why Use `PreparedStatement` Instead of String Concatenation?**

❌ **Bad Approach (Using `Statement`)** - **Vulnerable to SQL Injection**

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM users WHERE age > " + userInput;
ResultSet rs = stmt.executeQuery(sql);
```

- If `userInput = "25 OR 1=1"`, it becomes:
    
    ```sql
    SELECT * FROM users WHERE age > 25 OR 1=1;
    ```
    
- This returns **all rows** instead of filtering by age. **SQL Injection Attack!** 🚨

✅ **Good Approach (Using `PreparedStatement`)**

```java
String sql = "SELECT * FROM users WHERE age > ?";
PreparedStatement pstmt = conn.prepareStatement(sql);
pstmt.setInt(1, userInput);
ResultSet rs = pstmt.executeQuery();
```

- The database treats `?` as **data, not code**, making it **secure**.

### **Conclusion**

- `pstmt.setInt(1, 25);` ensures safe **dynamic query execution**.
- **Prevents SQL injection attacks**.
- **Improves performance** for repeated executions. 🚀

---

### **🚀 Key Takeaways**

✔ **Use `Statement`** **only for static queries.**  
✔ **Use `PreparedStatement`** **for queries with dynamic parameters** (✅ Best Practice).  
✔ **Use `CallableStatement`** **for stored procedures** to optimize performance in large applications.

Would you like an example of using a **stored procedure with CallableStatement**? 🚀


