# Encapsulation
- Encapsulation in java is a mechanism of wrapping the data(variables) and code acting on the data(methods) together as a single unit.
- Encapsulation is used to hide the values or state of a structured data object inside a class, preventing unauthorized parties' direct access to them.
- In encapsulation, the variables of a class will be hidden from other classes, and can be accessed only through the methods of their current class. this concept is known as data hiding.
## Key Aspects of Encapsulation
1. **Data Hiding**: The object's internal representation is hidden from the outside world.
2. **Access Control**: Controlling what parts of a program can access the members of a class.
3. **Bundling**: Keeping related data and methods together.
4. **Interface**: Providing a public interface for interacting with the object's data.
## Benefits of Encapsulation:
1. **Improved Maintainability**: Changes to the internal implementation don't affect external code.
2. **Increased Flexibility**: Implementation details can be changed without affecting the public interface.
3. **Enhanced Security**: Direct access to data is restricted, preventing unauthorized modifications.
4. **Modularity**: Objects become self-contained units, easier to understand and manage.
## Steps to achieve encapsulation
- Declare the variables of class as private.
- Provide public setter and getter methods to modify and view the variable values.

## Example
```java
public class BankAccount {
    private String accountNumber;
    private String accountHolder;
    private double balance;
    private boolean isLocked;

    public BankAccount(String accountNumber, String accountHolder) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = 0.0;
        this.isLocked = false;
    }

    // Getter for account number
    public String getAccountNumber() {
        return accountNumber;
    }

    // Getter for account holder
    public String getAccountHolder() {
        return accountHolder;
    }

    // Getter for balance
    public double getBalance() {
        return balance;
    }

    // Method to deposit money
    public void deposit(double amount) {
        if (isLocked) {
            System.out.println("Transaction failed. Account is locked.");
            return;
        }
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    // Method to withdraw money
    public void withdraw(double amount) {
        if (isLocked) {
            System.out.println("Transaction failed. Account is locked.");
            return;
        }
        if (amount > 0 && balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
        } else {
            System.out.println("Invalid withdrawal amount or insufficient funds.");
        }
    }

    // Method to lock the account
    public void lockAccount() {
        isLocked = true;
        System.out.println("Account locked.");
    }

    // Method to unlock the account
    public void unlockAccount() {
        isLocked = false;
        System.out.println("Account unlocked.");
    }
}

// Example usage
public class BankDemo {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("1234567890", "John Doe");

        account.deposit(1000);
        account.withdraw(500);
        System.out.println("Current Balance: $" + account.getBalance());

        account.lockAccount();
        account.withdraw(200); // This will fail

        account.unlockAccount();
        account.withdraw(200); // This will succeed
        System.out.println("Final Balance: $" + account.getBalance());
    }
}
```
**EXPLANATION**
In this example:
1. **Data Hiding**: All instance variables (`accountNumber`, `accountHolder`, `balance`, `isLocked`) are declared as private. This prevents direct access from outside the class.
2. **Access Control**: Public methods are provided to interact with the account data. For example, `getBalance()` allows reading the balance, while `deposit()` and `withdraw()` methods allow modifying it.
3. **Bundling**: All data and methods related to a bank account are kept together in the `BankAccount` class.
4. **Interface**: The class provides a clear public interface for interacting with bank accounts.
5. **Validation and Business Logic**: Methods like `deposit()` and `withdraw()` include logic to validate actions and maintain the integrity of the account state.
6. **Additional Functionality**: Methods like `lockAccount()` and `unlockAccount()` demonstrate how additional features can be added while maintaining encapsulation.

**Benefits Demonstrated**:

1. **Security**: Direct manipulation of the balance is not possible. All transactions must go through the `deposit()` or `withdraw()` methods, which include necessary checks.
2. **Flexibility**: If we need to change how balances are stored or calculated (e.g., switching to BigDecimal for better precision), we only need to modify the `BankAccount` class internals without affecting external code.
3. **Maintainability**: The implementation of account locking can be changed without affecting how other parts of the system interact with the `BankAccount` class.
