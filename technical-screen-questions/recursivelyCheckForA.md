# Recursively Check for "A"


## Prompt

Write a *recursive* function that determines whether or not an input
String contains the letter 'a'.


## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:
* Should the return type be a boolean? _Yes_
* Could the input String ever be null or empty? _Yes; in that case return false_
* Does case matter? _No, treat 'a' and 'A' as equivalent_
* Do I really have to use recursion? _Yep!_


## Sample Inputs & Outputs

| Input | Output |
|---|---|
| "Hello, World!" | false |
| "abcd" | true |
| "DBCA" | true |
| "" | false |


## Hints

If a fellow has been stuck for several minutes,
it's OK to offer a hint to keep things moving:
* If they really don't know where to begin, ask them what would be the base case, a.k.a. the situation where they don't want to make any more recursive calls (i.e. if input String is null or empty)
* If they are struggling with the induction step, ask how we might "break off" one character from the rest of the string to check if it's an 'a' (i.e. use `str[0]` to get first character and `str.substr(1)` to get the rest of the string)
* It will be tricky to realize that the check of whether the first character is 'a' and the recursive call with the rest of the string should be connected with a **logical or**. If need be, remind them we only need to check one character in the induction step; all the rest can be left to the recursive call.


## Solution Overview

General steps:
* If the input string is null or empty, return false
* Otherwise, return true if the first character of the String is 'a' (or 'A'), **or** if the rest of the String contains an 'a' (recursive call w/ rest of string)

## Solution Code

```java
// Java
public static boolean checkForA(String str) {
  if (str == null || str.length() == 0) {
      return false;
  }

  return (Character.toLowerCase(str.charAt(0)) == 'a') ||
          checkForA(str.substring(1));
}
```


```javascript
// Javascript
function checkForA(str) {
    if (str === null || str.length === 0) {
        return false;
    }

    return (str[0].toLowerCase() === 'a') || checkForA(str.substr(1));
}
```

```swift
//Swift
func containsA(str: String) -> Bool {
    guard !str.isEmpty else { return false }
    return String(str.last!).lowercased() == "a" || containsA(str: String(str.prefix(str.count - 1)))
}
```
