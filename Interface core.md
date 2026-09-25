# Java Interface --- Interview Questions & Answers

This README contains **20 Java Interface interview questions** with
detailed, interview-style answers. The answers are written in simple
language so they can be **explained verbally in an interview**, not just
memorized.

------------------------------------------------------------------------

## 1. What is an interface in Java?

An interface in Java is a **contract or blueprint** that defines what a
class must do, rather than how it should do it.

It is mainly used for **abstraction and loose coupling**.

When a class implements an interface, it agrees to provide
implementations for the methods required by that interface.

For example, a `Payment` interface can define a `pay()` operation.
Different classes such as CreditCardPayment, UPI, and NetBanking can
implement that operation in their own way.

### Interview Answer

> An interface defines a contract that implementing classes must follow.
> It is mainly used for abstraction, loose coupling, and achieving
> multiple inheritance of type in Java.

Since Java 8, an interface can also contain **default and static
methods**, and since Java 9, it can contain **private methods**.

------------------------------------------------------------------------

## 2. Can an interface have instance variables? Why or why not?

No, an interface cannot have **instance variables**.

Variables declared inside an interface are implicitly:

-   `public`
-   `static`
-   `final`

Therefore, they are **constants**, not instance variables.

The reason is that an interface does not represent an object with its
own instance state. When a class implements an interface, the interface
provides a contract rather than separate object-level data.

For example, if an interface contains a variable such as `MAX = 100`, it
belongs to the interface itself, not separately to every object of the
implementing class.

### Interview Answer

> An interface cannot have instance variables because interface fields
> are implicitly public, static, and final. Therefore, they are
> constants shared at the interface level rather than state belonging to
> individual objects.

### Remember

**Interface → constants**

**Class → instance state**

------------------------------------------------------------------------

## 3. Can an interface have constructors? Why?

No, an interface cannot have a constructor.

A constructor is used to initialize an **object of a class**.

An interface cannot be directly instantiated, so there is no interface
object whose state needs to be initialized.

Also, interfaces do not have instance variables that need
constructor-based initialization.

### Interview Answer

> An interface cannot have a constructor because constructors are used
> to initialize objects, and an interface cannot be instantiated
> directly.

------------------------------------------------------------------------

## 4. Can an interface be instantiated? If not, how can we use it?

No, we cannot directly instantiate an interface.

An interface defines a contract. It does not provide a complete concrete
object by itself.

We normally use an interface through a **class that implements it**.

For example, if `Vehicle` is an interface and `Car` implements it, we
can create a `Car` object and use a `Vehicle` reference to refer to that
object.

This is an example of **polymorphism**.

The reference type can be the interface, while the actual object is an
implementing class.

An interface can also be used with an **anonymous class**, and
functional interfaces can be used with **lambda expressions** where
applicable.

### Interview Answer

> We cannot directly instantiate an interface. We use it through an
> implementing class, usually by keeping an interface reference pointing
> to an object of the implementing class. This gives us abstraction and
> runtime polymorphism.

------------------------------------------------------------------------

## 5. What is the default access modifier for methods in an interface?

For a normal abstract method in an interface, the default access is:

**public**

A normal interface method is implicitly:

**public abstract**

So even if we do not explicitly write `public` or `abstract`, a normal
interface method has those properties.

### Important Exception

Modern interfaces can also contain:

-   `default` methods --- public by default
-   `static` methods --- public by default
-   `private` methods --- explicitly private

### Interview Answer

> A normal abstract method declared in an interface is implicitly public
> and abstract. However, interfaces can also have public default and
> static methods and private methods.

------------------------------------------------------------------------

## 6. How do you implement an interface in Java?

We use the **implements** keyword.

A class agrees to follow the contract of an interface by implementing
it.

Once a concrete class implements an interface, it must provide
implementations for all required abstract methods of that interface.

If it does not want to implement all methods, then the class itself must
be declared **abstract**.

### Interview Answer

> We implement an interface using the implements keyword. A concrete
> implementing class must provide implementations for the interface's
> abstract methods. Otherwise, the class must itself be abstract.

------------------------------------------------------------------------

## 7. Can a class implement multiple interfaces? Provide an example.

Yes.

A class can implement **multiple interfaces** in Java.

This is one of the important ways Java supports **multiple inheritance
of type** without allowing a class to extend multiple classes.

For example, a class called `SmartPhone` could implement:

-   `Camera`
-   `MusicPlayer`
-   `GPS`

The same class can therefore follow the contracts of all three
interfaces.

### Interview Answer

> Yes, a class can implement multiple interfaces. This allows a class to
> follow multiple contracts and provides multiple inheritance of type.

### Why is this useful?

A class can have different capabilities.

For example, a smartphone can behave as:

-   a camera
-   a music player
-   a GPS device

through different interfaces.

------------------------------------------------------------------------

## 8. What happens if a class does not implement all methods of an interface?

It depends on whether the class is concrete or abstract.

### Case 1: Concrete Class

If the class is concrete, it **must implement all abstract methods** of
the interface.

Otherwise, the compiler reports an error.

### Case 2: Abstract Class

If the class is declared `abstract`, it does not have to implement all
interface methods.

The responsibility can be passed to its child class.

### Interview Answer

> If a concrete class implements an interface, it must implement all of
> its abstract methods. If it does not, the class must be declared
> abstract, and its subclass can provide the remaining implementations.

------------------------------------------------------------------------

## 9. Can an interface extend another interface? How?

Yes.

An interface can extend another interface using the **extends** keyword.

The important point is:

> Interface extends interface.

It does not use `implements` for this relationship.

The child interface inherits the contract of the parent interface.

A class implementing the child interface must satisfy the requirements
coming from the inherited interface as well.

### Interview Answer

> Yes, an interface can extend another interface using the extends
> keyword. The child interface inherits the contract of the parent
> interface.

------------------------------------------------------------------------

## 10. Can an interface extend multiple interfaces?

Yes.

An interface can extend **multiple interfaces**.

This allows an interface to combine multiple contracts into one larger
contract.

For example, an interface called `SmartDevice` could extend:

-   `Camera`
-   `GPS`
-   `Bluetooth`

Any class implementing `SmartDevice` gets the combined contract of those
interfaces.

### Interview Answer

> Yes, an interface can extend multiple interfaces. This allows an
> interface to combine multiple contracts into one larger contract.

### Important Difference

A class can:

-   extend only **one class**
-   implement **multiple interfaces**

An interface can:

-   extend **multiple interfaces**

------------------------------------------------------------------------

## 11. What are default methods in an interface? Give an example.

A default method is a method inside an interface that has a **method
body**.

Default methods were introduced in **Java 8**.

Normally, interface methods were abstract and did not have
implementations. Default methods allow an interface to provide a
**common/default implementation**.

The implementing class can:

1.  use the default implementation, or
2.  override it with its own implementation.

### Real-World Example

Suppose an interface called `Vehicle` has a default method for starting
a vehicle.

The interface can provide common starting behavior.

A specific class such as `Car` can simply use that behavior or override
it if it needs different behavior.

### Interview Answer

> A default method is a method with an implementation inside an
> interface. It was introduced in Java 8 and allows implementing classes
> to inherit default behavior without being forced to implement that
> method.

------------------------------------------------------------------------

## 12. Why were default methods introduced in Java 8?

This is a very important interview question.

Default methods were mainly introduced to allow **existing interfaces to
evolve without breaking existing implementations**.

Imagine an interface has 10 methods and thousands of classes already
implement it.

Now suppose a new method needs to be added.

If the new method were abstract, every existing implementing class would
be forced to implement it.

That could break existing code.

Default methods solve this problem.

The interface can introduce a new method with a default implementation,
so existing classes can continue working.

### Interview Answer

> Default methods were introduced mainly for interface evolution and
> backward compatibility. They allow new behavior to be added to an
> existing interface without forcing every existing implementing class
> to immediately implement the new method.

### Key Point

**Java 8 default methods → interface evolution + backward
compatibility**

------------------------------------------------------------------------

## 13. What are static methods in an interface? How are they different from default methods?

A static method in an interface belongs to the **interface itself**, not
to objects of implementing classes.

A default method provides **instance behavior** to an implementing
class.

### Static Method

-   belongs to the interface
-   called using the interface name
-   is not inherited as an instance method by implementing classes
-   cannot be overridden like an instance method

### Default Method

-   provides instance behavior
-   can be inherited by implementing classes
-   can be overridden by implementing classes

### Interview Answer

> The main difference is that a static interface method belongs to the
> interface itself, whereas a default method provides instance behavior
> to implementing classes. Static methods are accessed through the
> interface name and cannot be overridden like instance methods.

### Easy Way to Remember

**static → interface**

**default → object behavior**

------------------------------------------------------------------------

## 14. What are private methods in an interface? Why are they useful?

Private methods were introduced in interfaces in **Java 9**.

They allow an interface to have **internal helper methods** that can be
reused by its own default or static methods.

Implementing classes cannot directly access these private methods.

Suppose an interface has two default methods and both need the same
internal logic.

Instead of duplicating that logic in both methods, that common logic can
be placed into a private method inside the interface.

### Why are they useful?

They help:

-   avoid duplicate code
-   improve readability
-   keep common internal logic in one place
-   support code reuse inside the interface

### Interview Answer

> Private methods were introduced in Java 9 to allow interfaces to share
> common internal logic between their default and static methods. They
> cannot be accessed or overridden by implementing classes.

------------------------------------------------------------------------

## 15. Can an interface contain a main() method? If yes, how?

Yes.

An interface can contain a `main()` method because `main()` can be
declared as a **static method**.

A main method does not require an object to execute.

Since interfaces can contain static methods, an interface can contain a
static main method.

We can execute that main method using the interface name.

### Interview Answer

> Yes, an interface can contain a main method if the main method is
> declared static. Since main is static, it can execute without creating
> an object of the interface.

### Important Point

This does **not** mean that the interface can be instantiated.

The `main()` method is simply a static method belonging to the
interface.

------------------------------------------------------------------------

## 16. How does an interface achieve multiple inheritance in Java?

Java does not allow a class to extend multiple classes because that can
create ambiguity and problems such as the classic **diamond problem**.

However, Java allows a class to implement multiple interfaces.

Therefore, a class can receive multiple **types and contracts** through
interfaces.

For example, a class can implement:

-   `Printable`
-   `Scannable`
-   `Faxable`

So one class can behave as all three types.

### Interview Answer

> Java achieves multiple inheritance of type through interfaces. A class
> can implement multiple interfaces, allowing it to follow multiple
> contracts without inheriting state from multiple classes.

### Important Clarification

Do not simply say:

> Interfaces provide complete multiple inheritance like C++.

A better answer is:

> Interfaces provide multiple inheritance of type, not multiple
> inheritance of class state.

------------------------------------------------------------------------

## 17. What happens if two interfaces have methods with the same name? How is ambiguity resolved?

It depends on the type of methods.

### Case 1: Both Interfaces Have the Same Abstract Method

Usually there is no problem if the method signatures are compatible.

The implementing class can provide **one implementation**, which
satisfies both interfaces.

Both interfaces are asking for the same behavior contract.

------------------------------------------------------------------------

### Case 2: Both Interfaces Have the Same Default Method

Now there can be a conflict.

Suppose:

-   Interface A has a default `show()`
-   Interface B also has a default `show()`

If a class implements both, Java cannot automatically decide which
default implementation to use.

Therefore, the implementing class must **resolve the conflict by
overriding the method**.

This is commonly called a **default-method conflict**.

------------------------------------------------------------------------

### Case 3: The Class Already Has the Method

Another important rule is:

> **Class method wins over interface default method.**

If the class or its superclass provides a suitable concrete method, that
method takes priority over an interface default method.

### Interview Answer

> If two interfaces contain the same abstract method, one implementation
> in the class can satisfy both. But if both interfaces provide
> conflicting default implementations, the class must resolve the
> ambiguity by overriding the method. Also, a class method has priority
> over an interface default method.

------------------------------------------------------------------------

## 18. Can an interface contain a method with a body (implementation)? When?

Yes.

Modern Java allows several types of methods with implementations inside
interfaces.

### 1. Default Methods

Introduced in **Java 8**.

They provide instance-level default behavior.

### 2. Static Methods

Introduced in **Java 8**.

They belong to the interface itself.

### 3. Private Methods

Introduced in **Java 9**.

They are used as internal helper methods.

### Interview Answer

> Yes. Since Java 8, interfaces can contain methods with implementations
> through default and static methods, and since Java 9 they can also
> contain private methods. These features were added mainly to support
> interface evolution and code reuse.

------------------------------------------------------------------------

# 19. What is the difference between an abstract class and an interface?

This is one of the most frequently asked Java interview questions.

Both are used for abstraction, but they serve somewhat different
purposes.

  -----------------------------------------------------------------------
  Abstract Class                      Interface
  ----------------------------------- -----------------------------------
  A class can extend only one class   A class can implement multiple
                                      interfaces

  Can have instance variables         Cannot have instance variables

  Can have constructors               Cannot have constructors

  Can maintain object state           Mainly defines a contract

  Can have abstract and concrete      Can have abstract, default, static
  methods                             and private methods

  Methods can have different access   Normal interface methods are public
  modifiers                           

  Represents a common base/class      Represents a contract/capability
  relationship                        
  -----------------------------------------------------------------------

### Deeper Difference

An abstract class is useful when classes have a **strong common
relationship** and need to share state or common implementation.

For example, `Employee` could be an abstract class.

Different employees can inherit common fields such as name and ID.

An interface is useful when we want to define a **capability or
contract**.

For example, `Payable`.

Different and potentially unrelated classes can implement `Payable`.

### Interview Answer

> An abstract class is useful when related classes need to share common
> state and implementation, while an interface is useful when we want to
> define a contract or capability that can be implemented by multiple
> unrelated classes. Another major difference is that a class can extend
> only one class but can implement multiple interfaces.

------------------------------------------------------------------------

# 20. When should we use an interface instead of an abstract class?

We should generally prefer an interface when our main requirement is to
define a **contract or capability**, especially when different classes
may need that capability.

For example, suppose we have:

-   `Car`
-   `Payment`
-   `Employee`
-   `Invoice`

They may be completely unrelated classes, but several of them could have
a `Payable` capability.

An interface is appropriate because each class can implement that common
contract.

An abstract class is more appropriate when classes have a **strong
"is-a" relationship** and need to share:

-   common state
-   common implementation
-   constructors
-   protected members
-   common behavior

### Interview Answer

> I would use an interface when I want to define a contract or
> capability that can be implemented by different classes, especially
> unrelated classes. I would use an abstract class when related classes
> need to share common state, constructors, or implementation.

------------------------------------------------------------------------

# Quick Revision --- Java Interface

## Interface Variables

**public + static + final**

They are constants.

## Normal Interface Methods

**public + abstract**

## Interface Constructor

**Not allowed**

## Interface Object

**Cannot be directly instantiated**

## Class → Interface

**implements**

## Interface → Interface

**extends**

## Class Can Implement

**Multiple interfaces**

## Interface Can Extend

**Multiple interfaces**

## Java 8

**default + static methods**

## Java 9

**private interface methods**

## Default Method

Provides a default implementation.

## Static Method

Belongs to the interface itself.

## Private Method

Internal helper method of the interface.

## Class Method vs Interface Default

**Class method wins.**

## Two Conflicting Default Methods

**Implementing class must resolve the conflict.**

## Main Method

An interface can contain a **static main()** method.

## Main Purpose of Interface

**Contract + abstraction + loose coupling + multiple inheritance of
type**

------------------------------------------------------------------------

# How to Answer Interface Questions in an Interview

A strong interview answer should normally follow this pattern:

### 1. Give the direct answer

> "Yes, an interface can extend multiple interfaces."

### 2. Explain why

> "This allows us to combine multiple contracts into one interface."

### 3. Give a simple practical example

> "For example, a SmartDevice interface could extend Camera, GPS and
> Bluetooth."

This approach shows the interviewer that you **understand the concept**,
rather than simply memorizing a definition.

------------------------------------------------------------------------

# Most Important Concepts to Be Ready For Follow-Up Questions

After these 20 questions, an interviewer may go deeper into:

1.  Default method conflict
2.  Diamond problem
3.  `InterfaceName.super.method()`
4.  Static methods in interfaces
5.  Private interface methods
6.  Functional interfaces
7.  `@FunctionalInterface`
8.  Lambda expressions
9.  Multiple interface inheritance
10. Interface reference and runtime polymorphism
11. Interface constants
12. Interface vs abstract class
13. Marker interfaces
14. Why Java does not support multiple class inheritance
15. Method resolution between class and interface defaults
