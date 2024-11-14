## First Way
```js
const mongoose = require('mongoose');

// User Credit Schema
const userCreditSchema = new mongoose.Schema({
  userId: {
    type: mongoose.Schema.Types.ObjectId,
    required: true,
    ref: 'User'
  },
  credits: {
    type: Number,
    default: 0
  },
  monthlyAllowance: {
    type: Number,
    required: true
  },
  lastResetDate: {
    type: Date,
    default: Date.now
  },
  creditHistory: [{
    amount: Number,
    operation: String, // 'add', 'subtract', 'reset'
    timestamp: {
      type: Date,
      default: Date.now
    },
    description: String
  }]
});

const UserCredit = mongoose.model('UserCredit', userCreditSchema);

class CreditManager {
  // Initialize credit account for a new user
  static async initializeCredits(userId, monthlyAllowance) {
    try {
      const userCredit = new UserCredit({
        userId,
        credits: monthlyAllowance,
        monthlyAllowance,
        lastResetDate: new Date(),
        creditHistory: [{
          amount: monthlyAllowance,
          operation: 'add',
          description: 'Initial credit allocation'
        }]
      });
      
      await userCredit.save();
      return userCredit;
    } catch (error) {
      throw new Error(`Failed to initialize credits: ${error.message}`);
    }
  }

  // Check and reset monthly credits if needed
  static async checkAndResetMonthlyCredits(userId) {
    try {
      const userCredit = await UserCredit.findOne({ userId });
      if (!userCredit) throw new Error('User credit account not found');

      const now = new Date();
      const lastReset = new Date(userCredit.lastResetDate);

      // Check if it's a new month
      if (now.getMonth() !== lastReset.getMonth() || now.getYear() !== lastReset.getYear()) {
        userCredit.credits = userCredit.monthlyAllowance;
        userCredit.lastResetDate = now;
        userCredit.creditHistory.push({
          amount: userCredit.monthlyAllowance,
          operation: 'reset',
          description: 'Monthly credit reset'
        });
        
        await userCredit.save();
      }

      return userCredit;
    } catch (error) {
      throw new Error(`Failed to reset monthly credits: ${error.message}`);
    }
  }

  // Use credits
  static async useCredits(userId, amount, description) {
    try {
      await this.checkAndResetMonthlyCredits(userId);
      
      const userCredit = await UserCredit.findOne({ userId });
      if (!userCredit) throw new Error('User credit account not found');
      
      if (userCredit.credits < amount) {
        throw new Error('Insufficient credits');
      }

      userCredit.credits -= amount;
      userCredit.creditHistory.push({
        amount,
        operation: 'subtract',
        description
      });

      await userCredit.save();
      return userCredit;
    } catch (error) {
      throw new Error(`Failed to use credits: ${error.message}`);
    }
  }

  // Get current credit balance
  static async getCredits(userId) {
    try {
      await this.checkAndResetMonthlyCredits(userId);
      const userCredit = await UserCredit.findOne({ userId });
      if (!userCredit) throw new Error('User credit account not found');
      
      return userCredit.credits;
    } catch (error) {
      throw new Error(`Failed to get credits: ${error.message}`);
    }
  }

  // Get credit history
  static async getCreditHistory(userId) {
    try {
      const userCredit = await UserCredit.findOne({ userId });
      if (!userCredit) throw new Error('User credit account not found');
      
      return userCredit.creditHistory;
    } catch (error) {
      throw new Error(`Failed to get credit history: ${error.message}`);
    }
  }
}

module.exports = CreditManager;
```
This implementation provides a complete monthly credit system with the following features:

1. Monthly credit allowance that resets automatically
2. Credit usage tracking
3. Credit history
4. Automatic monthly resets
5. Error handling

Here's how to use it:
```js
// Initialize credits for a new user
await CreditManager.initializeCredits(userId, 100); // 100 credits per month

// Use credits
await CreditManager.useCredits(userId, 10, 'API call');

// Check current balance
const balance = await CreditManager.getCredits(userId);

// Get credit history
const history = await CreditManager.getCreditHistory(userId);
```

### Add additional features like:
- Credit expiration
- Rollover credits
- Different credit tiers
- Usage analytics

### Second way - With Design Patterns
```js
// Singleton Pattern for CreditManager
class CreditManager {
  private static instance: CreditManager;
  private constructor() {}

  public static getInstance(): CreditManager {
    if (!CreditManager.instance) {
      CreditManager.instance = new CreditManager();
    }
    return CreditManager.instance;
  }

  // Factory Pattern for creating different types of credit operations
  private creditOperationFactory = {
    add: (amount: number, description: string) => ({
      amount,
      operation: 'add',
      timestamp: new Date(),
      description
    }),
    subtract: (amount: number, description: string) => ({
      amount,
      operation: 'subtract',
      timestamp: new Date(),
      description
    }),
    reset: (amount: number) => ({
      amount,
      operation: 'reset',
      timestamp: new Date(),
      description: 'Monthly credit reset'
    })
  };

  // Observer Pattern for credit changes
  private observers: CreditObserver[] = [];

  public addObserver(observer: CreditObserver): void {
    this.observers.push(observer);
  }

  private notifyObservers(userId: string, credits: number, operation: string): void {
    this.observers.forEach(observer => observer.update(userId, credits, operation));
  }
}

// Strategy Pattern for different credit calculation strategies
interface CreditCalculationStrategy {
  calculateCredits(baseAmount: number): number;
}

class StandardCreditStrategy implements CreditCalculationStrategy {
  calculateCredits(baseAmount: number): number {
    return baseAmount;
  }
}

class PremiumCreditStrategy implements CreditCalculationStrategy {
  calculateCredits(baseAmount: number): number {
    return baseAmount * 1.5;
  }
}

// Observer Pattern Interface
interface CreditObserver {
  update(userId: string, credits: number, operation: string): void;
}

// Example observer for logging
class CreditLogger implements CreditObserver {
  update(userId: string, credits: number, operation: string): void {
    console.log(`Credit Update - User: ${userId}, Credits: ${credits}, Operation: ${operation}`);
  }
}

// Example observer for notifications
class NotificationService implements CreditObserver {
  update(userId: string, credits: number, operation: string): void {
    if (credits < 10) {
      this.sendLowCreditsNotification(userId, credits);
    }
  }

  private sendLowCreditsNotification(userId: string, credits: number): void {
    console.log("Low credits notification sent to user ${userId}. Remaining: ${credits}");
  }
}

// Repository Pattern for data access
class CreditRepository {
  async findByUserId(userId: string): Promise<any> {
    return await UserCredit.findOne({ userId });
  }

  async save(creditData: any): Promise<any> {
    return await creditData.save();
  }
}

// Main Credit Service implementing the patterns
class CreditService {
  private creditManager: CreditManager;
  private creditStrategy: CreditCalculationStrategy;
  private repository: CreditRepository;

  constructor(
    creditStrategy: CreditCalculationStrategy = new StandardCreditStrategy(),
    repository: CreditRepository = new CreditRepository()
  ) {
    this.creditManager = CreditManager.getInstance();
    this.creditStrategy = creditStrategy;
    this.repository = repository;

    // Add observers
    this.creditManager.addObserver(new CreditLogger());
    this.creditManager.addObserver(new NotificationService());
  }

  async initializeCredits(userId: string, monthlyAllowance: number): Promise<any> {
    try {
      const calculatedCredits = this.creditStrategy.calculateCredits(monthlyAllowance);
      
      const userCredit = new UserCredit({
        userId,
        credits: calculatedCredits,
        monthlyAllowance: calculatedCredits,
        lastResetDate: new Date(),
        creditHistory: [
          this.creditManager['creditOperationFactory'].add(
            calculatedCredits, 
            'Initial credit allocation'
          )
        ]
      });

      const savedCredit = await this.repository.save(userCredit);
      this.creditManager['notifyObservers'](userId, calculatedCredits, 'initialize');
      return savedCredit;
    } catch (error) {
      throw new Error(`Failed to initialize credits: ${error.message}`);
    }
  }

  async useCredits(userId: string, amount: number, description: string): Promise<any> {
    try {
      await this.checkAndResetMonthlyCredits(userId);
      
      const userCredit = await this.repository.findByUserId(userId);
      if (!userCredit) throw new Error('User credit account not found');
      
      if (userCredit.credits < amount) {
        throw new Error('Insufficient credits');
      }

      userCredit.credits -= amount;
      userCredit.creditHistory.push(
        this.creditManager['creditOperationFactory'].subtract(amount, description)
      );

      const savedCredit = await this.repository.save(userCredit);
      this.creditManager['notifyObservers'](userId, userCredit.credits, 'use');
      return savedCredit;
    } catch (error) {
      throw new Error(`Failed to use credits: ${error.message}`);
    }
  }

  // ... rest of the methods
}

// Usage example
async function main() {
  // Initialize with standard credit strategy
  const standardCreditService = new CreditService();
  await standardCreditService.initializeCredits('user1', 100);

  // Initialize with premium credit strategy
  const premiumCreditService = new CreditService(new PremiumCreditStrategy());
  await premiumCreditService.initializeCredits('user2', 100); // Will get 150 credits
}
```
In this enhanced version, I've implemented several design patterns:

1. **Singleton Pattern**
    - Used for the `CreditManager` class
    - Ensures only one instance of the credit manager exists
    - Controls global state and operations
2. **Factory Pattern**
    - `creditOperationFactory` creates different types of credit operations
    - Encapsulates object creation logic
    - Makes adding new operation types easier
3. **Observer Pattern**
    - Implemented through `CreditObserver` interface
    - Allows multiple observers (Logger, NotificationService) to react to credit changes
    - Decouples credit operations from notification logic
4. **Strategy Pattern**
    - Different credit calculation strategies (Standard, Premium)
    - Allows for easy addition of new calculation methods
    - Can be switched at runtime
5. **Repository Pattern**
    - Abstracts data access logic
    - Makes the code more testable
    - Separates business logic from data access

Benefits of using these patterns:

1. **Loose Coupling**: Components are independent and can be modified without affecting others
2. **Easy to Extend**: New features can be added by implementing new strategies or observers
3. **Maintainable**: Clear separation of concerns makes the code easier to maintain
4. **Testable**: Components can be tested in isolation
5. **Flexible**: Business rules can be changed by adding new strategies or observers