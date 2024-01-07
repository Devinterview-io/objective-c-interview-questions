# 55 Essential Objective-C Interview Questions

<div>
<p align="center">
<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

#### You can also find all 55 answers here 👉 [Devinterview.io - Objective-C](https://devinterview.io/questions/web-and-mobile-development/objective-c-interview-questions)

<br>

## 1. Describe the basic structure of an _Objective-C_ class.

In **Objective-C**, classes and objects serve as the backbone for software structure. A class typically consists of **interface** and **implementation** sections.

### Interface

The class interface lists the properties and methods that are accessible to other classes, essentially acting as a public API.

Here is the Objective-C code:

```objective-c
@interface MyClass : NSObject

@property NSString *name;

- (void)someMethod;

@end
```

It begins with `@interface`, the class identifier (`MyClass`), and a base class (usually `NSObject`). The list following `@interface` comprises **Instance Variables** (if any), **Properties**, and **Method Declarations** (optional) visible to other classes.

### Properties

Properties define attributes accessed via getter and setter methods, offering a more controlled means of manipulating an object's state. Attributes like atomicity, memory management, and runtime behavior can be specified.

Here is the Objective-C code:

```objective-c
@interface MyClass : NSObject

@property (atomic, strong) NSString *name;

- (void)someMethod;

@end
```

The simplified form of a property in Objective-C would look like this:

```objective-c
@property NSString *name;
```

**Note**: Custom getter and setter methods can be defined for additional control.

### Methods

Method declarations specify the class's behavior. They may be singleton methods (denoted by a `+` symbol) or instance methods (denoted by a `-` symbol).

Here is the Objective-C code:

```objective-c
@interface MyClass : NSObject

- (void)methodOne;
- (NSInteger)methodReturningIntegerWithParameter:(NSString *)param;

+ (void)classMethodOne;

@end
```

### Instance Variables

In modern Objective-C, it's a best practice to directly access the instance variables via property accessors, as shown below:

```objective-c
@implementation MyClass
{
    NSString *_internalName;
}

- (void)setInternalName(NSString *)name {
    _internalName = name;
}
- (NSString *)internalName {
    return _internalName;
}
@end
```

However, in older Objective-C code, the explicit declaration was used as shown here:

```objective-c
@interface MyClass : NSObject
{
    NSString *_internalName;
}
@end
```

### Implementation

The `@implementation` section describes how class methods and instance methods are defined.

Here is the Objective-C code:

```objective-c
@implementation MyClass

- (void)someMethod {
    // Implementation here
}

+ (void)classMethodOne {
    // Class method implementation here
}

@end
```

The `@implementation` section is typically followed by method definitions, along with any additional internal methods that are not part of the interface.
<br>

## 2. How do you define and implement a _method_ in _Objective-C_?

In Objective-C, a **method** is a function that's called on an object. It consists of a **signature** and an **implementation**. Here, a signature conventionally starts with a return type enclosed in parentheses, followed by the method name and argument list.

### Method Signature

A method's signature typically looks like this:

```objc
- (void)doSomething:(NSInteger)withValue withData:(NSString *)data;
```

Here's what each component means:

- **Return Type**: Denotes the method's return value. Use "void" for methods that don't return anything.
  
- **Method Name**: Describes the action the method performs. Objective-C methods focus on readability, often using a "verb-adverb" pattern.

- **Parameter List**: Uses individual, descriptive parameter names. Each parameter, with its own data type, is separated by a defined keyword for better readability.

### Code Example: Method Signature

```objc
- (void)submitOrderForProduct:(NSString *)productName withQuantity:(NSInteger)quantity;
```

### Reimagined Signature

Function: submitOrderForProduct
input: productName (NSString), quantity (NSInteger)
output: None



### Method Implementation

The method's actual functionality is defined in its **implementation**, encompassed within curly braces. At a minimum, the method's signature should be declared in the `.h` header file, and the complete method, including the curly brace implementation, should be available in the `.m` implementation file. However, modern, Xcode-configured projects generally provide a `-Swift.h` bridging header that collates these details.

### Code Example: Method with Signature and Implementation

**Header File** (.h):

```objc
- (void)submitOrderForProduct: (NSString *)productName withQuantity:(NSInteger)quantity;
```

**Implementation File** (.m):

```objc
- (void)submitOrderForProduct:(NSString *)productName withQuantity:(NSInteger)quantity {
    if (productName && quantity > 0) {
        // Process the order
    }
}
```
<br>

## 3. What are the built-in _data types_ available in _Objective-C_?

**Objective-C** data types are often classified under standard C types with the added object-oriented extension known as **Foundation data types**.

While the former primarily work with primitive values, the latter allows for object-oriented functionalities, such as reference counting.

### C Scalar Types

- **int, float, double**
- **char** for characters
- **_Bool** for Boolean values
- **void** for absence of type or value

These types are used mainly in setting up collections, such as **`NSArray`** and **`NSDictionary`**.

### Standard C Library Types

Objective-C, being a superset of C, naturally inherits the C data types:

- **Basic Types**: char, int, float, double
- **Modifiers**: short, long, signed, unsigned
- **Others**: intptr_t, uintptr_t, size_t

### **Foundation Data Types**

These Objective-C objects, defined in the Foundation framework, are encapsulated versions of C data types:

- **NSNumber**: Object representation of numeric scalar values.
- **NSDate**: Represents a point in time. Uses a time interval which is defined as the number of seconds since 1970.
- **NSValue**: Wrapper object for C scalars, structs, and pointers.
- **NSString**: A sequence of Unicode characters.
- **NSArray**: Ordered collection of objects.
- **NSDictionary**: Collection of key-value pairs.
<br>

## 4. How do you work with _NSString_, and how is it different from a _C-style string_?

While both **NSString** and **C-style strings** serve for text manipulation, using `NSString` provides several advantages like dynamic memory management, Unicode support, and methods for common manipulations.

### NSString Basics

- **Initialization**: Strings can be initiated in several ways, such as `stringWithFormat` or `stringWithContentsOfFile`, and even from C-string literals.

- **Memory Management**: Unlike C-style strings needing manual memory allocation/deallocation, `NSString`'s memory management is automatic under ARC. For version control without ARC, use the `retain` or `release` model.

### Key Distinctions

- **Memory Management**: C-style strings require manual management, whereas `NSString` manages memory dynamically.

- **Null-Termination**: C-style strings mandate a '\0' termination, while NSString does not rely on null-termination.

- **Data Encapsulation**: C-style strings expose pointers to their data, allowing direct manipulation. In contrast, `NSStrings` encapsulate their data, promoting better data integrity and security.

- **Unicode Support**: `NSString` fully supports unicode out of the box. C-style strings may do so depending on the platform, compiler configuration, and the use of wide-character types like `wchar_t`.

### Example: Using NSString and C-style Strings

Here is the Objective-C code:

```objc
NSString *str = @"This is an NSString";
NSString *str2 = [NSString stringWithFormat:@"Integer value: %d", 22];

const char *cStr = "This is a C-string";
char cStrBuffer[50] = "";
strncpy(cStrBuffer, cStr, sizeof(cStrBuffer) - 1);
```
<br>

## 5. Explain the difference between a _class method_ and an _instance method_.

Let's start by defining class and instance methods and then delve into their differences.

### Core Distinctions

#### Class-Specific Behavior

   Class Method: Operates on class-level attributes and doesn't require instantiation. It is commonly used for **factory methods** or other utility functions.

   Instance Method: Pertains to an object's state and behavior. It is characteristic of the class and is utilized to manipulate object-specific properties.

#### Invocation Style

   Class Method: Invoked on the class itself, for example: `[MyClass myClassMethod]`.

   Instance Method: Invoked on an instantiated object using a dot notation, like `MyClass *object = [[MyClass alloc] init]; [object instanceMethod]`.

### Code Example: Class Methods and Instance Methods

Here is the Objective-C code:

```objective-c
// MyClass.h
@interface MyClass : NSObject
@property NSString *name;
- (instancetype)initWithName:(NSString *)name;
+ (void)announce; // class method
- (void)sayHello;  // instance method
@end

// MyClass.m
@implementation MyClass
- (instancetype)initWithName:(NSString *)name {
    self = [super init];
    if (self) {
        self.name = name;
    }
    return self;
}
+ (void)announce {
    NSLog(@"I'm a class method");
}
- (void)sayHello {
    NSLog(@"Hello, %@", self.name);
}
@end

// main.m
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        [MyClass announce];  // Invoking 'announce' as a class method
        MyClass *m = [[MyClass alloc] initWithName:@"Instance Method Example"];
        [m sayHello];  // Invoking 'sayHello' as an instance method
    }
    return 0;
}
```
<br>

## 6. Describe the use of _pointers_ in _Objective-C_.

In **Objective-C**, **pointers** are fundamental to many language features including **reference** and **dynamic memory allocation**. ***Selectors*** serve as pointers to methods, and **Block Objects** manage and manipulate blocks of code, often backed by pointers.

### Pointer Arithmetic in Objective-C

Both C and Objective-C support **pointer arithmetic**, which uses offsets to navigate data structures efficiently.

For example, in the code:

```objective-c
int array[5] = {0, 1, 2, 3, 4};
int *pointer = &array[0];
NSLog(@"Value: %d", *(pointer + 2));
```
the pointer is adjusted by 2 elements and dereferenced, outputting `2` to the console.

### Notable Patterns in Objective-C and Pointers

- **[Memory Storage]**: In Objective-C, pointers are employed for dynamic memory allocation with `alloc`, while primitives and objects are stored in a heap or stack memory.
  
- **[Function Parameters]**: Methods in Objective-C are designed to work with pointers to pass large objects efficiently. Modern Objective-C, however, generally uses **ARC** for memory management, lessening the need for manual pointer use.
<br>

## 7. What is a _property_ in _Objective-C_, and how do you use the `@synthesize` _directive_?

In **Objective-C**, a **property** provides a simple way to access and modify object attributes, known as **instance variables**.

### Components of a Property

- **Atomicity**: Protects from simultaneous access during multi-threading.
- **Readability**: Defines if the getter method is accessible.
- **Writeability**: Establishes access to the setter method.
- **Ownership**: Specifies memory management rules for the associated object.

### Syntax

A property is declared within `@interface` or `@protocol` using the `@property` keyword. The corresponding getter and setter methods can be custom-defined.

#### Objective-C Code Example

Here is the Objective-C code:

```objective-c
@interface MyClass : NSObject

@property (atomic, getter=isFlagged, strong) NSNumber *flag;

@end
```

Here are the corresponding keywords:

- **Atomicity**: 'atomic'
- **Readability**: 'getter=isFlagged'
- **Ownership**: 'strong'


### Using  `@synthesize`

Before Xcode 4.4, **properties** required their **instance variables** to explicit in your class implementation. This involved using `@synthesize` to create automated **getter** and **setter** methods.


#### Generates Automatic Accessor Methods

The `@synthesize` directive enables automatic generation of **instance variables** and corresponding accessor methods.

- **Getters**: Automatically named after the property. For instance, if the property is `flag`, the getter becomes `flag`.
- **Setters**: Follow a similar naming convention. For example, `setFlag`.

#### Simplifies Property Management

By allowing the compiler to handle variable and method creation, `@synthesize` significantly streamlines property management.

### Modern Syntax and Optimizations

Starting from Xcode 4.4, the **modern Objective-C** uses **Automatic Reference Counting (ARC)**. This feature provides automatic memory management for objects, reducing manual interventions and potential memory leaks.

#### Objective-C Code Example

Here is the Objective-C code:

```objective-c
#import <Foundation/Foundation.h>

@interface MyClass : NSObject
@property BOOL flag;
@end

@implementation MyClass
@synthesize flag;
@end
```

#### Post-Xcode 4.4

If you are using Xcode 4.4 or later, **you don't need to explicitly use `@synthesize`**. The compiler takes care of it for you.
<br>

## 8. How do you declare and use a _block_ in _Objective-C_?

In Objective-C, a **Block** is a mechanism to define and encapsulate executable code created inline. It has similar benefits to C function pointers and can capture surrounding state.

### Declaring a Block

A block is defined within curly braces `{}` followed by a caret `^` symbol. This indicates that it's a block of code rather than a traditional function or method.

Here is the syntax:

```objective-c
returnType (^blockName) (parameter1Type, parameter2Type, ...);
```

### Example: Declaring a Block

```objective-c
void (^simpleBlock) (void);
int (^multiplyTwoValues) (int, int);
```

### Block Types

In Objective-C, blocks can be of two types:

- **Stack-based blocks**: These are local and exist on the stack. When the function or method call terminates, the block ceases to exist.
  
- **Heap-based or Global blocks**: These are dynamically created and can be assigned to a `strong` property to extend their lifespan beyond the scope where they were created.

### Operation Modes

Blocks can have multiple operation modes, determined by how they access the encapsulated variables. Modes include:

- **\_\_block**: Variables are passed by reference so that changes inside the block reflect outside.
  
- **\_\_weak** or **\_\_unsafe_unretained**: To mitigate strong retain cycles in the context of strong reference cycles between objects and blocks.

### Using a Block

You can invoke a block like a function. If the block has parameters, they are provided in brackets after the block's name.

Here is the Invocation Syntax:

```objective-c
blockName(parameter1, parameter2);
```

### Example: Using a Block

```objective-c
void(^simpleBlock)(void) = ^{
    NSLog(@"This is a simple block");
};

simpleBlock();
```

### Typedef for Readability

To simplify and enhance the readability of your code, consider employing the `typedef` keyword for blocks.

Here is the Syntax:

```objective-c
typedef returnType(^TypeName)(parameter1Type, parameter2Type, ...);
```

### Example: Typedef for a Block

```objective-c
typedef void(^SimpleBlock)(void);

SimpleBlock simpleBlock = ^{
    NSLog(@"This is a simple block");
};

simpleBlock();
```

### Best Practices

- Use `copy` when assigning a Block to a `strong` property to prevent potential issues with a stack-based block.

- It might be beneficial to use `weak` if the block outlives its original scope and retains `self`. This approach can be especially relevant in View-Controller contexts to prevent retain cycles.
<br>

## 9. Provide examples of various _control flow structures_ available in _Objective-C_.

**Objective-C** pioneers the **control flow** options also found in C and introduces the intuitive `for-in` loop for fast and convenient iterations over collections.

### if-else Statement

The `if` and optional `else` statement allow for conditional branching:

```objective-c
int score = 75;

if (score >= 60) {
    NSLog(@"Pass");
} else {
    NSLog(@"Fail");
}
```

### switch Statement with break

The `switch` statement pairs with `case` labels to execute specific blocks of code. The `break` keyword ensures the control flow exits the `switch` block:

```objective-c
int option = 2;

switch (option) {
    case 1:
        NSLog(@"Option 1 selected");
        break;
    case 2:
        NSLog(@"Option 2 selected");
        break;
    default:
        NSLog(@"Unknown option selected");
        break;
}
```

### for Loop: Numeric Range

Use the `for` loop with an integer iterator to define the starting point, the end point, and an increment:

```objective-c
for (int i = 0; i < 5; i++) {
    NSLog(@"%d", i);
}
```

### Conditional Expression (Ternary Operator)

This operator provides a concise way to express a conditional operation:

```objective-c
int a = 10, b = 20;
int max = (a > b) ? a : b;
```

### while Loop: Pre-Tested Loop

The `while` loop tests the condition before each iteration:

```objective-c
int count = 1;

while (count <= 5) {
    NSLog(@"%d", count);
    count++;
}
```

### do-while Loop: Post-Tested Loop

The `do-while` loop guarantees at least one execution before evaluating the condition:

```objective-c
int num = 5;
do {
    NSLog(@"%d", num);
    num--;
} while (num > 0);
```

### for-in Loop: Collection Iteration

The `for-in` loop in Objective-C streamlines the iteration over collections. Here's an example using `NSArray`:

```objective-c
NSArray *cars = @[@"Honda", @"Toyota", @"Ford"];

for (NSString *car in cars) {
    NSLog(@"%@", car);
}
```
<br>

## 10. How do you create and use an _enum_ in _Objective-C_?

In Objective-C, you can utilize the `typedef enum` for better type-safety and readability. When you create an `enum`, a data type is defined, simplifying your code.

### Enum Syntax

Here is the Swift code:

```swift
typedef enum {
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
} DaysOfTheWeek;
```


### Enum Components

- **Enumerator Constants**: The identifiers within the `enum` are constants. By default, they are integers, the first one being `0` and incrementing by one.

- **Enum Name**: This optional identifier helps you reference the `enum`. It simplifies scoping when you have multiple `enum` types.

### Enum Declaration Types

- **Enum Declaration**: Provides a flexible solution but doesn't enforce type-safety.

```objective-c
enum {
    Cat,
    Dog,
    Horse
};
```

- **Named Enum**: Ensures type-safety, making code more readable and less error-prone.

```objective-c
typedef enum {
    Small,
    Medium,
    Large
} Size;
```

### Using Enums

1. **Typedef & Name**:

    ```objective-c
    Size currentSize = Small;
    if (currentSize == Medium) {
        NSLog(@"It's a medium size");
    }
    ```

2. **Enum Only**:

    ```objective-c
    DaysOfTheWeek today = Tuesday;
    int dayCode = today;  // Returns 2.
    ```

3. **Untyped Enums**:

    ```objective-c
    enum { A, B, C } myEnum;

    if (myEnum == A) {
        NSLog(@"It's A.");
    }
    ```
<br>

## 11. How does _inheritance_ work in _Objective-C_?

**Objective-C** relies heavily on a messaging system rather than direct function calls. This influences the way inheritance is implemented.

### Implementation

Inheritance is one of the three pillars of Object-Oriented Programming. It allows a **subclass** to inherit (reuse) characteristics and behaviors from a **superclass**. 

Within Objective-C, inheritance utilizes the `:` character in class/interface declarations, which helps set up the hierarchy and aids in **method resolution**.

### Key Mechanisms

- **Method Resolution**: If a method is invoked on an object of a certain class and that method is not defined for that class, the runtime follows a chain of inheritance to look for the method in the superclass.
  
- **Dynamic Typing**: Objects are typed at runtime, meaning that the actual class of an object can be different from the static type with which it was originally declared.

### Code Example: Unique Features of Inheritance in Objective-C

Here is the Objective-C code:

**Header File (`Vehicle.h`)**

```objective-c
#import <Foundation/Foundation.h>

@interface Vehicle : NSObject

- (void)startEngine;

@end
```

**Implementation File (`Vehicle.m`)**

```objective-c
#import "Vehicle.h"

@implementation Vehicle

- (void)startEngine {
    NSLog(@"Vehicle engine started.");
}

@end
```

**Header File (`Car.h`)**

```objective-c
#import "Vehicle.h"

@interface Car : Vehicle

- (void)drive;

@end
```

**Implementation File (`Car.m`)**

```objective-c
#import "Car.h"

@implementation Car

- (void)drive {
    [self startEngine]; // Inherits startEngine method from Vehicle
    NSLog(@"Car is being driven.");
}

@end
```
<br>

## 12. What is _polymorphism_, and how is it achieved in _Objective-C_?

**Polymorphism** in object-oriented programming refers to the ability of different classes to be treated as instances of a shared superclass. This allows methods to be called dynamically and for their behavior to be determined by the specific object in use.

### Achieving Polymorphism in Objective-C

Objective-C primarily leverages **dynamic binding** for polymorphism using the concept of **message dispatch**.

#### Dynamic Binding

At runtime, the system determines the correct method implementation for a particular object based on its class.

#### \#import Statements

The `#import` directive is used in Objective-C to ensure that a header file is only included once in a project or translation unit. This helps avoid header related issues. Here's a detailed example of using #import statements.

If we assume:
```plaintext
A.h -> #import "B.h" and #import "C.h"
B.h, C.h -> #import "D.h"
```
Then,
- "**D.h**" and other headers recursively included by "**D.h**" are included only once, which avoids redundancy.

- Circular inclusions are avoided.

### Coding Example: Using #import for Header Files

Here is the Code Example:

File **A.h**

```objc
#import "B.h"
#import "C.h"
// ...
```
File **B.h, C.h**
```objc
#import "D.h"
// ...
```
File **D.h**
```objc
// ...
```

In this setup, "**D.h**" is included once in each of **B.h** and **C.h**.

This approach avoids duplicated inclusions and prevents circular inclusion issues.
<br>

## 13. Explain the concept of _encapsulation_ and give an example in the context of _Objective-C_.

In Objective-C, **encapsulation** involves bundling the data (instance variables) and methods (instance methods) that act on the data into a single unit, the **class**. It restricts access to the class members, allowing only specific methods to operate on them. This primarily serves two purposes:

- **Data Hiding**: It provides a clear separation between the internal representation of an object and the outside world. This helps prevent unintentional changes in the internal state of the object and restricts the use of sensitive data.

- **Modularization**: It helps in modularizing complex systems by defining clear boundaries that separate different parts of the program. This ensures that changes made in one part of the program do not affect the stability of other components.

Encapsulation is implemented in Objective-C using the modern property syntax and access specifiers.

### Encapsulation Mechanisms in Objective-C

1. **Access Specifiers**:
   - Objective-C supports two access specifiers: `@public` and `@private`. However, their use is limited in comparison to other languages like C++.
   - Instance variables are private by default.
   
2. **Modern Property Syntax**:
   - The `@property` and `@synthesize` directives, prior to Objective-C 2.0, were used to declare instance variables and their corresponding getter and setter methods.
   - From Objective-C 2.0 onwards, the `@property` directive is utilized to declare properties, and the `@synthesize` directive is optional.

3. **Manual Encapsulation**:
   - Before the advent of modern property directives, encapsulation was primarily achieved manually. Each property in the class had to be backed by a private variable, and separate methods for getting and setting the property were required.

4. **Class Extensions**:
   - Objective-C permits the use of **class extensions** to define private methods and properties not accessible outside the class.

5. **Internal Representation**:
   - Objective-C **objects contain instance variables** that are not directly accessible from outside. This enforces a certain level of encapsulation or data hiding.

6. **Direct Access**:
   - Access to instance variables can still be achieved without the use of accessor methods or properties. This is, however, not always recommended, especially when using advanced features of Objective-C like Key-Value Observing (KVO).

### Code Example: Encapsulation in Objective-C

Here is the Objective-C code:

  ```objc
  @interface BankAccount : NSObject

  // Public properties
  @property (readonly) NSString* accountNumber;

  // Constructors
  - (instancetype)initWithNumber:(NSString*)number;
  + (instancetype)uninitializedAccount;

  // Public methods
  - (void)deposit:(double)amount;
  - (void)withdraw:(double)amount;

  @end

  @implementation BankAccount {
    // Private instance variable
    double _balance;
  }

  - (instancetype)initWithNumber:(NSString*)number {
    self = [super init];
    if (self) {
      _balance = 0.0;
      _accountNumber = [number copy];
    }
    return self;
  }

  - (void)deposit:(double)amount {
    if (amount > 0) {
      _balance += amount;
    }
  }

  - (void)withdraw:(double)amount {
    if (amount > 0 && amount <= _balance) {
      _balance -= amount;
    }
  }

  @end
  ```

	In this code example:

	- The `BankAccount` class encapsulates its internal state (the `_balance` variable) and methods (`deposit` and `withdraw`) that operate on that state.
	- The `accountNumber` property is read-only and is set at the time of account creation through the designated initializer `initWithNumber:`. Afterwards, it's not supposed to be modified, demonstrating the behavior of an attribute with limited write access.
	- It uses the private instance variable `_balance`, which isn't accessible outside the class, and direct access to it from outside the class is prevented. This showcases data hiding.
	- The balance can only be updated through the methods `deposit` and `withdraw`, not directly, thus enforcing consistent state transitions.
<br>

## 14. How do you define a _class_ in _Objective-C_, and what is the significance of the _NSObject_ class?

In Objective-C, a class primarily serves three roles:

1. **Blueprint for Objects**: It defines what data and behavior an object of the class will have.
2. **Namespace for Methods**: It groups related method implementations.
3. **Adheres to Protocols**: It can conform to one or more protocols.

### Key Components of an Objective-C Class

- **Interface** (Header File - .h): Contains the class's external-facing elements.
- **Implementation** (Source File - .m): Contains the method implementations and private declarations.

### The Anatomy of a Class in Objective-C

#### Interface Declaration

- **Extends Classes**: List of classes from which the class inherits.
- **Adheres to Protocols**: Describes the protocols with which the class complies.
- **Access Modifiers**: Can be specified using `@public`, `@protected`, and `@private`.

Here is the Objective-C code:

```objective-c
// Car.h: Header File

#import <Foundation/Foundation.h>

@interface Car: NSObject

// Properties
@property (nonatomic) NSString *make;  // Implicitly strong attribute
@property (nonatomic) NSString *model;
@property (nonatomic) int year;

// Methods
- (void)start;  // Public method declaration

@end
```

#### Implementation Definition

- **ivars**: Encapsulates instance variables.
- **Synthesize**: Binds properties to instance variables.
- **Methods**: Contains the implementations of public and private methods.

```objective-c
// Car.m: Implementation File
#import "Car.h"

@interface Car ()  // Private declarations here
@property (nonatomic) BOOL engineStarted;
@end

@implementation Car {
    // Private instance variables
    int mileage;
    float fuelLevel;
}

// Synthesize methods
@synthesize engineStarted;

// Method implementations
- (void)start {
    // Start car engine
    self.engineStarted = YES;
}

@end
```

## The Foundation Class: NSObject

The `NSObject` class brings fundamental behaviors and protocols to all classes in Objective-C, including memory management, introspection, and protocol support. This class is the foundation for object-oriented development in the language.

### Key Methods and Behaviors Provided by NSObject

#### Memory Management

- `+ (id)alloc`: Responsible for allocating memory.
- `- (id)init`: Initializes the object.
- `- (void)dealloc`: Manages the deallocation of object resources.

#### Type and Protocol Information

- `+ (BOOL)isSubclassOfClass:(Class)aClass`: Tests if the class is a subclass of `aClass`.
- `- (BOOL)conformsToProtocol:(Protocol *)aProtocol`: Checks if the class conforms to `aProtocol`.

#### Object Lifecycle and Awareness

- `- (BOOL)isEqual:(id)object`: Compares the current object with `object` for equality.
- `- (NSUInteger)hash`: Returns a hash value for the object.
- `- (NSString *)description`: Provides a textual description of the object.

Make sure to adhere to the inheritance hierarchy and let your classes, directly or indirectly, inherit from `NSObject` for foundational Objective-C support.
<br>

## 15. What is _method overloading_, and is it supported in _Objective-C_?

**Objective-C** does not directly support method overloading as is the case in **Java** or **C++**. Instead, it uses a practice known as **"making similar methods"**, where you define distinct names for methods exhibiting varied behaviors or parameter sets.

### Objective-C's Approach

Objective-C relies on message-passing through its `-[SomeClass someMethod]` format. When you attempt to call a method on an object, Objective-C's runtime system **determines** which specific method to invoke based on its parameter signature. It uses the method's selector, which identifies the method's name and parameter lists.

#### Creating Variants Via Parameters

You can achieve the method-overloading behavior by using different parameters or none at all. For example, the `doSomething` method below can be invoked with varied argument sets. Objective-C discerns between these based on the number of parameters or their specific types.

```objc
- (void) doSomething;        // No parameters
- (void) doSomething:(int)a; // Single int parameter
- (void) doSomething:(int)a andMore:(int)b; // Two int parameters
```

This way, calling `doSomething`, `doSomething:42`, or `doSomething:42 andMore:99` helps the Objective-C runtime understand which method to execute based on the specific parameter set used during the method call.

### Practical Example: NSMutableArray

Objective-C core **Apple frameworks**, including the Foundation framework, implement method overloading through these unique method names.

For example, `NSMutableArray` offers these distinctive method signatures to **add objects**:

- `- (void)addObject:(ObjectType)anObject;`
- `- (void)insertObject:(ObjectType)anObject atIndex:(NSUInteger)index;`

This mechanism streamlines the handling process for developers working on Objective-C codebases, especially if they're accustomed to the practice of method overloading from other object-oriented languages.
<br>



#### Explore all 55 answers here 👉 [Devinterview.io - Objective-C](https://devinterview.io/questions/web-and-mobile-development/objective-c-interview-questions)

<br>

<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

