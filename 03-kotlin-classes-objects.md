## Classes and Objects

### Classes

- The class declaration consists of the class name, the class header (specifying its type parameters, the primary constructor, and some other things), and the class body surrounded by curly braces. Both the header and the body are optional; if the class has no body, the curly braces can be omitted.

#### Kotlin has two types of constructors
1. Primary Constructor
2. Secondary Constructor

- A class in Kotlin can have a primary constructor and one or more secondary constructors. The primary constructor is a part of the class header, and it goes after the class name.
- It's not mandatory to have primary constructor. A classs can also have secondary contructors and no primmary constructor.

#### Primmary Constructor
- If the primary constructor does not have any annotations or visibility modifiers, the constructor keyword can be omitted.
  ```
  class Person(firstName: String) { /*...*/ }
  ```
- The primary constructor cannot contain any code. Initialization code can be placed in initializer blocks prefixed with the `init` keyword. It can only contain parameters,
- During the initialization of an instance, the initializer blocks `init` are executed in the same order as they appear in the class body.
- Primary constructor parameters can be used in the initializer blocks. They can also be used in property initializers declared in the class body.
- In kotlin, we have init block it is used to further perform initializations or add any code before the program starts.
- We can also assign a defaulft value into the constructor's parameters.
- Properties declared in the primary constructor can be mutable (var) or read-only (val).
- If the constructor has annotations or visibility modifiers, the `constructor` keyword is required and the modifiers go before it.
  ````
  class Customer public @Inject constructor(name: String) { /*...*/ }
  ````

#### Secondary Constructor
- A class can also declare secondary constructors, with a `constructor` keyword
  ```
  class Pet {
    constructor(owner: Person) {
        owner.pets.add(this) // adds this pet to the list of its owner's pets
    }
  }
  ```
- If a class has a primary constructor, each secondary constructor needs to delegate or invoke the primary constructor either implicitly or explicitly.
- Delegation to another constructor of the same class is done using the `this` keyword.
  ```
  class Person(val name: String) {
    val children: MutableList<Person> = mutableListOf()
    constructor(name: String, parent: Person) : this(name) {
        parent.children.add(this)
    }
  }
  ```
- Code in initializer blocks effectively becomes part of the primary constructor. The code in all initializer blocks and property initializers is executed before the body of the secondary constructor.
- Even if the class has no primary constructor, the delegation still happens implicitly, and the initializer blocks are still executed.

- If a non-abstract or concrete class does not declare any constructors (primary or secondary), it will have a generated primary constructor with no arguments. The visibility of the constructor will be public.
- If you don't want your class to have a public constructor, declare an empty primary constructor with private modifier.
  ```
  class DontCreateMe private constructor() { /*...*/ }
  ```
- Kotlin does not have a `new` keyword.
- A class can have one or more initializer `init` block

#### Class Members
- Constructor and initializer blocks
- Functionns
- Properties
- Nested and inner classes
- Object Declarationns


### Inheritance

- All classes in kotlin are derived from a common superclass `any`.
- Any has three methods `equals()`, `hashCode()`, and `toString()`. Thus, these methods are defined for all Kotlin classes.
- By default, Kotlin classes are final they can't be inherited. To make a class inheritable, mark it with the `open` keyword.
- If the derived class has a primary constructor, the base class must be initialized first in that sub class's primary constructor.
- If the derived class has no primary constructor, each of its secondary constructor has to initialize the base class constructor by using the `super` keyword. In this case the derived class secondary constructor can call different constructors of a base class.
  ```
  class MyView : View {
    constructor(ctx: Context) : super(ctx)

    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)
  }
  ```

#### Overriding methods
- Kotlin requires explicit modifier for all overridable members.
- In order, to override a function from base class, that function must be `open` and the derived class must explicitly define the override modifier.
- If the modifier is not define explicitly the compiler will complain.
- Declaring a method with same signature is not allowed in sub class or derived class.
- Final class is a class wothout `open` modifier.
- The `open` modifier has no effect when added to members of a final class.
- A member marked with `override` is a `open` itself. So it may be override in to further subclasses. In order to stop further re-overriding use `final` keyword.
  ```
  open class Rectangle() : Shape() {
    final override fun draw() { /*...*/ }
  }
  ```

#### Override Properties
- 
