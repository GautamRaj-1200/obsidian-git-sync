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

