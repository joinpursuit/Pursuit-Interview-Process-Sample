# Lemonade Change

https://leetcode.com/problems/lemonade-change/

## Prompt

At a lemonade stand, each lemonade costs $5.

Customers are standing in a queue to buy from you, and order one at a time (in the order specified by bills).

Each customer will only buy one lemonade and pay with either a $5, $10, or $20 bill.  You must provide the correct change to each customer, so that the net transaction is that the customer pays $5.

Return true if and only if you can provide every customer with correct change.


## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:

- Do you start with any change? _No, you start with 0 bills_
- Can there be zero customers? _Yes, then return true_
- Does the order matter? _Yes, you must serve each customer in order by their index in the bills array_
- Can they pay with  ($1 / $50 / $100) bills or with quarters, nickels, dimes, or pennies? _No, each bill will be either 5, 10, or 20_

## Sample Inputs and Outputs

### Example One:

#### Input

```swift
let input = [5,5,5,10,20]
```

#### Output

```swift
let expectedOutput = true
```
#### Explanation

From the first 3 customers, we collect three $5 bills in order.

From the fourth customer, we collect a $10 bill and give back a $5.

From the fifth customer, we give a $10 bill and a $5 bill.

Since all customers got correct change, we output true.

### Example Two:

#### Input

```swift
let input = [5,5,10]
```

#### Output

```swift
let expectedOutput = true
```
#### Explanation

We collect two $5 bills from the first two customers and give one back as change to the last customer.

### Example Three:

#### Input

```swift
let input = [10,10]
```

#### Output

```swift
let expectedOutput = false
```
#### Explanation

The first customer needs $5 back in change, but we don't have any five dollar bills.

### Example Four:

#### Input

```swift
let input = [5,5,10,10,20]
```

#### Output

```swift
let expectedOutput = false
```
#### Explanation

From the first two customers in order, we collect two $5 bills.

For the next two customers in order, we collect a $10 bill and give back a $5 bill.

For the last customer, we can't give change of $15 back because we only have two $10 bills.

Since not every customer received correct change, the answer is false.

## Hints

If a fellow has been stuck for several minutes, it's OK to offer a hint to keep things moving:

- How can we track the money that we've received so far?
- What are the different ways that we can make change for a $20 bill?  Which one should we try first?
- How do we know that we can't make change for the next customer?


## Solution Overview

- Make variables to track the number of 5s and 10s on hand
- Iterate through each bill in the input array
  - If the bill is a five, add one to your fives on hand
  - If the bill is a ten, add a ten and take away one of your fives
  - If the bill is a twenty, first try to make change with a ten and a five.  If you don't have any tens, make change with three fives.
  - Check to make sure you didn't give away a five you didn't have
- If you made it through each customer without running out of fives, return true.

### Notes

- Making change for a twenty with a ten and a five is always better than making change with three fives.  This is because two fives is more valuable than one ten for making change.
- The greedy algorithm explained above would not work if the bills were different and there wasn't a single answer for how best to make change.  A [dynamic programming approach](https://leetcode.com/problems/lemonade-change/discuss/370939/Dynamic-Programming-solution) would then be necessary.

## Solution Code

### Swift

```swift
func lemonadeChange(_ bills: [Int]) -> Bool {        
    var fives = 0
    var tens = 0
    for bill in bills {   
        switch bill {
        case 5:
            fives += 1
        case 10:
            tens += 1
            fives -= 1
        case 20:
            if tens > 0 {
                tens -= 1
                fives -= 1
            } else {
                fives -= 3
            }
        default: fatalError("Unexpected bill")
        }
        guard fives >= 0 else { return false }
    }
    return true
}
```

### JavaScript

```js
var lemonadeChange = function(bills) {
    let fives = 0, tens = 0;
    for (let bill of bills) {
        if (bill === 5) {
            fives++;
        }
        else if (bill === 10) {
            fives--;
            tens++;
        } else if (bill === 20 && tens > 0) {
            fives--;
            tens--;
        } else {
            fives-=3;
        }
        if (fives < 0) return false ;
    }
    return true;
};
```
