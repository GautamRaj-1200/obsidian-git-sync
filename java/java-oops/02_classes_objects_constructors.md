## Class
- A class is a collection of Objects.
- It is not a real world entity. It is just a template or blueprint or prototype for creating Objects.
- It does not occupy memory.
- A class can include :
	- fields and variables
	- methods
	- constructors
	- blocks
	- nested class
- Syntax:
```java
access-modifier class ClassName{}  
```
- By default the access modifier is default.
## Object
- An object is an instance of a class.
- It is a real world entity.
- It occupies memory.
- It consists of
	- Identity (name)
	- State/Attribute : properties/variables
	- Behaviors : methods
- All the objects share the attributes and behavior of the class.
- Syntax for creating an object
	1. Using `new`
	2. Using `newInstance`
	3. Using ` clone`
	4. Using `deserialization`
	5. Using  `factory` methods
- Using `new` keyword
	1. Declaration
		- Declaring a variable with an Object type
		- It does not create an object.
			- `Vehicle car;`
	2. Instantiation
		- This is when memory is allocated for an Object.
		- The `new` keyword is used to create an object.
		- A reference to the Object that was created is returned from the new keyword
			- `car = new`
	3. Initialization
		 - The `new` keyword is followed by a call to a constructor. This call initializes the Object.
		 - In this, the values are put in the memory that was allocated.
			 - `Car = new Vechicle()`
	- In Two Lines
  
```java
 Vehicle car 
 car = new Vehicle()
```

  - In Single
  
```java
 Vehicle car = new Vehicle()
```
- We can call the methods and attributes using the object using dot operator.
	- `car.noOfWheels`
	- `car.drive()`

### Initialization of an Object
1. ***By Reference Variable***

```java
package oops;  

class Car{  
  
	// attributes  
	String typeOfCar;  
	String model;  
	int year;  
	String color;  
  
	// methods  
	int calculateAge(int y){  
		return (2024-y);  
	}  
}  
  
public class VehicleMain {  
	public static void main(String[] args) {  
		Car c1 = new Car();
		// Initialization using reference variable
		c1.typeOfCar="Jeep";  
		c1.model = "Thar";  
		c1.year = 2008;  
		c1.color = "Black";  
  
		System.out.println("-----Car Information-----");  
		System.out.println("Type: "+c1.typeOfCar+","+"Model: "+c1.model+","+"Year: "+c1.year+","+"Color: "+c1.color);  
		// Calling methods using object
		System.out.println("Age of the car: "+c1.calculateAge(c1.year));  
	}  
}
```
	 
   - This method is not so good. For ex. Let's say we have to create 5 objects. Then we have to repeat the initialization 5 times. So we can create a method for this.
	
2. ***By Methods***

``` java
package oops;  
  
class Car{  
  
    // attributes  
    String typeOfCar;  
    String model;  
    int year;  
    String color;  
  
    // methods  
    void initializeObject(String t,String m, int y, String c){  
        typeOfCar = t;  
        model = m;  
        year = y;  
        color = c;  
    }  
    void display(){  
        System.out.println("-----Car Information-----");  
        System.out.println("Type: "+typeOfCar+","+"Model: "+model+","+"Year: "+year+","+"Color: "+color);  
    }  
    int calculateAge(int y){  
        return (2024-y);  
    }  
}  
  
public class VehicleMain {  
    public static void main(String[] args) {  
        Car c1 = new Car();  
        // initialization using method  
        c1.initializeObject("Jeep","Thar",2008,"Black");  
        // calling display method  
        c1.display();  
        System.out.println("Age of the car: "+c1.calculateAge(c1.year));  
    }  
}
```

3. ***By Constructors***
	- It is a block similar to method having same name as that of a class name.
	- It does not have any return type, not even void.
	- It is used to initialize an object, not to create an object.
	- The only modifiers applicable for constructors: *public*,*private*,*default*,*protected*. 
	- *static*, *final*, and *synchronized* cannot be used with contructors.
	- It executes automatically when we create an object.
	- Two ways to call constructor
		- `Test t = new Test()`
		- `new Test()` (No need to create reference variable)
	- Need for constructors
		- Without Constructor, when we create objects, default values are assigned which might become problematic.
		 ```java
			 package oops;  
  
			class Student{  
			  
			    // attributes  
			    String name;  
			    int admNo;  
			  
			    void display(){  
			        System.out.println("Name: "+name+","+"Admission No: "+admNo);  
			    }  
			}  
			  
			public class VehicleMain {  
			    public static void main(String[] args) {  
			        Student s1 = new Student();  
			        Student s2 = new Student();  
			        s1.display();  
			        s2.display();  
			    }  
			}
        ```
        - Output
	     ```
		     Name: null,Admission No: 0
			 Name: null,Admission No: 0
		 ```
		 
		- As we can see Admission Number is initialized as 0. Two students having same Admission Number is not what we want.
		- Initially, we used reference variables to set the values of an object's attributes. However, this approach becomes cumbersome and repetitive when dealing with multiple objects, as it requires writing the same code repeatedly for each object.
		- The next approach involved using methods to initialize object attributes. While this reduces repetition, it still requires explicitly calling the method for each object, adding to the manual effort.
		- Constructors offer a more efficient solution. Unlike methods, constructors automatically initialize the object's attributes at the time of creation, eliminating the need for explicit method calls and streamlining the object creation process.

		  ```java
			package oops;

			class Student{

				// attributes
				String name;
				int admNo;

				// constructor
				Student(String n, int a){
					name = n;
					admNo = a;
				}
				void display(){
					System.out.println("Name: "+name+","+"Admission No: "+admNo);
				}
			}

			public class VehicleMain {
				public static void main(String[] args) {
					Student s1 = new Student("Shubham",1001);
					Student s2 = new Student("Shubham",1002);
					s1.display();
					s2.display();
				}
			}
		  ```
  
        - We can create the above program in a different way. Like this:
		  
		  ```java
		    package oops;

			class Student{

				// attributes
				String name;
				int admNo;

				// constructor
				Student(String name, int admNo){
					this.name = name;
					this.admNo = admNo;
				}
				void display(){
					System.out.println("Name: "+this.name+","+"Admission No: "+this.admNo);
				}
			}

			public class VehicleMain {
				public static void main(String[] args) {
					Student s1 = new Student("Shubham",1001);
					Student s2 = new Student("Shubham",1002);
					s1.display();
					s2.display();
				}
			}
		  ```
  
        - ***In the first approach***
          - **Constructor Parameters**: The parameters n and a are used to pass the values to the instance variables name and admNo.
          - **Assignment**: Inside the constructor, the instance variables name and admNo are directly assigned the values of n and a.
          - **Display Method**: The display method directly accesses the instance variables name and admNo.
        - ***In the second approach***
          - **Constructor Parameters**: The constructor uses name and admNo as parameter names, which are the same as the instance variable names.
          - **Assignment with this**: The this keyword is used to distinguish between the instance variables and the constructor parameters. this.name refers to the instance variable, while name refers to the parameter.
          - **Display Method**: The display method also uses this.name and this.admNo, making it clear that the instance variables are being accessed.
       - ***Why the second approach is better?***
         - **Clarity and Readability**:
           - **Avoids Ambiguity**: By using the this keyword, the code clearly distinguishes between instance variables and parameters or local variables that have the same name. This makes the code easier to understand, especially for other developers who might work on it in the future.
           - **Consistency**: Using this consistently can improve the readability of the code. It makes it immediately apparent that a variable belongs to the instance of the class, rather than being a local variable or parameter
         - **Best Practice**:
           - **Standard Practice**: It is a common best practice in object-oriented programming to use the same names for parameters as the instance variables, relying on the this keyword to differentiate them. This reduces the cognitive load on developers, as they don’t need to invent new names for parameters and can focus on the logic of the code.
         - **Reduces Potential Bugs**:
           - **Eliminates Mistakes**: When working with larger classes or more complex code, using this reduces the likelihood of mistakenly assigning a value to the wrong variable. Without this, it's easy to inadvertently introduce bugs, especially in scenarios where the variable names are similar or identical.

## Types of Constructors

### 1. Default Constructor
- A default constructor is a constructor that is automatically provided by the Java compiler if no other constructors are defined in the class. It initializes the object with default values: null for objects and 0 for numeric types.
- Characteristics:
  - Implicitly provided if no constructors are defined
  - Has no parameters.
  - Assigns default values to the object’s attributes.

```java
package oops;

class Student{

    // attributes
    String name;
    int admNo;
    
    void display(){
        System.out.println("Name: "+this.name+","+"Admission No: "+this.admNo);
    }
}

public class VehicleMain {
    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student();
        s1.display();
        s2.display();
    }
}

```
- In the Example:
  - Since no constructor is defined in the Student class, the Java compiler provides a default constructor.
  - When Student s1 = new Student(); is called, the default constructor initializes name to null and admNo to 0.

### 2. No-Argument Constructor
- A no-argument constructor is explicitly defined by the programmer. It is similar to the default constructor, but it is written by the developer to potentially include custom initialization code.
- Characteristics:
  - Explicitly defined by the programmer.
  - Takes no parameters.
  - Can be used to initialize the object with custom default values or to perform specific actions during object creation.

```java
package oops;

class Student{

    // attributes
    String name;
    int admNo;

    // constructor
    Student(){
    }
    void display(){
        System.out.println("Name: "+this.name+","+"Admission No: "+this.admNo);
    }
}

public class VehicleMain {
    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student();
        s1.display();
        s2.display();
    }
}

```
- In the Example:
    - The Student class includes an explicitly defined no-argument constructor, Student(){}, which doesn't do anything in this case.
    - Like the default constructor, it initializes the object, but since no code is provided in the constructor, the attributes name and admNo remain null and 0, respectively.

### Parameterized Constructor
- A parameterized constructor is one that accepts arguments to initialize the object's attributes with specific values at the time of object creation.
- Characteristics:
  - Takes one or more parameters.
  - Used to initialize an object with specific values, allowing for greater control over the object’s state at the time of creation.
  - It can be overloaded to provide multiple ways to create objects with different sets of parameters.

```java
package oops;

class Student{

    // attributes
    String name;
    int admNo;

    // constructor
    Student(String name, int admNo){
        this.name = name;
        this.admNo = admNo;
    }
    void display(){
        System.out.println("Name: "+this.name+","+"Admission No: "+this.admNo);
    }
}

public class VehicleMain {
    public static void main(String[] args) {
        Student s1 = new Student("Shubham",1001);
        Student s2 = new Student("Shubham",1002);
        s1.display();
        s2.display();
    }
}

```
- In the Example:
  - The Student class includes a parameterized constructor Student(String name, int admNo).
  - When Student s1 = new Student("Shubham",1001); is called, the name and admNo attributes are initialized with the values "Shubham" and 1001, respectively.

## Is user defined no argument constructor useless?
- A no-argument (no-arg) constructor, even if it appears unnecessary at first, plays a significant role in Java programming. It allows for the creation of objects without requiring parameters, providing flexibility in how and when an object's properties are initialized. This is particularly useful in scenarios where immediate property assignment isn't possible or when working with mutable objects.

- Moreover, certain frameworks and libraries, such as Hibernate or JPA, rely on no-arg constructors to create instances via reflection. Dependency injection frameworks also utilize no-arg constructors for object creation before injecting dependencies.

- In addition, no-arg constructors are beneficial in constructor overloading, enabling different ways to initialize objects with or without default values. They are also essential in inheritance, as subclass constructors implicitly call the superclass's no-arg constructor.

- Overall, a no-arg constructor is a valuable tool for future-proofing classes and ensuring compatibility with Java features and third-party tools, making it an important consideration in class design.

### If we can set variables while calling constructor, why bother creating getters and setters in java?
There are several important reasons to use getters and setters in Java, even when you can set variables through a constructor:
1. **Encapsulation**: Getters and setters allow you to control access to class fields. By making fields private and providing public methods to access them, you can enforce encapsulation, which is a key principle of object-oriented programming.
2. **Validation**: Setters allow you to add logic to validate input before assigning values to fields. For example, you can check if a value is within an acceptable range.
3. **Flexibility**: You can change the internal implementation of a class without affecting the code that uses it. For instance, you might want to calculate a value instead of storing it directly.
4. **Read-only or write-only access**: You can provide only a getter (read-only) or only a setter (write-only) if needed.
5. **Lazy initialization**: Getters allow you to implement lazy loading of resources, initializing them only when first accessed.
6. **Thread safety**: In multi-threaded environments, getters and setters can be made thread-safe more easily than direct field access.
7. **Observable properties**: In frameworks like JavaFX, getters and setters are used to implement observable properties.
8. **Debugging and logging**: You can add logging or breakpoints in getters and setters to track when and how fields are accessed or modified.
- Example
*CODE*
```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        setName(name);
        setAge(age);
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        if (name == null || name.trim().isEmpty()) {
            throw new IllegalArgumentException("Name cannot be null or empty");
        }
        this.name = name.trim();
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age < 0 || age > 150) {
            throw new IllegalArgumentException("Age must be between 0 and 150");
        }
        this.age = age;
    }
}
public class PersonMain{
	public static void main(String[] args){
		Person p1 = new Person("Ram", 50);
	}
}
```
***EXPLANATION***
Here's what happens:
1. The constructor is called with the arguments "Ram" and 50.
2. Inside the constructor, the setters are called:
```java
public Person(String name, int age) {
    setName(name);
    setAge(age);
}
```
3. These setter calls then trigger the validation logic:
```java
public void setName(String name) {
    if (name == null || name.trim().isEmpty()) {
        throw new IllegalArgumentException("Name cannot be null or empty");
    }
    this.name = name.trim();
}

public void setAge(int age) {
    if (age < 0 || age > 150) {
        throw new IllegalArgumentException("Age must be between 0 and 150");
    }
    this.age = age;
}
```
This approach gives us several benefits:
1. **Consistent validation**: The same validation occurs whether you're creating a new object or modifying an existing one.
2. **DRY principle**: You Don't Repeat Yourself. The validation logic is in one place, not duplicated in the constructor and setters.
3. **Maintainability**: If you need to change the validation logic, you only need to change it in one place.
It's worth noting that not all classes will necessarily call setters from the constructor. Some might set fields directly for performance reasons, especially if the class is designed to be immutable.
