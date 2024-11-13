	# Super 
- super keyword is a reference variable which is used to refer to immediate parent class object.
*CODE*
```java
class A{
    int num=10;
}
class B extends A{
    int num = 20;
    
    void show(int num){
        System.out.println(num);
        System.out.println(this.num);
        System.out.println(super.num);
    }
}

public class Main{
    public static void main(String[] args){
        B b1 = new B();
        b1.show(30);
    }
}
```
*OUTPUT*
```
30
20
10
```
## Uses
1. super keyword can be used to refer immediate parent class instance variable.
	- Already discussed above
2. super keyword can be used to invoke immediate parent class method
*CODE*
```java
class A{
    void greet(){
        System.out.println("Hello, I am greeting you from Class A");
    }
}
class B extends A{
    void greet(){
        System.out.println("Hello, I am greeting you from Class B");
    }
    void show(){
       greet();
       super.greet();
    }
}

public class Main{
    public static void main(String[] args){
        B b1 = new B();
        b1.show();
    }
}
```
*OUTPUT*
```
Hello, I am greeting you from Class B
Hello, I am greeting you from Class A
```
3. super() can be used to invoke immediate parent class constructor
- In Java, constructors in a subclass automatically call the no-argument constructor of the superclass if not explicitly specified. 
- However, we can use super() in a subclass constructor to call a specific constructor in the superclass. 
- This allows you to pass arguments and initialize the superclass's state. For instance, if the superclass has a parameterized constructor, we can use super(argument) in the subclass constructor to ensure proper initialization of the superclass before initializing the subclass-specific attributes.
*CODE-without super()*
```java
class A{
    A(){
        System.out.println("Hello, I am constructing you from Class A");
    }
}
class B extends A{
    B(){
        System.out.println("Hello, I am constructing you from Class B");
    }
}

public class Main{
    public static void main(String[] args){
        B b1 = new B();
    }
}
```
*OUTPUT*
```
Hello, I am constructing you from Class A
Hello, I am constructing you from Class B
```
*CODE - with super()*
```java
class A{
    A(){
        System.out.println("Hello, I am constructing you from Class A");
    }
}
class B extends A{
    B(){
        super();
        System.out.println("Hello, I am constructing you from Class B");
    }
}

public class Main{
    public static void main(String[] args){
        B b1 = new B();
    }
}
```
*OUTPUT*
```
Hello, I am constructing you from Class A
Hello, I am constructing you from Class B
```

*CODE - Parameterized Constructor call and initialization using super*
```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void introduce() {
        System.out.println("Hi, I'm " + name + " and I'm " + age + " years old.");
    }
}

class Employee extends Person {
    private String company;

    public Employee(String name, int age, String company) {
        super(name, age); // Call the parent class constructor
        this.company = company;
    }

    @Override
    public void introduce() {
        super.introduce(); // Call the parent class method
        System.out.println("I work at " + company + ".");
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee("John", 30, "TechCorp");
        emp.introduce();
    }
}
```
*OUTPUT*
```
Hi, I'm John and I'm 30 years old.
I work at TechCorp.
```