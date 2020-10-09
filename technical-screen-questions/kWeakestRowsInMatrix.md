# k Weakest Rows in Matrix

https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/

## Prompt

Given a `m * n` matrix mat of ones (representing soldiers) and zeros (representing civilians), return the indexes of the `k` weakest rows in the matrix ordered from the weakest to the strongest.

A row ***i*** is weaker than row ***j***, if the number of soldiers in row ***i*** is less than the number of soldiers in row ***j***, or they have the same number of soldiers but ***i*** is less than ***j***. Soldiers are **always** stand in the frontier of a row, that is, always ones may appear first and then zeros.

## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:

- What if two rows have the same number of soldiers? _The higher row is weaker_
- Will any of the rows be different lengths? _No, all rows will be the same length n_
- Can `k` be zero? _No, k will be between 1 and m_
- Can the matrix ever have no rows or no columns? _No: 2 <= n, m <=100_

## Sample Inputs and Outputs

### Example One:

#### Input

```swift
let matrix = [[1,1,0,0,0],
              [1,1,1,1,0],
              [1,0,0,0,0],
              [1,1,0,0,0],
              [1,1,1,1,1]]
let k = 3              
```

#### Output

```swift
let correctOutput = [2,0,3]
```
#### Explanation

The number of soldiers for each row is:
- row 0 -> 2
- row 1 -> 4
- row 2 -> 1
- row 3 -> 2
- row 4 -> 5

Rows ordered from the weakest to the strongest are [2,0,3,1,4]

### Example Two:

#### Input

```swift
let matrix = [[1,0,0,0],
              [1,1,1,1],
              [1,0,0,0],
              [1,0,0,0]]
let k = 2              
```

#### Output

```swift
let correctOutput = [0,2]
```
#### Explanation

The number of soldiers for each row is:
- row 0 -> 1
- row 1 -> 4
- row 2 -> 1
- row 3 -> 1

Rows ordered from the weakest to the strongest are [0,2,3,1]

## Hints

If a fellow has been stuck for several minutes, it's OK to offer a hint to keep things moving:

- Is there a data structure we could use to organize the mapping between the row and it's strength?
- How will you handle two rows with the same strength?
- Once you have the strength mapping, how will you order it?

## Solution Overview

1. Build a dictionary mapping the row to its strength.
2. Convert the dictionary into an array of tuples sorted by the strength of the row.  If the strengths are equal, order the higher row first.
3. Map the sorted array to only the keys (rows indices), the get the first k elements

## Solution Code

### Swift

```swift
func kWeakestRows(_ mat: [[Int]], _ k: Int) -> [Int] {
    var dict = [Int: Int]()
    for rowIndex in 0..<mat.count {
        let row = mat[rowIndex]
        dict[rowIndex] = row.reduce(0) { $0 + $1 }
    }
    let sortedKeyValueTupleArr = dict.sorted {
        if $0.value == $1.value {
            return $0.key < $1.key
        } else {
            return $0.value < $1.value    
        }            
    }
    return Array(sortedKeyValueTupleArr.map{ $0.key }.prefix(k))
}
```

### JavaScript

```js
const kWeakestRows = (mat, k) => {
    let rowStrengths = []
    for (let rowIndex = 0; rowIndex < mat.length; rowIndex++) {
        const strength = mat[rowIndex].reduce((a, b) => a + b)
        rowStrengths.push({strength, rowIndex})
    }
    let sortedStrengths = rowStrengths.sort((obj1, obj2) => {
        if (obj1.strength == obj2.strength) {
            return obj1.rowIndex - obj2.rowIndex
        } else {
            return obj1.strength - obj2.strength
        }
    })
    return sortedStrengths.map((obj) => obj.rowIndex).slice(0, k)
}
```
