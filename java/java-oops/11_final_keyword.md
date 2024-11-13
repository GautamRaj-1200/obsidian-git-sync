# final keyword
### final variable - It becomes constant, it can't be changed.
*CODE*
```java
class Circle {
    private final double PI = 3.14159265359;
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double calculateArea() {
        return PI * radius * radius;
    }

    public double calculateCircumference() {
        return 2 * PI * radius;
    }
}

public class Main {
    public static void main(String[] args) {
        Circle circle = new Circle(5);
        System.out.println("Area: " + circle.calculateArea());
        System.out.println("Circumference: " + circle.calculateCircumference());

        // Attempting to modify PI would result in a compilation error
        // circle.PI = 3.14; // This line would cause an error if uncommented
    }
}
```
*OUTPUT*
```
Area: 78.53981633974999
Circumference: 31.4159265359
```
**EXPLANATION**
> In this example, `PI` is a `final` variable, ensuring that its value remains constant throughout the program's execution. This prevents accidental modifications to this important mathematical constant.

### final method - It cannot be overridden
*CODE*
```java
public class BankAccount {
    private double balance;
    private final double INTEREST_RATE = 0.05; // 5% interest rate

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public final double calculateInterest() {
        return balance * INTEREST_RATE;
    }

    public void addInterest() {
        double interest = calculateInterest();
        balance += interest;
        System.out.println("Added interest: $" + interest);
        System.out.println("New balance: $" + balance);
    }
}

class SavingsAccount extends BankAccount {
    public SavingsAccount(double initialBalance) {
        super(initialBalance);
    }

    // Attempting to override calculateInterest() would result in a compilation error
    // public double calculateInterest() { ... } // This method would cause an error if uncommented
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount(1000);
        account.addInterest();

        SavingsAccount savingsAccount = new SavingsAccount(2000);
        savingsAccount.addInterest();
    }
}
```
*OUTPUT*
```
Added interest: $50.0
New balance: $1050.0
Added interest: $100.0
New balance: $2100.0
```
**EXPLANATION**
> In this example, the `calculateInterest()` method is declared as `final`. This ensures that all  subclasses (like `SavingsAccount`) use the same interest calculation method, preventing potential errors or fraud that could occur if this critical financial calculation were altered.

### final class - It cannot be inherited or extended
*EXAMPLE*
```java
final class One{
    void display(){
        System.out.println("hello");
    }
}
class Two extends One{ // error: cannot inherit from final One

}
public class Main{
    public static void main(String[] args){
        One ob1 = new One();
        ob1.display();
    }
}
```
*CODE*
```java
final class SecurityManager {
    private String encryptionKey;

    public SecurityManager(String key) {
        this.encryptionKey = key;
    }

    public String encrypt(String data) {
        // Simplified encryption for demonstration
        return data + encryptionKey;
    }

    public String decrypt(String encryptedData) {
        // Simplified decryption for demonstration
        return encryptedData.substring(0, encryptedData.length() - encryptionKey.length());
    }
}

// Attempting to extend SecurityManager would result in a compilation error
// class CustomSecurityManager extends SecurityManager { } // This class would cause an error if uncommented

public class Main {
    public static void main(String[] args) {
        SecurityManager securityManager = new SecurityManager("secretKey");
        String sensitiveData = "Confidential information";

        String encryptedData = securityManager.encrypt(sensitiveData);
        System.out.println("Encrypted: " + encryptedData);

        String decryptedData = securityManager.decrypt(encryptedData);
        System.out.println("Decrypted: " + decryptedData);
    }
}
```
*OUTPUT*
```
Encrypted: Confidential informationsecretKey
Decrypted: Confidential information
```
**EXPLANATION**
> In this example, `SecurityManager` is declared as a `final` class. This prevents other classes from extending it, which is crucial for maintaining the integrity and security of the encryption and decryption processes. By making the class `final`, we ensure that no one can create a subclass that might compromise the security features or leak sensitive information.

