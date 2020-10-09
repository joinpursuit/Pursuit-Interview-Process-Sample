# Common Elements of Two Arrays

https://leetcode.com/problems/intersection-of-two-arrays/

## Prompt

Given two arrays, write a function that returns all elements that appear in both arrays.

## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:

- Should there be duplicates in the final array? _No, each element in the resulting array must be unique_
- Do I need to preserve the order of the inputs? _No, the result can be in any order_
- Can the inputs be empty? _Yes, an array may contain zero elements._

## Sample Inputs and Outputs

### Example One:

#### Input

```swift
let firstArr = [1,2,2,1]
let secondArr = [2,2]
```

#### Output

```swift
let correctOutput = [2]
```

### Example Two:

#### Input

```swift
let firstArr = [4,9,5]
let secondArr = [9,4,9,8,4]
```

#### Output

```swift
let correctOutput = [9,4]
```

## Hints

If a fellow has been stuck for several minutes, it's OK to offer a hint to keep things moving:

- How can we remove duplicate elements from an array?
- What data structure can tell us whether it contains an element in O(1) time?

## Solution Overview

1. Convert the input arrays into Sets to get unique elements
1. Iterate over one of the sets and filter out all of the elements that are not contained in the other set.

## Solution Code

### Swift

```swift
func intersection(_ nums1: [Int], _ nums2: [Int]) -> [Int] {
    return Array(Set(nums1).intersection(Set(nums2)))
}
```

If they use `.intersection`, prompt them to build a solution without using the built in method:

```swift
func intersection(_ nums1: [Int], _ nums2: [Int]) -> [Int] {
    let numsOneSet = Set(nums1)
    let numsTwoSet = Set(nums2)
    var intersectionSet = Set<Int>()
    for num in numsOneSet {
        if numsTwoSet.contains(num) {
            intersectionSet.insert(num)
        }
    }
    return Array(intersectionSet)
}
```

### JavaScript

```js
const intersection = (nums1, nums2) => {
    const nums2Set = new Set(nums2)
    return [... new Set(nums1)].filter(val => nums2Set.has(val))
};
```
