# Functions in Swift

**A function is a self-contained block of code that performs a specific task.** 

In Swift, functions are first-class citizens, meaning they can be,
- passed as arguments,
- returned from other functions, and 
- assigned to variables.

## 1. Basic Function Syntax
Every function starts with the **`func`** keyword, followed by its name, parameters in parentheses, and the return type after the **`->`** symbol.

```swift
swift

func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}

print(greet(person: "Arun")) // Output: "Hello, Arun!"
```

## 2. Argument Labels and Parameter Names
Swift functions have two names for each parameter:
- **Argument Label:** Used when calling the function.
- **Parameter Name:** Used inside the body of the function.

```swift
swift

func sayHello(to person: String, from hometown: String) -> String {
    return "Hello \(person)! Glad you could visit from \(hometown)."
}

// 'to' and 'from' are argument labels
print(sayHello(to: "Arun", from: "Coimbatore"))
```

### Omitting Argument Labels
Use an underscore **_** if you don't want a label when calling the function.

```swift
swift

func multiply(_ number1: Int, by number2: Int) -> Int {
    return number1 * number2
}

print(multiply(5, by: 4)) // Output: 20
```

## 3. Return Values

### Functions without Return Values
If a function doesn't return a value, you can omit the -> symbol.

```swift
swift

func printMessage() {
    print("This function returns nothing.")
}
```

### Functions with Multiple Return Values (Tuples)
You can return multiple values at once by using a **Tuple**.

```swift
swift

func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var curMin = scores[0]
    var curMax = scores[0]
    var curSum = 0
    
    for score in scores {
        if score > curMax { curMax = score }
        else if score < curMin { curMin = score }
        curSum += score
    }
    
    return (curMin, curMax, curSum)
}

let stats = calculateStatistics(scores: [5, 3, 100, 3, 9])
print("Max is \(stats.max), Sum is \(stats.sum)")

```

## 4. Advanced Parameters

### Default Parameter Values
You can provide a default value for any parameter.

```swift
swift

func displayPower(value: Int, power: Int = 2) {
    print("Result: \(value * power)")
}

displayPower(value: 10)          // Uses default: 20
displayPower(value: 10, power: 3) // Uses provided: 30
```

### Variadic Parameters
A variadic parameter accepts zero or more values of a specified type.

```swift
swift

func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}

print(arithmeticMean(1, 2, 3, 4, 5)) // Output: 3.0
```

### In-Out Parameters (inout)

By default, function parameters are constants. To modify a variable passed to a function, use the **inout** keyword.

```swift
swift

func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var x = 3
var y = 107
swapTwoInts(&x, &y) // Note the ampersand (&)
print("x is now \(x), y is now \(y)")
```

## 5. Function Types
Functions have types, just like Int or String. You can store functions in variables.

```swift
swift

func addTwoInts(_ a: Int, _ b: Int) -> Int { return a + b }

var mathFunction: (Int, Int) -> Int = addTwoInts
print("Result: \(mathFunction(2, 3))")
```

## 6. Functional Programming Basics

Swift arrays provide high-level functions that take closures (anonymous functions) to transform data.


| Function | Purpose | 
| --- | --- |
| map | Transforms every element in an array. |
| compactMap | Transforms elements and removes nil values. |
| flatMap | Flattens a nested array into a single array. |
| filter | Returns only elements that satisfy a condition. |
| reduce | Combines all elements into a single value. |

```swift
swift

let numbers = [1, 2, 3, 4, 5]

// Map: Square all numbers
let squares = numbers.map { $0 * $0 } // [1, 4, 9, 16, 25]

// Filter: Get even numbers
let evens = numbers.filter { $0 % 2 == 0 } // [2, 4]

// Reduce: Sum all numbers
let total = numbers.reduce(0, +) // 15
```

### 7. Swift 6: Modern Concurrency (async/await)

Functions that perform **long-running tasks** (like API calls) use **async**.

```swift
swift

func fetchUserData() async throws -> Data {
    let url = URL(string: "https://api.example.com/user")!
    let (data, _) = try await URLSession.shared.data(from: url)
    return data
}
```

### Key Takeaways for iOS Developers
1. **Readability:** Use argument labels to make function calls read like English sentences.
2. **Safety:** Use guard inside functions to exit early if requirements aren't met.
3. **Efficiency:** Use inout carefully to avoid unnecessary object copying for large structs.
4. **Modernity:** Favor map, filter, and reduce over manual for loops for data transformation.

