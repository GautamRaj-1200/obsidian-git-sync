## `static` keyword
- Static keyword is primarily used for memory management.
- It can be applied to 
	- Variables
	- Methods
	- Blocks
	- Nested Classes
- **Main Concept**: It belongs to the class rather than instances of the class.
	- Ex: Suppose you have a School class then "the name of the school" - belongs to the class
	- Ex: Suppose you have a Student class then "the count(total number) of students" - belongs to the class.
- Whenever we need to attach any thing to the class not with the instances, we can use static keyword.
- So, It ***saves memory*** as we would not be creating that variable for every instance that we create.
- Example
### static variable
*CODE*
```java
package static_keyword;  
  
public class Student {  
    private String name;  
    private int age;  
  
    public static int count = 0;  //public static variable
    
    public Student(String name, int age){  
        this.name =name;  
        this.age = age;  
        count++;  
    }  
}  
class StudentMain{  
    public static void main(String[] args) {  
        Student s1 = new Student("John",20);  
        Student s2 = new Student("Martin",18);  
        Student s3 = new Student("David",21);  
        Student s4 = new Student("Yuri",17);  
        Student s5 = new Student("Watson",22);  
        
        System.out.println(Student.count);  //5
    }  
}
```
*OUTPUT*
```
5
```

### static method
*CODE*
```java
package static_keyword;  
  
public class Student {  
    private String name;  
    private int age;  
  
    private static int count = 0;  //private static variable
  
    public Student(String name, int age){  
        this.name =name;  
        this.age = age;  
        count++;  
    }  
  
    public static int getCount(){  //public static method
        return count;  
    }  
}  
class StudentMain{  
    public static void main(String[] args) {  
        Student s1 = new Student("John",20);  
        Student s2 = new Student("Martin",18);  
        Student s3 = new Student("David",21);  
        Student s4 = new Student("Yuri",17);  
        Student s5 = new Student("Watson",22);  
        
        System.out.println(Student.getCount());  //5
    }  
}
```
*OUTPUT*
```
5
```
### static block
- Java supports a special block, called a static block (also called static clause) that can be used for static initialization of a class. 
- This code inside the static block is executed only once: the first time the class is loaded into memory.
- We can initialize static variables directly in the class but if we want to implement any logic on that then static block is better. 
- It is good for one time setup tasks.
- Example:
*CODE*
```java
package static_keyword;  
  
public class StudentThree{  
    private String name;  
    private int age;  
  
    private static int count;  
  
    // Static block  
    static {  
        System.out.println("Static block executed. Initializing count...");  
        count = 0;  
    }  
  
    public StudentThree(String name, int age) {  
        this.name = name;  
        this.age = age;  
        count++;  
    }  
  
    public static int getCount() {  
        return count;  
    }  
}  
  
class StudentMainThree {  
    public static void main(String[] args) {  
        StudentThree s1 = new StudentThree("John", 20);  
        StudentThree s2 = new StudentThree("Martin", 18);  
        StudentThree s3 = new StudentThree("David", 21);  
        StudentThree s4 = new StudentThree("Yuri", 17);  
        StudentThree s5 = new StudentThree("Watson", 22);  
        System.out.println("Total number of students: " + StudentThree.getCount());  
    }  
}
```
*OUTPUT*
```
Static block executed. Initializing count...
Total number of students: 5
```
***Important Points***
- Frequently used(Utility) methods are generally created as static
- `this`and `super` can't be used in the static context.
- static is widely used in singleton design patterns

- Example: Utils
*CODE*
```java
package static_keyword;  
  
public class StudentFour {  
    public static void main(String[] args) {  
        System.out.println(Utils.trimAndUpperCase("   Jack Sparrow     "));  
    }  
}
```

```java
package static_keyword;  
  
public class Utils {  
    public static String trimAndUpperCase(String name){  
        return name.trim().toUpperCase();  
    }  
}
```
*OUTPUT*
```
JACK SPARROW
```