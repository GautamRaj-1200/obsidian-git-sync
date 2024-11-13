# Interface
- An interface in Java is a completely abstract class that is used to group related methods with empty bodies. 
- It serves as a contract for classes that implement it, specifying what methods a class must implement without dictating how these methods should be implemented.

## Why interface?
- it is used to achieve abstraction.
- It supports multiple inheritance
- It can be used to achieve loose coupling.
	- loose coupling is a design goal that seeks to reduce the inter-dependencies between components of a system with the goal of reducing the risk that changes in one component will require changes in any other component. Loose coupling is much more generic concept intended to increase the flexibility of the system, make it more maintainable and makes the entire framework more stable.
## Key Characteristics of Interfaces:
**SYNTAX**
```java
interface InterfaceName{
	//public abstract methods
	// public static final field
	// default void display
}
```
- All methods are implicitly public and abstract (except for default, static, and private methods introduced in later Java versions).
	-  From java 8th version 
		- we can create `default concrete methods`
		- we can create `public static methods`
	- From Java 9th version - we can create `private methods`
- All variables are implicitly public, static, and final.
- A class can implement multiple interfaces, enabling a form of multiple inheritance.
- Interfaces cannot be instantiated.
## Why Use Interfaces?

1. **Achieve Abstraction**: Interfaces provide a way to achieve 100% abstraction.
2. **Multiple Inheritance**: Java doesn't support multiple inheritance of classes, but a class can implement multiple interfaces.
3. **Loose Coupling**: Interfaces allow for flexibility in code design, reducing dependencies between different parts of a program.
4. **Standardization**: They provide a way to enforce certain properties on a class.

## Example: Payment Processing System
```java
// Define the payment processor interface
public interface PaymentProcessor {
    boolean processPayment(double amount);
    void refundPayment(double amount);
    default void displayPaymentMethod() {
        System.out.println("Generic Payment Method");
    }
}

// Credit Card payment processor
public class CreditCardProcessor implements PaymentProcessor {
    private String cardNumber;
    private String expiryDate;

    public CreditCardProcessor(String cardNumber, String expiryDate) {
        this.cardNumber = cardNumber;
        this.expiryDate = expiryDate;
    }

    @Override
    public boolean processPayment(double amount) {
        // Logic to process credit card payment
        System.out.println("Processing credit card payment of $" + amount);
        return true;
    }

    @Override
    public void refundPayment(double amount) {
        // Logic to refund to credit card
        System.out.println("Refunding $" + amount + " to credit card");
    }

    @Override
    public void displayPaymentMethod() {
        System.out.println("Credit Card Payment");
    }
}

// PayPal payment processor
public class PayPalProcessor implements PaymentProcessor {
    private String email;

    public PayPalProcessor(String email) {
        this.email = email;
    }

    @Override
    public boolean processPayment(double amount) {
        // Logic to process PayPal payment
        System.out.println("Processing PayPal payment of $" + amount);
        return true;
    }

    @Override
    public void refundPayment(double amount) {
        // Logic to refund via PayPal
        System.out.println("Refunding $" + amount + " via PayPal");
    }

    @Override
    public void displayPaymentMethod() {
        System.out.println("PayPal Payment");
    }
}

// Main payment service
public class PaymentService {
    public void makePayment(PaymentProcessor processor, double amount) {
        processor.displayPaymentMethod();
        if (processor.processPayment(amount)) {
            System.out.println("Payment successful");
        } else {
            System.out.println("Payment failed");
        }
    }

    public void processRefund(PaymentProcessor processor, double amount) {
        processor.refundPayment(amount);
    }
}
```
*OUTPUT*
```
Credit Card Payment
Processing credit card payment of $100.0
Payment successful
PayPal Payment
Processing PayPal payment of $50.0
Payment successful
Refunding $25.0 to credit card
Refunding $10.0 via PayPal
```

**EXPLANATION**
This design demonstrates several benefits of using interfaces:
1. **Abstraction**: The `PaymentService` doesn't need to know the specifics of how each payment method works.
2. **Loose Coupling**: We can easily add new payment methods (e.g., `BitcoinProcessor`) without changing the `PaymentService` class.
3. **Polymorphism**: We can treat different payment processors uniformly through the `PaymentProcessor` interface.
4. **Flexibility**: The system is open for extension (new payment methods) but closed for modification (existing code doesn't need to change).

### Multiple inheritance using interface
```java
// Existing PaymentProcessor interface
interface PaymentProcessor {
    boolean processPayment(double amount);
    void refundPayment(double amount);
}

// New interface for secure transactions
interface SecureTransaction {
    void encrypt();
    void decrypt();
}

// New interface for international payments
interface InternationalPayment {
    void setExchangeRate(double rate);
    double convertCurrency(double amount);
}

// Updated CreditCardProcessor implementing multiple interfaces
class CreditCardProcessor implements PaymentProcessor, SecureTransaction, InternationalPayment {
    private String cardNumber;
    private String expiryDate;
    private double exchangeRate = 1.0;

    public CreditCardProcessor(String cardNumber, String expiryDate) {
        this.cardNumber = cardNumber;
        this.expiryDate = expiryDate;
    }

    @Override
    public boolean processPayment(double amount) {
        System.out.println("Processing secure international credit card payment of $" + amount);
        return true;
    }

    @Override
    public void refundPayment(double amount) {
        System.out.println("Refunding $" + amount + " to credit card");
    }

    @Override
    public void encrypt() {
        System.out.println("Encrypting credit card data");
    }

    @Override
    public void decrypt() {
        System.out.println("Decrypting credit card data");
    }

    @Override
    public void setExchangeRate(double rate) {
        this.exchangeRate = rate;
    }

    @Override
    public double convertCurrency(double amount) {
        return amount * exchangeRate;
    }
}

// Main payment service
class PaymentService {
    public void processInternationalPayment(PaymentProcessor processor, double amount) {
        if (processor instanceof SecureTransaction) {
            ((SecureTransaction) processor).encrypt();
        }
        
        if (processor instanceof InternationalPayment) {
            InternationalPayment intl = (InternationalPayment) processor;
            intl.setExchangeRate(1.2); // Example exchange rate
            amount = intl.convertCurrency(amount);
        }

        if (processor.processPayment(amount)) {
            System.out.println("International payment successful");
        } else {
            System.out.println("International payment failed");
        }

        if (processor instanceof SecureTransaction) {
            ((SecureTransaction) processor).decrypt();
        }
    }
}
public class Main {
    public static void main(String[] args) {
        PaymentService paymentService = new PaymentService();
        CreditCardProcessor creditCard = new CreditCardProcessor("1234-5678-9012-3456", "12/25");
        
        paymentService.processInternationalPayment(creditCard, 100.00);
    }
}
```
*OUTPUT*
```
Encrypting credit card data
Processing secure international credit card payment of $120.0
International payment successful
Decrypting credit card data
```

**EXPLANATION**
This updated example demonstrates multiple inheritance through interfaces:

1. We've added two new interfaces: `SecureTransaction` and `InternationalPayment`.
2. The `CreditCardProcessor` class now implements three interfaces: `PaymentProcessor`, `SecureTransaction`, and `InternationalPayment`.
3. This allows `CreditCardProcessor` to inherit abstract methods from multiple interfaces, effectively achieving multiple inheritance.

**Key points**:

1. **Multiple Inheritance**: The `CreditCardProcessor` class inherits behavior from three different interfaces, showcasing how interfaces enable a form of multiple inheritance in Java.
2. **Flexibility**: We can add new functionalities (like security and international payments) without modifying the existing `PaymentProcessor` interface.
3. **Polymorphism**: The `PaymentService` can work with objects that implement any combination of these interfaces, checking for capabilities at runtime.