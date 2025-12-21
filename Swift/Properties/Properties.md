## Properties in Swift

Properties are **variables** or **constants** associated with a particular type — usually a class, structure, or enumeration. They store values or provide a way to compute values relevant to that type..

Swift properties come in two main categories, 
 - **`stored properties`**, and 
 - **`computed properties`**. 
    
Additionally, for more advanced use cases Swift supports, 
- **`property observers`**, 
- **`lazy properties`**, 
- **`type properties`**, and 
- **`property wrappers`**.


## 🧱 Stored Properties

A stored property is a **`constant`** or **`variable`** stored as part of an instance.


```
swift

struct Person {
    var name: String                // Read-write stored property
    let birthYear: Int              // Read-only stored property
}

var person = Person(name: "Arun", birthYear: 1991)

person.name = "Prasanth"           // Can be modified
// person.birthYear = 2000         ❌ Error: birthYear is a constant
```

If we create an instance using a  **`let`**  constant, we **can’t modify** any variable properties inside it because both struct and its properties are immutable.

## ⚙️ Computed Properties

A computed property **doesn’t store** a value directly. Instead, it provides a **getter** and an **optional setter** to **calculate values dynamically**.

```
swift

struct Rectangle {
    var width: Double
    var height: Double
    
    var area: Double {
        get {
            width * height
        }
        set {
            height = newValue / width
        }
    }
}

var rect = Rectangle(width: 10, height: 5)
print(rect.area)       // 50.0
rect.area = 100
print(rect.height)     // 10.0


```

## 💤 Lazy Stored Properties

A lazy property **delays its initialization** until the first time it’s accessed. This is useful when the property’s value depends on external factors or is expensive to create.

```
swift

class DataManager {
    lazy var data = loadData()
    
    func loadData() -> [String] {
        print("Loading data...")
        return ["Item1", "Item2", "Item3"]
    }
}

let manager = DataManager()
print(manager.data)         // Triggers 'loadData()' only now
```
⚠️ **Lazy properties** must always be declared with  **var** , since their values might not exist until after initialization.


**_Note:_** 

_Why **lazy property** is **not** a **computed property**?_

Lazy properties compute and store a value only on first access, while computed properties **recalculate every time**.

## 🔍 Property Observers
 
Property observers let you respond to changes in a property’s value. Swift provides two observer blocks:
- **`willSet`**  — called right before the value changes
- **`didSet`**  — called right after the value changes

```
swift

class StepCounter {
    var steps: Int = 0 {
        willSet {
            print("About to set steps to \(newValue)")
        }
        didSet {
            print("Added \(steps - oldValue) steps")
        }
    }
}

let counter = StepCounter()
counter.steps = 100
counter.steps = 150
```

## 🧮 Type Properties 

Type properties belong to the **type itself**, not to any particular instance. They are defined using  **`static`** for **structs** and **enums**, or  **`class`**  for **classes** (if overriding is needed).

```
swift

struct Configuration {
    static let defaultTimeout = 30
    static var maxConnections = 5
}

print(Configuration.defaultTimeout)
Configuration.maxConnections = 10
```

## 🎁 Property Wrappers

Property wrappers provide a reusable mechanism to add extra functionality around property storage — like validation, formatting, or persistent storage.

```
swift

@propertyWrapper
struct Capitalized {
    private var value: String = ""
    
    var wrappedValue: String {
        get { value }
        set { value = newValue.prefix(1).uppercased() + newValue.dropFirst() }
    }
}

struct User {
    @Capitalized var name: String
}

var user = User()
user.name = "arun prasanth"
print(user.name) // "Arun prasanth"
```

In the above example, the wrapper handles capitalization without manual processing in the setter.

## Quick Comparison Table

| Property Type        | Stores Value    | Can be computed?  | Observers | Lazy  | Type Scope |
|----------------------|-----------------|-------------------|-----------|-------|------------|
| `Stored Property`    | ✅ Yes          | ❌ No             |✅ Yes    | ✅ Yes | Instance
| `Computed Property`  | ❌ No           | ✅ Yes            |❌ No     | ❌ No  | Instance
| `Lazy Property`      | ✅ Yes          | ❌ No             |✅ Yes    | ✅ Yes | Instance
| `Type Property`      | ✅ Yes          | ✅ Yes            |❌ No     | ❌ No  | Type-level



## 🧠 Key Takeaways

- Use **`stored properties`** for **direct storage**.
- Use **`computed properties`** to derive **data dynamically**.
- Use **`lazy properties`** to **delay initialization**.
- Use **`property observers`** to **track value changes**.
- Use **`type properties`** when **shared across all instances**.
- Use **`property wrappers`** to **encapsulate custom logic**.


