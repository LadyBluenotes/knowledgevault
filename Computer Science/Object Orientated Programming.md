- Contains 4 major principles

|Pillar|Core Idea|Key Mechanism|Real-World Use Case|
|---|---|---|---|
|**Encapsulation**|Hide data, expose controlled access|`private` fields, getters/setters|Secure banking apps|
|**Abstraction**|Hide implementation, show interface|Abstract classes, interfaces|Plugin architectures|
|**Inheritance**|Reuse & extend parent class logic|`extends`, `implements`|GUI frameworks (Button → Widget)|
|**Polymorphism**|One interface, multiple forms|Method overriding, interfaces|Payment processors (CreditCard, PayPal)|

---

## Encapsulation

- The mechanism of bundling data (attributes) and methods (behavior) into a single unit (class) while restricting direct access to internal state from outside the class.

### Importance

- **Prevents Invalid State**: Ensures data integrity (e.g., a `BankAccount` balance can’t be set to negative).
- **Reduces Coupling**: External code depends on methods, not direct field access.
- **Enables Refactoring**: Internal changes (e.g., switching from an array to a linked list) don’t break dependent code.

### Key technical aspects

- **Access Modifiers** (`private`, `protected`, `public`):
  - `private`: Only accessible within the class.
  - `protected`: Accessible within the class and subclasses.
  - `public`: Accessible from anywhere.
- **Getters & Setters (Accessors & Mutators)**:
  - Controlled access to fields (e.g., validation in setters).
- **Immutability**:
  - Making fields `final` (Java) or `readonly` (C#) to prevent modification after initialization.
- **Information Hiding**:
  - Internal implementation (e.g., data structures, algorithms) can change without affecting dependent code.

---

## Abstraction

- Process of hiding complex implementation details and exposing only essential features through interfaces or abstract classes.

### Importance

- **Reduces Complexity**: Users interact with high-level APIs, not low-level details.
- **Promotes Loose Coupling**: Code depends on interfaces, not concrete classes.
- **Facilitates Testing**: Mock implementations can be injected via interfaces.

### Key technical aspects

- **Abstract Classes**:
  - Can have both abstract (unimplemented) and concrete methods.
  - Cannot be instantiated directly.
- **Interfaces (Pure Abstraction)**:
  - Define contracts (method signatures) without implementation (prior to Java 8).
  - Now support `default` and `static` methods.
- **Layered Architecture**:
  - Higher-level modules depend on abstractions, not concrete implementations (Dependency Inversion Principle).

---

## Polymorphism

- Allows a subclass (child class) to inherit fields and methods from a superclass (parent class), promoting code reuse and hierarchical classification.

### Importance

- **Avoids Code Duplication**: Common logic is centralized in the parent class.
- **Supports Polymorphism**: Enables runtime method binding.
- **Can Lead to Fragile Base Class Problem**: Poorly designed inheritance can make systems rigid.

### Key points

- **"Is-A" Relationship**:
  - A `Car` **is a** `Vehicle`.
- **Method Overriding**:
  - Subclass provides a specific implementation of an inherited method (`@Override` in Java).
- **Single vs. Multiple Inheritance**:
  - Java/C# allow **single inheritance** (one parent class).
  - C++/Python allow **multiple inheritance** (multiple parents).
- **Composition Over Inheritance**:
  - Favoring object composition (e.g., `Car` has an `Engine`) over deep inheritance hierarchies.

---

## Inheritance

- Allows a class (child/sublcass) to reuse and extend the properties and methods of another (parent/superclass)

### Importance

- **Extensibility**: New subclasses can be added without modifying existing code.
- **Reduces Conditional Logic**: No need for `if-else` chains to handle different types.
- **Supports Dependency Injection**: Components can be swapped at runtime.

### Key technical aspects

- **Compile-Time (Static) Polymorphism**:
  - Method overloading (same method name, different parameters).
- **Runtime (Dynamic) Polymorphism**:
  - Method overriding (subclass provides a new implementation).
- **Interface-Based Polymorphism**:
  - A `List` can be an `ArrayList` or `LinkedList`, but code interacts with `List` interface.
- **Liskov Substitution Principle (LSP)**:
  - Subtypes must be substitutable for their base types without altering correctness.
