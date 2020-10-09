# Second Largest Value


## Prompt

Write a function that accepts an array of integers as input,
and returns the second-largest value in that array.


## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:
* Will the input array be sorted? _No_
* Could the array have length 0 or 1? _No; assume the input array will always have a length >= 2_
* Will all the values in the array be positive? _Not necessarily; could be positive, negative, or zero_
* What if there are multiple copies of the largest integer, like [1, 5, 2, 5, 3]? _Then the second largest would be 5; it can be equivalent to the largest in that case_
* Is an O(nlogn) solution acceptable, for example sorting the array then returning the second to last value? _That would yield the correct result, but let's find an O(n) algorithm instead_


## Sample Inputs & Outputs

| Input | Output |
|---|---|
| [4, -7, 5, 1] | 4 |
| [3, 2, 1, 0] | 2 |
| [-1, -2, -3] | -2 |
| [1, 5, 2, 5, 3]  | 5 |
| [5, 5, 5, 5] | 5 |


## Hints

If a fellow has been stuck for several minutes,
it's OK to offer a hint to keep things moving:
* If they really don't know where to begin, ask how they might be able to look at each value in the array one at a time. (i.e. iterate over it with a loop)
* If they don't know what to do inside the loop, ask what it is that we want to determine about each value (i.e. is it bigger than the largest we've seen so far? is it bigger than the 2nd largest we've seen so far?)
* If they initialize their temp variables (e.g. largest and secondLargest) to zero, ask what would happen if all entries in the input array were negative.

## Solution Overview

General steps:
* Declare two temp variables: largest and secodLargest
  * Initialize largest to the larger of the first two values in the array
  * Initialize secondLargest to the other of the first values
* Iterate through the remaining values in the array
* For each value, check if it is larger than largest
  * If yes, overwrite secondLargest with largest, and largest w/ the current value
  * If no, check if current value is larger than secondLargest
    * If yes, overwrite secondLargest with current value
* Return secondLargest

Note: many fellows may initialize both largest and secondLargest to the
first value in the array. This would be problematic if the array happens
to be sorted in descending order. A fellow can still be marked proficient
if the interviewer needs to point this out to them, as long as they can
modify their solution to account for it.

## Solution Code

```java
// Java
public static int getSecondLargest(int[] arr) {
    int largest = arr[1] > arr[0] ? arr[1] : arr[0];
    int secondLargest = arr[1] > arr[0] ? arr[0] : arr[1];

    for (int i = 2; i < arr.length; i++) {
      if (arr[i] > largest) {
          secondLargest = largest;
          largest = arr[i];
      } else if (arr[i] > secodLargest) {
          secodLargest = arr[i];
      }
    }

    return secodLargest;
}
```


```javascript
// Javascript
function getSecondLargest(arr) {
    var largest = arr[1] > arr[0] ? arr[1] : arr[0];
    var secondLargest = arr[1] > arr[0] ? arr[0] : arr[1];

    for (var i = 2; i < arr.length; i++) {
        if (arr[i] > largest) {
            secondLargest = largest;
            largest = arr[i];
        } else if (arr[i] > secondLargest) {
            secondLargest = arr[i];
        }
    }

    return secondLargest;
}
```
```swift
//Swift
func secondLargestLinear(in arr: [Int]) -> Int {
    var largest = Int.min
    var secondLargest = Int.min
    for num in arr {
        if num > largest {
            secondLargest = largest
            largest = num
        } else if num > secondLargest {
            secondLargest = num
        }
    }
    return secondLargest
}
```
