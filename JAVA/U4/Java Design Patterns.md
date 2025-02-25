
- Design Patterns are guidlines for solving recurring problems in Java.
- Helps us to solve a programming problem during project development.
- It helps us in fixing performance & memory related issues.


## Singleton Design Pattern

It allows creation of only one object of a class.

List of scenarios where singleton design patterns are used : 
- Config Management
- Logging
- Database Connection
- Printer Spooler
- Resource Management
- Device Mgmt
- Authentication Mgmet
- Service Locator
- Security Mgmt

Steps for writing a Singleton DP :
- Privatre Constructor
- Static Instance Variable
- Public Static Method
- Thread Safety

Example :
```Java

class SimpleSingleton {
private static SimpleSingleton instance;
private SimpleSingleton() {
	System.out.println("SInleton instance created.");
}

public static SimpleSingleton getInstance() {
	if (instance == null) {
		instance = new SimpleSingleton();
		return instance;
	}
}
public void showMessage() {
	System.out.println("Hello form Singleton");
}

public class SingletonEx {

	public static void main(String[] args) {
		SimpleSingleton singleton = SimpleSingleton.getInstance();
        singleton.showMessage();
        SimpleSingleton anotherInstance = SimpleSingleton.getInstance();=
        System.out.println(singleton == anotherInstance);
	}

}
```


## Factory Pattern DP

Steps to create : 
- Defien a common Interface or Abstract Class
- Ctreate Concrete Classes
- Create the factory c;ass
- Write Client Code to Ise the Factory

#### Example with JavaBean  :

```java

interface Shape {
    void draw();
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Circle.");
    }
}

class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Rectangle.");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Square.");    
    }
}

class ShapeFactory {
    public static Shape getShape(String shapeType)
    {
        if(shapeType==null)
        {
            return null;
        }
        if(shapeType.equalsIgnoreCase("CIRCLE"))
        {
            return new Circle();
        }
        else if(shapeType.equalsIgnoreCase("RECTANGLE"))
        {
            return new Rectangle();
        }
        else if(shapeType.equalsIgnoreCase("SQUARE"))
        {
            return new Square();
        }
        return null;
    }
}

public class FactoryPatternDemo {
    public static void main(String[] args) {
        Shape circle = ShapeFactory.getShape("CIRCLE");
        Shape rectangle = ShapeFactory.getShape("RECTANGLE");
        Shape square = ShapeFactory.getShape("SQUARE");

        circle.draw();
        rectangle.draw();
        square.draw();
    }
}

```

## Fcatory Pattern using Java Bean : 

```Java

// Factory Pattern using Bean
class Person {
    private String name;
    private int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    Person() {
    }

    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person {name = '" + name + ", age = " + age + "}";
    }
}

class PersonFactory {
    static Person createPerson() {
        return new Person();
    }
    static Person creatPerson(String name, int age) {
        return new Person(name, age);
    }
}

public class FactoryPatternUsingBean {
    public static void main(String[] args) {
        Person defaultPerson = PersonFactory.createPerson();
        defaultPerson.setName("Avi");
        defaultPerson.setAge(22);
        System.out.println("Default Person : " + defaultPerson);
        Person customPerson = PersonFactory.creatPerson("Ken", 19);
        System.out.println("Custom Person : " + customPerson);
    }  
}
```

## Decorator Design Pattern : 

Class explosion refers to a situation where the number of classes in a system grows unctontrollably, making the codebase harder to understand, maintain, and extend.
This problem iften arises when we are adding new functionalities using inheritance rather than composition.

The Decorator Design Pattern is an effective solution to prevent class explosion, as it allows you to dynamically add fucntionality to objects without creating a large number of subclasses.

#### Steps : 

- Component : The interface or abstract class that defines main object.
- ConcreteComponent : The main object whose behavior will be extended.
- Decorator : An abstract class that implements the component interface has a reference to a component object.
- ConcreteDecorator : Extend the decorator class to add additional data.

1. Create base insterface or abstract class & define basic functionality.
2. Implement base interface or abstract class with concrete classes.
3. Define abstract decorator class that implements the same interfaceas the core component.
4. Extend the abstract decorator to implement additional features.
5. In the client code, use decorators to dynamically add features to the core component at runtime.

CODE : 

```JAVA

// Base interface for pizza

interface Pizza {

    String getDescription();

    double getCost();

}

  

// Concrete Component

class PlainPizza implements Pizza {

    @Override

    public String getDescription() {

        return "Plain Pizza";

    }

  

    @Override

    public double getCost() {

        return 5.00;

    }

}

  

//Abstract decorator

abstract class PizzaDecorator implements Pizza {

    protected Pizza pizza;

  

    public PizzaDecorator(Pizza pizza) {

        this.pizza = pizza;

    }

  

    @Override

    public String getDescription() {

        return pizza.getDescription();

    }

  

    @Override

    public double getCost() {

        return pizza.getCost();

    }

}

  

// Concrete Decorator : Cheese

class Cheese extends PizzaDecorator {

    public Cheese(Pizza pizza) {

        super(pizza);

    }

  

    @Override

    public String getDescription() {

        return super.getDescription() + " Cheese";

    }

  

    @Override

    public double getCost() {

        return super.getCost() + 1.50;

    }

}

  

// Concrete Decorator : Olives

class Olives extends PizzaDecorator {

    public Olives(Pizza pizza) {

        super(pizza);

    }

  

    @Override

    public String getDescription() {

        return super.getDescription() + " Olives";

    }

  

    @Override

    public double getCost() {

        return super.getCost() + 0.75;

    }

}

  

// Concrete Decorator : Mushroom

class Mushroom extends PizzaDecorator {

    public Mushroom(Pizza pizza) {

        super(pizza);

    }

  

    @Override

    public String getDescription() {

        return super.getDescription() + " Mushroom";

    }

  

    @Override

    public double getCost() {

        return super.getCost() + 1.25;

    }

}

  

public class DecoratorDPEx {

    public static void main(String[] args) {

        // Create a plain pizza

        Pizza plainPizza = new PlainPizza();

        System.out.println(plainPizza.getDescription() + " -> Rs. " + plainPizza.getCost());

  

        // Add cheese to the pizza

        Pizza cheesePizza = new Cheese(plainPizza);

        System.out.println(cheesePizza.getDescription() + " -> Rs. " + cheesePizza.getCost());

  

        // Asdd olives and mushroom on top of the cheese

        Pizza deluxPizza = new Mushroom(new Olives(new Cheese(plainPizza)));

        System.out.println(deluxPizza.getDescription() + " -> Rs. " + deluxPizza.getCost());

    }

}

```


## Strategy Pattern : 

Creating Strategy Pattern : 

- Context : The class that uses a strategy.
- Strategy Interface : Defines a family of algorithms (or behaviors).
- Concrete Strategies : Implementations of the Strategy Interface, each representing a specific algorithm.
- Client : The class that chooses a strategy to use.

CODE : 

```JAVA

//Strategy Interface

interface PaymentStrategy {
    void pay(double amount);
}

// Concrete Strategy :  Credit Card Payment
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;
    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using Credit Card : " + cardNumber);
    }
}

// Concrete Strategy : PayPal Payment
class PaypalPayment implements PaymentStrategy
{
    private String email;
    public PaypalPayment(String email)
    {
        this.email=email;
    }
    @Override
    public void pay(double amount)
    {
     System.out.println("\nPaid "+amount+" using paypal: "+email);
    }
}

class BankTransferPayment implements PaymentStrategy
{
    private String bankAccount;
    public BankTransferPayment(String bankAccount)
    {
        this.bankAccount=bankAccount;
    }
    @Override
    public void pay(double amount)
    {
     System.out.println("\nPaid "+amount+" using bank transfer: "+bankAccount);
    }
}

public class StrategyPatternEx {
    public static void main(String args[])
    {
       PaymentStrategy paycredit=new CreditCardPayment("1234-562-222-123");
       PaymentStrategy paypal=new PaypalPayment("avi@gmail.com");
       PaymentStrategy bankpay=new BankTransferPayment("SBI1245");
       paycredit.pay(1999);
       paypal.pay(20000);
       bankpay.pay(4500);  
    }
}
```