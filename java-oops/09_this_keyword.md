## `this` keyword
- `this` keyword is the reference variable that refers to the current object.
- this points to object : it refers to the object that is executing the current method or constructor.
- this.variable_name points to instance variable: when we use `this` followed by a dot and a variable name, we're specifically referring to an instance variable of the current object, distinguishing it from local variables or parameters that might have the same name.
### Without `this`
*CODE*
```java
public class BankAccount {
    private String accountHolder;
    private double balance;

    // Constructor without using 'this'
    public BankAccount(String accountHolder, double balance) {
        accountHolder = accountHolder; // Problematic!
        balance = balance; // Problematic!
    }

    // Method to display account info
    public void displayInfo() {
        System.out.println("Account Holder: " + accountHolder);
        System.out.println("Balance: $" + balance);
    }

    // Main method to test the class
    public static void main(String[] args) {
        BankAccount account = new BankAccount("John Doe", 1000.0);
        account.displayInfo();
    }
}
```
*OUTPUT*
```
Account Holder: null
Balance: $0.0
```
**EXPLANATION**
In this example, we have a `BankAccount` class with two instance variables: `accountHolder` and `balance`. The constructor takes parameters with the same names as the instance variables.

Without using `this`, we encounter a problem:

1. In the constructor, `accountHolder = accountHolder;` and `balance = balance;` don't actually set the instance variables. Instead, they just assign the parameter values to themselves.
2. As a result, the instance variables remain uninitialized (null for `accountHolder` and 0.0 for `balance`).

### With `this`
*CODE*
```java
public class BankAccount {
    private String accountHolder;
    private double balance;

    // Constructor without using 'this'
    public BankAccount(String accountHolder, double balance) {
        this.accountHolder = accountHolder; // Problematic!
        this.balance = balance; // Problematic!
    }

    // Method to display account info
    public void displayInfo() {
        System.out.println("Account Holder: " + accountHolder);
        System.out.println("Balance: $" + balance);
    }

    // Main method to test the class
    public static void main(String[] args) {
        BankAccount account = new BankAccount("John Doe", 1000.0);
        account.displayInfo();
    }
}
```
*OUTPUT*
```
Account Holder: John Doe
Balance: $1000.0
```
**EXPLANATION**
With `this` keyword:

1. `this.accountHolder = accountHolder;` correctly assigns the parameter value to the instance variable.
2. `this.balance = balance;` does the same for the balance.
### Benefits of using `this`:

1. It clearly distinguishes between instance variables and parameters/local variables.
2. It prevents the shadowing problem where a parameter name hides an instance variable.
3. It makes the code more readable and self-explanatory.

## 6 uses of this keyword
- `this` keyword can be used to refer current class instance variable.
- `this` keyword can be used to invoke current class method(implicitly)
- `this()` can be used to invoke current class constructor
- `this` can be used to pass as an argument in the method call
- `this` can be used to pass as an argument in the constructor call
- `this` can be used to return the current class instance from the method

1. `this` is used to refer current class instance variable
	- Already discussed above.
2. `this` can be used to invoke current class method(implicitly)
	- implicitly means the compiler will add `this` if we don't specify
*CODE*
```java
public class Calculator {
    private int value;

    public Calculator(int initial) {
        this.value = initial;
    }

    public void add(int num) {
        this.value += num;
        this.displayResult(); // Using 'this' to call current class method
    }

    private void displayResult() {
        System.out.println("Current value: " + this.value);
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator(5);
        calc.add(3);
    }
}
```

*OUTPUT*
```
Current Value:8
```

3. `this`-can be used to invoke current class constructor
*CODE*
```java
public class Person {
    private String name;
    private int age;

    public Person() {
        this("John Doe", 30); // Calls the parameterized constructor
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }

    public static void main(String[] args) {
        Person person1 = new Person();
        person1.displayInfo();

        Person person2 = new Person("Jane Doe", 25);
        person2.displayInfo();
    }
}
```

*OUTPUT*
```
Name: John Doe, Age: 30
Name: Jane Doe, Age: 25
```

4. `this`-can be used to pass as an argument in the method call
*CODE*
```java
public class ThisDemo{
    void m1(ThisDemo td){
        System.out.println("M1 method");
    }
    void m2(){
        m1(this);
    }
    public static void main(String[] args){
        ThisDemo td = new ThisDemo();
        td.m2();
    }
}
```

*OUTPUT*
```
M1 method
```

*CODE*
```java
class Employee {
    private String name;

    public Employee(String name) {
        this.name = name;
    }

    public void introduce(Introducer introducer) {
        introducer.introduce(this);
    }

    public String getName() {
        return this.name;
    }
}

public class Introducer {
    public void introduce(Employee employee) {
        System.out.println("Let me introduce " + employee.getName());
    }

    public static void main(String[] args) {
        Employee emp = new Employee("Alice");
        Introducer introducer = new Introducer();
        emp.introduce(introducer);
    }
}
```

*OUTPUT*
```
Let me introduce Alice
```

5. `this`-can be used to pass as an argument in the constructor call
 *CODE*
```java
class Test{
    Test(ThisDemo td){
        System.out.println("Test Class Constructor");
    }
}
public class ThisDemo{
    void m1(){
        Test t = new Test(this);
    }
    public static void main(String[] args){
        ThisDemo td = new ThisDemo();
        td.m1();
    }
}
```

*OUTPUT*
```
Test Class Constructor
```

*CODE*
```java
public class Car {
    private String model;
    private String color;

    public Car(String model, String color) {
        this.model = model;
        this.color = color;
    }

    public Car getClone() {
        return new Car(this); // Passing 'this' to constructor
    }

    private Car(Car other) {
        this.model = "Clone of " + other.model;
        this.color = other.color;
    }

    public void displayInfo() {
        System.out.println("Model: " + model + ", Color: " + color);
    }

    public static void main(String[] args) {
        Car originalCar = new Car("Tesla", "Red");
        Car clonedCar = originalCar.getClone();

        originalCar.displayInfo();
        clonedCar.displayInfo();
    }
}
```

*OUTPUT*
```
Model: Tesla, Color: Red
Model: Clone of Tesla, Color: Red
```

6. `this`-can be used to return the current class instance from the method
*CODE*
```java
public class StringBuilder {
    private String str;

    public StringBuilder() {
        this.str = "";
    }

    public StringBuilder append(String s) {
        this.str += s;
        return this; // Returning current instance
    }

    public StringBuilder clear() {
        this.str = "";
        return this; // Returning current instance
    }

    public String toString() {
        return this.str;
    }

    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        String result = sb.append("Hello")
                          .append(" ")
                          .append("World")
                          .append("!")
                          .toString();
        System.out.println(result);

        sb.clear().append("New String");
        System.out.println(sb.toString());
    }
}
```

*OUTPUT*
```
Hello World!
New String
```
