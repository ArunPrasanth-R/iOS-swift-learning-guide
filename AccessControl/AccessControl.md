## 🔐 Access Control

Access Control restricts the visibility of **types** **_(classes, structs, enums, protocols)_** and their **members** **_(stored/computed properties, methods, initializers, subscripts, extensions)_** across **files** and **modules**.

- __File__: A single `.swift` source file (eg: `UserService.swift`)
- __Module__: A module is a single, self-contained unit of code distribution, such as a framework or application that is compiled together and imported into other modules using the `import` keyword. (eg: `import UIKit`)

Swift access control system provides **five** access levels:

From most restrictive to least,
- `private`
- `fileprivate`
- `internal`
- `public`
- `open`

## private
Accessible only within the __enclosing declaration__ and it's __extension__ in the __same file__.

_Note: Best for strictly encapsulated details._

```
//Location.swift
swift

class Location {
    private var city: String
    private var country: String

    init(city: String, country: String) {
        self.city = city
        self.country = country
    }
}

extension Location {
    func getCity() -> String {
      return city   // ✅ Correct: Accessible because extension is in the same file.
    }
}

//Extension.swift
extension Location {
    func getCountry() -> String {
      return country   // ❌ Error: Not accessible because extension is in a different file.
    }
}
```

In this example, `city` is accessible because the extension is in the same source file `(Location.swift)`, but `country` is not accessible because the extension is in a different file `(Extension.swift)`.

## fileprivate
Accessible anywhere within the __same source file__. Use `fileprivate` to enable access from other classes or structs in the same file while blocking it from outside that file.

_Note: Best to hide implementation detail in a single source file._

```
//Location.swift
swift

class Location {
    fileprivate var city: String

    init(city: String, country: String) {
        self.city = city
        self.country = country
    }
}
```
In this example, `city` variable is accessible only inside `Location.swift` source file. We can't access `city` variable outside this source file.

## internal (default)
Accessible anywhere within the same module (target/framework), not from other modules. `internal` is the default access level, no need to specify the keyword.

_Note: Best to keep private to the target or framework_

```
swift

class Location {
    func getCities() -> [String] {
        return ["Coimbatore", "Appenzell", "Queenstown"]
    }
}
```
In this example, `Location` class and `getCities()` method are `internal` by default since no access modifier is specified. Hence it can be accessed within the same module not outside.

## public 
Accessible from __any module__, but __cannot__ be __subclassed__ or __overridden__ by external modules.

```
swift
//Module A
public class Location {
    public var city: String
    
    public init(city: String) {
        self.city = city
    }

    public func getCities() -> [String] {
        return ["Coimbatore", "Appenzell", "Queenstown"]
    }
}

//Module A
class Vacation: Location {
    var location = Location(city: "coimbatore")

    init() {
        print("City = \(location.city)")
    }

    override func getCities() -> [String] {
        return ["Coimbatore"]
    }
}

//Module B
import Location

class Vacation: Location { // ❌ Error: cannot be subclassed in outside module

    // ✅ Correct: instantiate and use (no subclassing)
    var location = Location(city: "coimbatore")

    init() {
        print("City = \(location.city)")  // ✅ Works
    }
    
    // ❌ Error: cannot be overridden in the outside module
    override func getCities() -> [String] { 
        return ["Coimbatore"]
    }

    func getMyCities() -> [String] {
        let cities = location.getCities()  // ✅ Call public method
        return [cities[0]]                
    }
}

```
In this example `Location` class can be accessed in both Module A and Module B, but cannot be subclassed or overridden in `Module B`. 

## open 
Accessible from __any module__ and can be __subclassed__ or __overridden__ by external modules. It is the __most permissive__ access level.

```
swift
//Module A
public class Location {
    public var city: String
    
    public init(city: String) {
        self.city = city
    }

    public func getCities() -> [String] {
        return ["Coimbatore", "Appenzell", "Queenstown"]
    }
}

//Module B
import Location

class Vacation: Location { // ✅ Correct: can be subclassed in outside module

    var location = Location(city: "coimbatore")

    init() {
        print("City = \(location.city)")  // ✅ Works
    }
    
    // ✅ Correct: can be overridden in the outside module
    override func getCities() -> [String] { 
        return ["Coimbatore"]
    }
}

```
In this example `Location` class can be accessed, subclassed, and overridden in an outside Module.
