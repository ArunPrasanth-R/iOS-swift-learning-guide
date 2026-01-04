## Possible interview question in Swift Functions

### __1.  What is the difference between an Argument Label and a Parameter Name?__

The **Argument Label** is used when calling the function to make it read like a sentence (e.g., to: in greet(to: "Arun")). The **Parameter Name** is used inside the function body to refer to the value. You can use _ to omit the argument label.

### __2. Explain the difference between map and compactMap__

Both transform elements in a collection. However, **map** returns an array of the same length (even if some results are **nil**), whereas **compactMap** automatically removes any **nil** values and **unwraps the optionals**, returning a flattened array of non-nil values.

### __3. What are "First-Class Functions" in Swift?__

It means functions are treated like any other type. You can **assign a function** to a variable, **pass a function** as an argument to another function (higher-order functions), or **return a function from another function**.

### __4. Why use guard instead of if inside a function?__

__guard__ is an "early exit." It checks a requirement at the top and quits immediately if it's not met, keeping the rest of your code clean.

```swift
swift

func submit(name: String) {
    guard !name.isEmpty else { 
        return  // Stop here if empty
    } 
    print("Saving \(name)...")
}
```

### __5. How do you handle code that might fail?__

Mark the function with __throws__. The caller must then use try to handle potential errors.

```swift

swift
func check(id: Int) throws {
    if id == 0 { 
        throw MyError.invalid 
    }
}

try? check(id: 0) // Returns 'nil' if it fails, instead of crashing
```
### __6. How do you modify a value passed into a function (inout parameters)?__

By default parameters are constants. To change them, you use the __`inout`__ keyword. When calling the function, you must pass the variable with an __`ampersand (&)`__.

```swift

swift

func increment(_ value: inout Int) {
    value += 1
}

var score = 10
increment(&score) // score is now 1
```
