Harver iOS Exercise
============================

## Get started

Copy below code to https://repl.it/languages/swift and modify the code to complete the assesment tasks as below. Once you completed click on share to share a link to the assesment.

```

import Foundation

let words = ["start", "citizen", "flour", "circle", "petty", "neck", "seem", "lake", "page", "color", "ceiling", "angle", "agent", "mild", "touch", "bite", "cause", "finance", "greet", "eat", "minor", "echo", "aviation", "baby", "role", "surround", "incapable", "refuse", "reliable", "imperial", "outer", "liability", "struggle", "harsh", "coerce", "front", "strike", "rage", "casualty", "artist", "ex", "transaction", "parking", "plug", "formulate", "press", "kettle", "export", "hiccup", "stem", "exception", "report", "central", "cancer", "volunteer", "professional", "teacher", "relax", "trip", "fountain", "effect", "news", "mark", "romantic", "policy", "contemporary", "conglomerate", "cotton", "happen", "contempt", "joystick", "champagne", "vegetation", "bat", "cylinder", "classify", "even", "surgeon", "slip", "private", "fox", "gravity", "aspect", "hypnothize", "generate", "miserable", "breakin", "love", "chest", "split", "coach", "pound", "sharp", "battery", "cheap", "corpse", "hobby", "mature", "attractive", "rock"]


extension Collection where Indices.Iterator.Element == Index {
    subscript (safe index: Index) -> Iterator.Element? {
        return indices.contains(index) ? self[index] : nil
    }
}

func getRandomWordSync() -> String {
    let index = randomInRange(min: 0, max: 100)
    let word = words[index]
    return word
}

func getRandomWord(slow: Bool = false, completion:@escaping(_ word: String?, _ error: String?)->()) {
    let index = randomInRange(min: 0, max: 200)
    guard let word = words[safe: index] else {
      return completion(nil, "Fatal error: Index out of range")
    }
    
    let delay = slow ? 500.0 : 0.0
    
    DispatchQueue.main.asyncAfter(deadline: .now() + delay) {
        completion(word, nil)
    }
}

func randomInRange(min: Int, max: Int) -> Int {
    return Int.random(in: min ..< max)
}

```

## Tasks

Complete these tasks in order. If you can't complete a task, just proceed with the next one.

1. Print numbers from 1 to 100 to the console, but for each number also print a random word using the function `getRandomWordSync`. E.g.

```
1: four
2: firm
3: shape
4: choice
5: coach
6: purple
...
100: buffalo
```

2. Modify your code to be a "Fizz Buzz" program. That is, print the numbers as in the previous step, but
for multiples of three, print "Fizz" (instead of the random word), for multiples of five, print "Buzz" and
for numbers which are both multiples of three and five, print "FizzBuzz".

3. Create a version of steps *1* and *2* using the **asynchronous** function, `getRandomWord`. This function
returns a Promise, which resolves to a random word string.

4. Add error handling to both the synchronous and asynchronous solutions (calling `getRandomWord()` will throw an error instead of returning a random word). When an error is caught, the programm should print "It shouldn't break anything!" instead of the random word, "Fizz", "Buzz" or "FizzBuzz"

5. Instead of printing the console. Write the information to a file in the root of this project.

6. send your result to an HTTP endpoint (since there is no running endpoint, this
part of your solution does not need to actually run)

**Bonus:**
* The numbers should be printed in ascending order.
* Imagine `getRandomWord`'s implementation is slow and takes 500ms to complete (call `getRandomWord({ slow: true })` to emulate this). Can you make your solution run in less than 1000ms with the `slow` option turned on?
