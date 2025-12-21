## Possible interview question in Swift Properties

### __1. What are the differences between stored and computed properties?__

Stored properties hold actual values in memory, while computed properties calculate values dynamically on access without storage.

__Key Differences:__

**Stored properties**
- They store and retrieve values directly
- They are declared with a specific type and can have initial values assigned to them.
- They can be variable (`var`) or constant (`let`), depending on whether their value can be modified after initialization.

```
struct Rectangle {
    var width: Double
    var height: Double
}
```

**Computed properties**
- They do not store values directly but provide a getter and an optional setter to compute (or calculate) the value dynamically.
- They are declared with a type, but they do not store any value themselves. Instead, they provide a mechanism to retrieve and set values based on computations.
- They are always declared with `var`, as they are inherently variable.

```
struct Rectangle {
    var width: Double
    var height: Double
    var area: Double {  
        // Computed
        width * height
    }

    var perimeter: Double {  
        // Computed
        2 * (width + height)
    }
}
```

### __2. What is lazy initialization and discuss the pros and cons of using it?__

Lazy initialization in Swift defers property computation until first access using the __lazy__ keyword. It stores the result after initial computation for subsequent fast access.

**Pros**
- **Performance optimization:** Avoids expensive setup during instance initialization, ideal for resource-heavy objects like network calls or large data structures.
- **Cleaner initializers:** Defers properties dependent on other instance values post-init.
- **Memory efficiency:** Prevents allocation of rarely used objects.

**Cons**
- **Runtime overhead:** First access incurs branch checks and computation cost every time until initialized.
- **Not thread-safe:** Concurrent access from multiple threads can cause race conditions or multiple initializations.
- **Mutability required:** Must be  var , not  let , reducing immutability guarantees.
- **Debugging challenges:** Hides expensive operations, delaying performance issues to unpredictable runtime moments.

**_Tip: Use judiciously for truly expensive operations, not as default._**

