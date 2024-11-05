# Abstraction
- Abstraction is a fundamental principle in object-oriented programming (OOP) that allows us to hide complex implementation details while exposing only the essential features of an object. It's about creating a simplified view of an object or system, focusing on what it does rather than how it does it.

## Two ways of achieving Abstraction
- Abstract classes (0-100)%
- Interface (100)%

## Abstract Class
- An abstract class is a class that cannot be instantiated and is typically used as a base class for other classes. It may contain a mix of concrete (fully implemented) methods and abstract methods (methods without a body).
- **ABSTRACT METHOD**: A method without body (no implementation) is known as an abstract method.

### Key characteristics of Abstract classes
- If a class has an abstract method, it should be declared abstract as well.
	- But it is not necessary to have abstract method inside an abstract class.
- If a regular class extends an abstract class, then the class must have to implement all the abstract methods of abstract parent class or it has to be declared abstract as well.
- Abstract methods in an abstract class are meant to be overridden in derived concrete classes otherwise compile-time error will be thrown.
- Abstract classes can't be instantiated, means we can't create objects of abstract class.
- Can have final methods which will prevent method overriding
- Can have instance variables

### Why use Abstract Classes?
- **Code Reusability**: Abstract classes allow you to define a common interface and shared functionality for a group of related classes.
- **Enforcing a Contract**: They can define a set of methods that derived classes must implement, ensuring a consistent interface.
- **Partial Implementation**: You can provide some implemented methods while leaving others to be implemented by subclasses.
- **Flexibility**: They offer more flexibility than interfaces, as they can contain both abstract and concrete methods.

### Example : Game Character System
```java
abstract class GameCharacter {
    protected String name;
    protected int health;
    protected int level;

    public GameCharacter(String name, int health, int level) {
        this.name = name;
        this.health = health;
        this.level = level;
    }

    // Concrete method
    public void displayInfo() {
        System.out.println("Name: " + name + ", Health: " + health + ", Level: " + level);
    }

    // Abstract methods
    public abstract void attack();
    public abstract void defend();
    public abstract void specialAbility();
}

class Warrior extends GameCharacter {
    public Warrior(String name, int health, int level) {
        super(name, health, level);
    }

    @Override
    public void attack() {
        System.out.println(name + " swings a sword!");
    }

    @Override
    public void defend() {
        System.out.println(name + " raises a shield!");
    }

    @Override
    public void specialAbility() {
        System.out.println(name + " enters a berserker rage!");
    }
}

class Mage extends GameCharacter {
    public Mage(String name, int health, int level) {
        super(name, health, level);
    }

    @Override
    public void attack() {
        System.out.println(name + " casts a fireball!");
    }

    @Override
    public void defend() {
        System.out.println(name + " creates a magical barrier!");
    }

    @Override
    public void specialAbility() {
        System.out.println(name + " teleports to safety!");
    }
}
public class Main{
	public static void main(String[] args){
		GameCharacter warrior = new Warrior("Conan", 100, 5); 
		GameCharacter mage = new Mage("Gandalf", 80, 7); 
		warrior.displayInfo(); // Uses method from abstract class
		warrior.attack(); // Uses overridden method 
		mage.displayInfo(); // Uses method from abstract class
		mage.specialAbility(); // Uses overridden method
	}
}
```
``
*OUTPUT*
```
Name: Conan, Health: 100, Level: 5
Conan swings a sword!
Name: Gandalf, Health: 80, Level: 7
Gandalf teleports to safety!
```

*EXPLANATION*
In this example:
1. `GameCharacter` is an abstract class that defines common attributes (name, health, level) and a concrete method (`displayInfo()`).
2. It also declares abstract methods (`attack()`, `defend()`, `specialAbility()`) that must be implemented by subclasses.
3. `Warrior` and `Mage` are concrete classes that extend `GameCharacter` and provide specific implementations for the abstract methods.

This structure allows for:
- **Code Reuse**: Common functionality (like `displayInfo()`) is implemented once in the abstract class.
- **Polymorphism**: You can create an array or list of `GameCharacter` objects that can hold both `Warrior` and `Mage` instances.
- **Enforcement of Structure**: Any new character type must implement the basic actions defined in `GameCharacter`.
- **Flexibility**: You can easily add new character types by extending `GameCharacter`.

## Abstraction vs Encapsulation
| Feature               | Abstraction                                    | Encapsulation                                   |
|-----------------------|------------------------------------------------|------------------------------------------------|
| Definition            | Simplifying complex systems by focusing on essential features and hiding unnecessary details. | Bundling data and methods that operate on that data within a single unit (class), restricting access to some of the object's components. |
| Purpose               | To reduce complexity and increase efficiency by exposing only relevant attributes. | To protect the internal state of an object and control access through methods. |
| Example               | Using an abstract class or interface to define a blueprint for derived classes. | Using private variables and public methods (getters/setters) in a class. |
| Focus                 | Emphasizes "what" an object does.             | Emphasizes "how" an object is structured and its internal workings. |
| Visibility            | Can expose only essential features.            | Controls visibility of data and methods (public, private, protected). |
| Relation to OOP       | A fundamental principle that guides design.    | A technique to implement data hiding within OOP. |
| Real-World Analogy    | Driving a car (you know how to operate it without needing to understand the engine). | A pill capsule (the medicine is inside, and the outer shell protects it). |