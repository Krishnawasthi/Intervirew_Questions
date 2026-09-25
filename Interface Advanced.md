# Advanced Java Interface Interview Questions

This README covers advanced and follow-up questions that are commonly
asked after the basic Java Interface concepts.

The answers are written in **simple interview-friendly language** so
they can be explained naturally during an interview.

------------------------------------------------------------------------

## 21. What is a default method conflict in Java?

A default method conflict occurs when a class implements two interfaces
that contain default methods with the same method signature.

For example:

-   Interface A has a default `show()` method.
-   Interface B also has a default `show()` method.
-   A class implements both A and B.

Java now has two possible implementations and cannot automatically
decide which one to use.

Therefore, the implementing class must **override the method and resolve
the conflict**.

### Interview Answer

> A default method conflict occurs when a class implements multiple
> interfaces that provide default methods with the same signature. Java
> cannot choose between the two implementations, so the implementing
> class must override the method and resolve the conflict.

### Important Point

If both interfaces contain the same abstract method, there is generally
no conflict because the class can provide one implementation.

The conflict occurs when **both interfaces provide competing default
implementations**.

------------------------------------------------------------------------

## 22. What is the Diamond Problem in Java?

The diamond problem is an ambiguity caused by multiple inheritance when
the same method can be inherited through multiple paths.

A simplified structure looks like this:

``` text
       A
      / \
     B   C
      \ /
       D
```

If A provides a method and both B and C inherit it, D may have two
possible paths to the same method.

Java avoids this problem for classes by **not allowing a class to extend
multiple classes**.

However, Java allows multiple interfaces, so a similar conflict can
happen with default methods.

In that case, Java requires the implementing class to resolve the
conflict.

### Interview Answer

> The diamond problem is an ambiguity caused by multiple inheritance
> when the same method can be inherited through multiple paths. Java
> avoids this problem for classes by allowing a class to extend only one
> class. With interfaces, default-method conflicts can still occur, and
> Java requires the implementing class to resolve them.

### Remember

-   Multiple classes → Not allowed
-   Multiple interfaces → Allowed
-   Conflicting default methods → Must be resolved

------------------------------------------------------------------------

## 23. What is `InterfaceName.super.method()`?

`InterfaceName.super.method()` is used when a class implements an
interface that provides a default method and the class wants to
explicitly call that interface's default implementation.

It is especially useful when two interfaces provide different default
implementations of the same method.

For example, if interfaces A and B both provide a default `show()`
method, a class can override `show()` and explicitly select the
implementation it wants.

Conceptually:

``` java
A.super.show();
```

or:

``` java
B.super.show();
```

### Interview Answer

> `InterfaceName.super.method()` is used inside an implementing class to
> explicitly invoke the default method of a particular interface. It is
> mainly useful for resolving default-method conflicts between
> interfaces.

### Important Restriction

It is used for a default method of a **direct superinterface**.

It is not a way to call:

-   static interface methods
-   abstract methods
-   methods from unrelated interfaces

------------------------------------------------------------------------

## 24. What are static methods in interfaces?

A static method in an interface belongs to the **interface itself**,
rather than to objects of implementing classes.

Static interface methods were introduced in **Java 8**.

They are useful when the behavior is related to the interface but does
not require object-specific state.

A static interface method is accessed using the interface name.

Conceptually:

``` java
InterfaceName.method();
```

### Static vs Default

**Static method:**

-   belongs to the interface
-   accessed through the interface name
-   is not inherited as an instance method
-   cannot be overridden as an instance method

**Default method:**

-   provides instance behavior
-   can be inherited by implementing classes
-   can be overridden by implementing classes

### Interview Answer

> A static method in an interface belongs to the interface itself. It
> does not belong to implementing class objects and is accessed using
> the interface name. Unlike default methods, static methods cannot be
> overridden as instance methods.

### Easy Way to Remember

**Static → Interface**

**Default → Object behavior**

------------------------------------------------------------------------

## 25. What are private methods in an interface?

Private methods were introduced in interfaces in **Java 9**.

They are used as **helper methods inside an interface**.

Suppose an interface has several default methods and they share common
logic.

Instead of writing the same logic repeatedly, that common logic can be
placed inside a private method.

The private method can then be used by the interface's own methods.

### Why are they useful?

They help with:

-   code reuse
-   avoiding duplicate logic
-   better maintainability
-   keeping implementation details inside the interface

### Can an implementing class access the private method?

No.

The private method belongs to the internal implementation of the
interface.

### Interview Answer

> Private interface methods were introduced in Java 9 to allow default
> and static methods inside an interface to share common implementation.
> They are internal helper methods and cannot be accessed or overridden
> by implementing classes.

------------------------------------------------------------------------

## 26. What is a functional interface?

A functional interface is an interface that contains **exactly one
abstract method**.

It can still contain:

-   default methods
-   static methods
-   private methods

The important rule is that it must have exactly **one abstract method**.

Functional interfaces are especially important because they can be used
with **lambda expressions**.

### Examples

Common functional interfaces in Java include:

-   `Runnable`
-   `Callable`
-   `Comparator`
-   `Predicate`
-   `Function`
-   `Consumer`
-   `Supplier`

### Interview Answer

> A functional interface is an interface with exactly one abstract
> method. It can have any number of default, static, and private
> methods, but only one abstract method. Functional interfaces are used
> as the target type for lambda expressions.

------------------------------------------------------------------------

## 27. What is `@FunctionalInterface`?

`@FunctionalInterface` is an annotation used to tell the compiler that
an interface is intended to be a functional interface.

It allows the compiler to check that the interface has exactly one
abstract method.

If another abstract method is accidentally added, the compiler reports
an error.

### Why is it useful?

It provides:

-   compile-time validation
-   clearer developer intention
-   protection against accidentally breaking a functional interface

### Important Point

The annotation itself does **not** make an interface functional.

An interface is functional because it has exactly one abstract method.

### Interview Answer

> `@FunctionalInterface` is an annotation that tells the compiler that
> an interface is intended to contain exactly one abstract method. It
> provides compile-time validation and makes the developer's intention
> clear.

------------------------------------------------------------------------

## 28. What is a lambda expression and how is it related to interfaces?

A lambda expression is a concise way of providing an implementation for
the **single abstract method of a functional interface**.

Before Java 8, we often used anonymous classes for this purpose.

Lambda expressions made this much shorter and easier to read.

### Important Relationship

Lambda expressions require a **functional interface** as their target
type.

They do not work with an interface that has multiple abstract methods.

### Interview Answer

> A lambda expression provides a concise implementation of the single
> abstract method of a functional interface. It was introduced in Java 8
> and is mainly used to make functional-style programming shorter and
> more readable.

### Easy Relationship

``` text
Functional Interface
        ↓
One Abstract Method
        ↓
Lambda can implement it
```

------------------------------------------------------------------------

## 29. Can a functional interface have default and static methods?

Yes.

A functional interface can contain:

-   one abstract method
-   multiple default methods
-   multiple static methods
-   private methods

The important rule is that it must have **only one abstract method**.

### Example Concept

An interface can have:

-   `calculate()` → abstract
-   `print()` → default
-   `validate()` → static

It is still a functional interface because only `calculate()` is
abstract.

### Interview Answer

> Yes. A functional interface can contain multiple default, static, and
> private methods. The only requirement is that it must have exactly one
> abstract method.

------------------------------------------------------------------------

## 30. Can an interface extend multiple interfaces?

Yes.

An interface can extend more than one interface.

This allows us to combine multiple contracts into one interface.

For example:

``` text
Camera
   \
    SmartDevice
   /
GPS
```

`SmartDevice` can extend both `Camera` and `GPS`.

A class implementing `SmartDevice` must satisfy the inherited contracts.

### Interview Answer

> Yes, an interface can extend multiple interfaces. This allows us to
> combine multiple contracts into one interface and is one of the ways
> Java supports multiple inheritance of type.

------------------------------------------------------------------------

## 31. What is an interface reference and runtime polymorphism?

An interface reference can refer to an object of any class that
implements that interface.

For example, if `Vehicle` is an interface and `Car` implements it,
conceptually:

``` java
Vehicle v = new Car();
```

Here:

-   `Vehicle` is the reference type.
-   `Car` is the actual object type.

When an overridden method is called, Java chooses the implementation
based on the **actual object at runtime**.

This is called **runtime polymorphism** or **dynamic method dispatch**.

### Interview Answer

> An interface reference can refer to an object of any implementing
> class. When an overridden instance method is called through that
> reference, Java selects the implementation based on the actual object
> at runtime. This is runtime polymorphism.

### Remember

``` text
Reference type → Interface
Actual object  → Implementing class
Method chosen  → At runtime
```

This is widely used to achieve **loose coupling**.

------------------------------------------------------------------------

## 32. What are interface constants?

Variables declared inside an interface are automatically:

-   `public`
-   `static`
-   `final`

Therefore, they are called **interface constants**.

### Why static?

Because the value belongs to the interface itself.

### Why final?

Because the value cannot be reassigned.

### Why public?

Because interface constants are part of the interface's publicly
accessible contract.

### Interview Answer

> Variables declared in an interface are implicitly public, static, and
> final. Therefore, they are constants rather than instance variables.
> They belong to the interface and cannot be reassigned.

### Remember

**Interface variable = public + static + final**

------------------------------------------------------------------------

## 33. What is the difference between an interface and an abstract class?

Both are mechanisms for abstraction, but they solve somewhat different
problems.

### Abstract Class

An abstract class is useful when multiple classes have a **strong common
relationship** and need to share:

-   instance variables
-   constructors
-   common implementation
-   protected members
-   abstract methods

For example:

``` text
Employee
   |
   ├── Developer
   └── Manager
```

The subclasses can share common employee information and behavior.

### Interface

An interface is more focused on a **contract or capability**.

For example:

``` text
Payable
```

Different classes can implement `Payable`, even if they do not belong to
the same class hierarchy.

### Major Differences

  -----------------------------------------------------------------------
  Abstract Class                      Interface
  ----------------------------------- -----------------------------------
  A class can extend only one class   A class can implement multiple
                                      interfaces

  Can have instance variables         Cannot have instance variables

  Can have constructors               Cannot have constructors

  Can maintain object state           Fields are constants

  Can have abstract and concrete      Can have abstract, default, static
  methods                             and private methods

  Can represent common base           Usually represents a
  implementation                      contract/capability
  -----------------------------------------------------------------------

### Interview Answer

> I use an abstract class when related classes need to share state and
> common implementation. I use an interface when I want to define a
> contract or capability that can be implemented by multiple classes,
> including unrelated classes.

------------------------------------------------------------------------

## 34. What is a marker interface?

A marker interface is an interface that contains **no methods defining
behavior**.

Its purpose is to provide information or metadata to the JVM, compiler,
or framework.

It essentially tells Java:

> "This class has a particular property or capability."

### Examples

Common marker interfaces include:

-   `Serializable`
-   `Cloneable`
-   `RandomAccess`

For example, `Serializable` indicates that an object can participate in
Java serialization.

### Interview Answer

> A marker interface is an interface with no methods that is used to
> mark a class with a particular capability or property. Examples
> include Serializable and Cloneable.

### Important Point

A marker interface is different from a normal interface because its
primary purpose is not to define methods that the implementing class
must implement.

Its purpose is **type-based metadata or capability indication**.

------------------------------------------------------------------------

## 35. Why does Java not support multiple inheritance of classes?

Java does not allow a class to extend multiple classes mainly to avoid
**ambiguity and complexity**, especially the diamond problem.

Imagine a class inherits from two parent classes, and both parents have
a method with the same name.

Which implementation should the child use?

The inheritance hierarchy can become ambiguous and difficult to
maintain.

Java therefore uses:

> **Single inheritance for classes**

A class can extend only one class.

But Java provides another mechanism:

> **Multiple inheritance of type through interfaces**

A class can implement multiple interfaces.

### Interview Answer

> Java does not support multiple inheritance of classes mainly to avoid
> ambiguity and complexity such as the diamond problem. Instead, Java
> allows a class to implement multiple interfaces, providing multiple
> inheritance of type without inheriting state from multiple classes.

------------------------------------------------------------------------

## 36. How does Java resolve a method between a class and an interface default method?

There is an important rule in Java:

> **A class method has priority over an interface default method.**

Suppose a class implements an interface that provides a default method
called `show()`.

If the class itself already provides a concrete `show()` method, Java
uses the class's implementation.

The interface default implementation is not selected.

### Why?

Java gives the class hierarchy higher priority than an interface default
method.

### Interview Answer

> If a class inherits a method from its class hierarchy and also gets a
> default method with the same signature from an interface, the class
> method takes priority. The interface default method is used only when
> there is no more specific class implementation.

### Easy Priority

``` text
Class method
     ↓
Interface default method
```

The class method wins.

------------------------------------------------------------------------

## 37. What happens if a superclass and an interface both provide the same method?

The **superclass method wins** over the interface default method.

For example:

``` text
        Parent
          |
        Child
          |
    implements Interface
```

If both `Parent` and `Interface` provide a compatible `show()` method,
the implementation inherited from `Parent` takes priority.

### Interview Answer

> If a superclass provides a concrete method and an interface provides a
> default method with the same signature, the superclass method has
> priority. Java gives the class hierarchy priority over interface
> default methods.

------------------------------------------------------------------------

## 38. What happens if two interfaces provide the same default method but one interface extends the other?

This is different from two unrelated interfaces.

Suppose:

``` text
ParentInterface
       ↑
ChildInterface
```

Both provide a default method with the same signature.

The **more specific child interface** takes priority.

Therefore, if a class implements the child interface, the child's
default implementation is preferred.

### Interview Answer

> If one interface extends another and both provide a default method
> with the same signature, the more specific child interface's default
> method takes priority.

------------------------------------------------------------------------

# Interface Method Resolution --- Important Rules

## Rule 1 --- Class method beats interface default

``` text
Class method
     ↓
Interface default
```

The class method wins.

------------------------------------------------------------------------

## Rule 2 --- Child interface beats parent interface

``` text
Child Interface
      ↓
Parent Interface
```

The more specific interface wins.

------------------------------------------------------------------------

## Rule 3 --- Two unrelated interfaces with conflicting defaults

``` text
Interface A → default show()
Interface B → default show()

        ↓

      Class
```

The class must **override `show()`** to resolve the conflict.

------------------------------------------------------------------------

## Rule 4 --- Same abstract method in two interfaces

Usually there is no ambiguity.

One implementation in the class can satisfy both interface contracts.

------------------------------------------------------------------------

# Final Advanced Revision Sheet

  -----------------------------------------------------------------------
  Topic                               Key Point
  ----------------------------------- -----------------------------------
  Default method conflict             Class must resolve conflicting
                                      defaults

  Diamond problem                     Ambiguity caused by multiple
                                      inheritance paths

  `InterfaceName.super.method()`      Calls a specific interface's
                                      default method

  Static interface method             Belongs to the interface

  Private interface method            Internal helper method

  Functional interface                Exactly one abstract method

  `@FunctionalInterface`              Compiler checks the
                                      functional-interface rule

  Lambda expression                   Implements a functional interface's
                                      abstract method

  Multiple interface inheritance      A class can implement multiple
                                      interfaces

  Interface reference                 Can refer to any implementing
                                      object

  Runtime polymorphism                Actual object determines overridden
                                      method

  Interface constants                 `public static final`

  Abstract class vs interface         Shared state/implementation vs
                                      contract/capability

  Marker interface                    Interface used as a
                                      marker/capability

  Multiple class inheritance          Not supported to avoid ambiguity

  Class vs default method             Class method wins

  Superclass vs default method        Superclass method wins

  Child vs parent interface           More specific interface wins

  Two conflicting defaults            Implementing class must resolve the
                                      conflict
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# Interview Answering Pattern

For these advanced questions, avoid giving only a one-line definition.

Use this structure:

### 1. Direct Answer

> "Yes, an interface can extend multiple interfaces."

### 2. Explain the Reason

> "This allows us to combine multiple contracts into one interface."

### 3. Give a Simple Example

> "For example, a SmartDevice interface can extend Camera and GPS."

This makes the answer sound like you **understand the concept** rather
than simply memorizing definitions.

------------------------------------------------------------------------

# Key Concepts to Revise Before an Interview

Before an interview, make sure you can explain these without looking at
notes:

-   Default method conflict
-   Diamond problem
-   `InterfaceName.super.method()`
-   Static interface methods
-   Private interface methods
-   Functional interfaces
-   `@FunctionalInterface`
-   Lambda expressions
-   Multiple interface inheritance
-   Interface reference
-   Runtime polymorphism
-   Interface constants
-   Interface vs abstract class
-   Marker interfaces
-   Why Java avoids multiple class inheritance
-   Method resolution between classes and interface defaults
