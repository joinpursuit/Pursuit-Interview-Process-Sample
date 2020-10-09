# Adjacent Duplicates in String

https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string

## Prompt

Given a string `str`, a duplicate removal consists of choosing two adjacent and equal letters, and removing them.

We repeatedly make duplicate removals on S until we no longer can.

Return the final string after all such duplicate removals have been made.  It is guaranteed the answer is unique.

## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:

- Can the string be empty? _Yes, and you should return an empty string_
- Can removing duplicates bring two letters together that weren't duplicates? _Yes, you need to keep removing adjacent duplicates until no more remain_
- Are `"A"` and `"a"` duplicates? _The input string will only contain lowercase letters in the set [a-z]*_

## Sample Inputs and Outputs

### Example Two:

#### Input

```swift
let input = "bookkeeper"
```

#### Output

```swift
let expectedOutput = "bper"
```
#### Explanation

`"oo"`, `"kk"`, and `"ee"` are adjacent duplicates.  Removing any pair does not cause more duplicates to appear.

### Example Two:

#### Input

```swift
let input = "abbaca"
```

#### Output

```swift
let expectedOutput = "ca"
```
#### Explanation

"abbaca" -> "aaca" -> "ca"

## Hints

If a fellow has been stuck for several minutes, it's OK to offer a hint to keep things moving:

- Is there a data structure we could use to track and manipulate the end of a string that we're building?

## Solution Overview

1. Create a stack of characters.
1. Iterate of the input string.  If the current character is at the top of the stack, pop from the stack.  Otherwise, push the element to the stack.
1. Join the stack and return it.

## Solution Code

### Swift


```swift
func removeDuplicates(from str: String) -> String {
    guard !str.isEmpty else { return str }
    var stack = [Character]()
    for char in str {
        guard let topElement = stack.last, topElement == char else {
            stack.append(char)
            continue
        }
        stack.popLast()
    }
    return String(stack)
}
```

### JavaScript

```js
var removeDuplicates = function(str) {    
    let stack = []
    for (let i = 0; i < str.length; i++) {
        if (stack[stack.length - 1] === str[i]) {
            stack.pop()
        } else {
            stack.push(str[i])
        }
    }
    return stack.join('')
};
```
