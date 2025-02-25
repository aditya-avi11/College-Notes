
Syntax : 

```java
Permission static(op) Return_type functionName(parameter list) throws Exception_Type {
	statements;
	return;
}
```

## Access Methods : 

1. Public : Can be accessed from any other class.
2. Private : Can be accessed from the same clas.
3. Protected : Can be accessed by any sub-class within the same package.
4. Default : When no access modifier is specified for a class, method, or data member – It is said to be having the ****default**** access modifier by default. The data members, classes, or methods that are not declared using any access modifiers i.e. having default access modifiers are accessible ***only within the same package**.


# Method Overloading

- Happens at Compile Time (also called compile time polymorphism).
- Many functions with same name but different number of parameters.


## Constructors : 

### this keyword :

- can be used to invoke the constructors, methods, static members, etc, of the current instance of class.
```JAVA
class Code {
	int value;
	coid assign(int var){
		this.value = var;
	}
}
```


### Getter Methods  :
Syntax :

```JAVA
public <return_tyoe> get<field_name>() {
	return this.<field_name>
}
```

- Instance variables are typically declared as private to enforce encapsulation, getter methods provide a way to read their values outside the class.

Although we can simply print the value of a private variables without this keyword, to return its value we have to use this keyword.


## Static Block :

The static block is executed only once when the class is loaded into memory.
This is useful for initializing static variables or performing ....

## Instance Block :

Executed everytime when an instance of a class is created.

## Suppose we create 2 objects, the execution flow will be : 

1. Static block
2. 2. Main Method
3. Instance Block
4. Constructor
5. Instance Block
6. Constructor
7. Main Method End
Refer Blocks.java at D:PESU/SEM3/JEAD/Blocks.java

	