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
      return city   // Accessible because extension is in the same file.
    }
}

//Extension.swift
extension Location {
    func getCountry() -> String {
      return country   // Not accessible because extension is in a different file.
    }
}
```

In this example, `city` is accessible because the extension is in the same source file `(Location.swift)`, but `country` is not accessible because the extension is in a different file `(Extension.swift)`.

## fileprivate
Accessible anywhere within the same source file. Use `fileprivate` to enable access from other classes or structs in the same file while blocking it from outside that file.

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

