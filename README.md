# Burpple Swift Style and Conventions Guide

This is Burpple's Swift Style and Conventions Guide.

The purposes of this document are

* to improve code readability 
* to have common rules in dev team

You can write flixible code using Swift, though, it's hard for team development to standardize and to improve readability. This is the reason why we are making this document. Of course as we are still improving and looking for good ways, if you have suggestion, let us know and open a pull request :)

## Contribution
This document is open to anyone who wants to contribute.

## Environment
Xcode 6.1.1, Swift 1.1

## Current Version
v0.1.0

## Rules

----
### Whitespace

#### Indent
Use tabs, instead of using spaces

#### Function, Method 
Place 1 space before the leading brace, the return value, the return arrow

```swift
// good
func hello() {
}

// good
func hello() -> String {
	return "hello"
}

// bad
func hello(){
}

// bad
func hello() ->String {
	return "hello"
}	
```

#### Variable/Constant declaration

Place 1 space after the colon

```swift
// good
let name: String

// bad
let name:String
```

#### Argument

Place 1 space after the comma

```swift
// good
func hello(name: String, message: String) {
}

// bad
func hello(name: String,message: String) {
}
```

#### Operator
Operator with 1 space

```swift
// good
let x = 1 + 1

// bad
let x=1+1
```

----
### Comment
#### #pragma mark
// MARK: - HelloWorld

---
### Variable, Constant

#### Declaration
When declaration is with right side value, you don't need to specify the type

```swift
// good
let message = "hello"

// bad
let message: String = "hello"
```

But if right side value is ambiguous, you should specify the type

```swift
// you can't tell the type of the right side value. CGFloat, Float, Double?
let value: CGFloat = 1.0
```

If right side value is return value which you can't tell the type explicitly, you should specify the type on the left side

```swift
let result: Bool = delegate.writeGreatCode()
```
	
But if return type is obvious, you don't need to specify the type on the left side

```swift
// it's obvious that return value is UIApplication's instance
let application = UIApplication.sharedApplication()
```

Also if use cast, you don't need to specify the type on the left side

```swift
// good
let movie = object as Movie

// bad
let movie: Movie = object as Movie
```

#### @IBOutlet
Use weak and unwrapped type to define IBOutlet

```swift
// good
@IBOutlet weak var headerView: UIView!

// bad
@IBOutlet weak var headerView: UIView?

// bad
@IBOutlet var headerView: UIView!
```

#### let vs var
If the value won't be changed afterwards, use let.

----
### String

#### String Format
Use Swift style

```swift
// good
"I am \(name)"

// bad
NSString(format: "I am %@", name)
```

#### String vs NSString
* String is Struct, NSString is Class
* Use Swift native type, which is String, whenever possible
* Convert from String to NSString when you want to use NSString method

```swift
("test" as NSString).XXXXXX
```

----
### Number
Use Swift native type, Int, UInt, Float etc, whenever possible

#### Float, CGFloat
When you need to use CGFloat, like when you make CGRect, convert Float to CGFloat

```swift
var f: Float = 10.0
CGRectMake(CGFloat(f), 0, 10, 10)
```

----
### Array
#### Array vs NSArray
* Array is Struct, NSArray is Class
* Use Swift native type, which is Array, whenever possible

#### Creating an Empty Array
Follow Apple official document

```swift
// good
var someInts = [Int]()

// bad
var someInts = Array<Int>()
```

#### Iterate
Use for-in style

```swift
// good
for value in array {
}

// bad
for var i = 0; i < array.count; i++ {
    let value = array[i]
}
```

----
### Dictionary
#### Dictionary vs NSDictionary
* Dictionary is Struct, NSDictionary is Class
* Use Swift native type, which is Dictionary, whenever possible

#### Creating an Empty Dictionary
Follow Apple official document

```swift
// good
var namesOfIntegers = [Int: String]()

// bad
var namesOfIntegers = Dictionary<Int, String>()
```

----
### Struct, Class, Enum
#### Value (struct and enum)
* Copied when passed as an argument to a function
* Copied when assigned to a different variable
* Immutable if assigned to a variable with let

#### Reference (class)
* Stored in the heap and reference counted automatically
* when passed as an argument, doesn't make a copy(just passing a pointer to same instance)

#### Which to use?
* Usually choose class over struct. struct tends to be more for fundamental types.

----
### Function
If return value is Void, you don't need to specify return type

```swift
// good
func doSomethingGreat() {
}

// bad
func doSomethingBad() -> () {
}
```

----
### Closure
If return value is Void, you don't need to specify return type

```swift
// good
var closure = { (value: String) in
    println(value)
}

// bad
var closure = { (value: String) -> () in
    println(value)
}
```

----
### self
If you access to a property or method, write "self" explicitly

```swift
// good
func doSomethingGreat() {
	self.doSomethingGreater()
}

// bad
func doSomethingGreat() {
	doSomethingGreater()
}
```

---
##Statements
### if
You don't need to write ()

```swift
// good
if x == 1 {
}

// bad
if (x == 1) {
}
```

### for
Use for-in style

```swift
// good
for value in array {
}

// good
for index in 1...5 {
}

// bad
for var i = 0; i < array.count; i++ {
}
```

----
### Protocols
Any functions that are expected to mutate the receiver should be marked mutating

```swift
protocol SomeProtocol : InheritedProtocol {
	mutating func changeIt()
}
```

---
### Property

#### Initial Value
When you declare property and set initial value, initialize it in init

```swift
// good
class Person {
  var age: Int
  init () {
    self.age = 20
  }
}

// bad
class Person {
    var age: Int = 20
}
```

#### Optional Type, Unwrapped Optional Type
If a property is initialised in init, you don't need to use Optional, Unwrapped Optional Type

```swift
// good
class Person {
  var name: String
  init () {
      self.name = "Swift"
  }
}

// bad
class Person {
  var name: String!
  init () {
    self.name = "Swift"
  }
}

// bad
class Person {
  var name: String?
  init () {
    self.name = "Swift"
  }
}
```

If a property initialised in loadView, viewDidLoad, awakeFromNib (setup methods), you can use unwrapped optional type

```swift
// good
class SwiftViewController: UIViewController {

  var name: String!

  override func viewDidLoad() {
  	self.name = "Swift"
	}
}

// bad
class SwiftViewController: UIViewController {

  var name: String?

  override func viewDidLoad() {
  	self.name = "Swift"
	}
}
```

---
### init

#### init
TODO: implementing...

#### convenience init
TODO: implementing...

---
### weak, unowned
TODO: implementing...

---
### Extension
As this feature is easily abused

* Extensions should be used to add clarity to readability
* Don't use this feature as a substitute for OO design

----
### Access Control
TODO: implementing...

---
### Log
TODO: implementing...

----
## Contributors
* [@akirahrkw](https://github.com/akirahrkw).

## History
[CHANGELOG](./CHANGELOG.md).

## TODO
* init
* convenience init
* weak, unowned
* Access Control
* Log
etc

## Reference

[The Swift Programming Language](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/)

[Developing iOS 8 Apps with Swift](https://itunes.apple.com/us/course/developing-ios-8-apps-swift/id961180099).

[Swiftコーディング規約@Wantedly](http://qiita.com/susieyy/items/f71435cc962e70d81b37)

[Collection Types](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/CollectionTypes.html)

[Working with Cocoa Data Types](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/BuildingCocoaApps/WorkingWithCocoaDataTypes.html)

[More Swift and Foundation Frameworks](https://itunes.apple.com/us/course/developing-ios-8-apps-swift/id961180099).

[Access Control](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/AccessControl.html#//apple_ref/doc/uid/TP40014097-CH41-ID3)
