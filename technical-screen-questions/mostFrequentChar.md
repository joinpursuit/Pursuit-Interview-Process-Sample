# Most Frequent Character


## Prompt

Write a function that accepts a String as input and returns
the character that appears most frequently in that String.


## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:
* Could the input String ever be null? _Yes_
* What should be returned if input is null? _Return null_
* What should be returned if input is an empty string? _Return an empty string_
* Do spaces count? _No; ignore spaces_
* Do punctuation or digits count? _Yes; consider them like like you would letters_
* Does case matter? _No, "a" should be treated as equivalent to "A"_
* What if two or more characters "tie" as the most frequently occurring? _Return whichever one appears first in the input String_

## Sample Inputs & Outputs

* `mostFrequentChar("Hello World!")` returns `'l'`
* `mostFrequentChar("abacaba")` returns `'a'`
* `mostFrequentChar("xyyXzz")` returns `'x'` _(not y)_
* `mostFrequentChar("")` returns `''`
* `mostFrequentChar("a b a b a")` returns `'a'` _(not space)_

## Hints

If a fellow has been stuck for several minutes,
it's OK to offer a hint to keep things moving:
* If they really don't know where to begin, ask how they might be able to look at each character in the string one at a time. (i.e. iterate over it with a loop)
* If they don't know what to do inside the loop, ask what it is that we want to to with each character (i.e. keep a running count of how often it appears)
* If they're stuck trying to use a single temp variable to hold the counts for multiple characters, ask if there is a data structure they can use to keep track of multiple counts (i.e. map/hashmap/dictionary)

## Solution Overview

General steps:
* Declare an empty hashmap or dictionary
* Iterate through the characters of the input String with a loop
* For each character check if it is a key in the map
  * If no, add the char as a key with value 1 (but not if it's a space!)
  * If yes, increment the value associated with that char by 1
* Declare a variable to hold the most frequent character
* Iterate through the input String again
* For each character, check if it's value in the map is higher than the value associated with the current value of the most frequent character variable
  * If yes, update the most frequent character variable to be the current character
* Return the most frequent character

Note: many fellows may iterate through the keys of the map,
rather than iterate over the input String a second time.
This approach would not guarantee that in the case of a tie the character
appearing _first_ in the input String would be returned.
This is an edge case though, and should not necessarily result in
the fellow being marked as less than proficient.

## Solution Code

```java
// Java
public static char getMostFrequentChar(String str) {
    Map<Character, Integer> counts = new HashMap<>();

    for (int i = 0; i < str.length(); i++) {
        char c = Character.toLowerCase(str.charAt(i));
        if (counts.containsKey(c)) {
            counts.put(c, count.get(c) + 1);
        } else {
            counts.put(c, 1);
        }
    }

    char mostFreqChar = str.charAt(0);

    for (int i = 0; i < str.length(); i++) {
        if (counts.get(Character.toLowerCase(str.charAt(i))) >
            counts.get(Character.toLowerCase(mostFreqChar))) {
            mostFreqChar = str.charAt(i);
        }   
    }

    return mostFreqChar;
}
```


```javascript
// Javascript
function getMostFrequentChar(str) {
    var counts = {};

    for (var i = 0; i < str.length; i++) {

        var char = str[i].toLowerCase();

        if (counts[char]) {
            counts[char]++;
        } else if (char !== ' ') {
            counts[char] = 1;
        }
    }

    var mostFreqChar = str[0];

    for (i = 0; i < str.length; i++) {
        if (counts[str[i].toLowerCase()] >
              counts[mostFreqChar.toLowerCase()]) {
            mostFreqChar = str[i];
        }
    }

    return mostFreqChar;
}
```

```swift
//Swift
func mostFrequentlyOccurringChar(in str: String) -> Character? {
    guard str.count > 0 else { return nil }
    let str = str.lowercased().filter{$0 != " "}
    var frequencyDict = [Character: Int]()
    var firstAppearanceDict = [Character: Int]()
    for (i,c) in str.enumerated() {
        frequencyDict[c] = frequencyDict[c, default: 0] + 1
        if firstAppearanceDict[c] == nil {
            firstAppearanceDict[c] = i
        }
    }
    var max = (char: "", occurrences: 0)
    for (char, count) in frequencyDict {
        if count > max.occurrences || (count == max.occurrences &&
                                       firstAppearanceDict[char]! < firstAppearanceDict[Character(max.char)]!) {
            max = (String(char), count)
        }
    }
    return Character(max.char)
}
```
