## What happens when we create an instance of a class?

1. Reads the class to identify the members
2. Invokes the constructors of all those classes
3. Allocates the memory that is required for execution

---

# Constructors in C#

## What is a Constructor?

A **constructor** is a special method inside a class that is automatically called when an instance (object) of that class is created. It has the same name as the class and does not have a return type (not even `void`).

### Key Characteristics of a Constructor:
- **Same name as the class** — The constructor must have the exact same name as the class it belongs to.
- **No return type** — Constructors do not return any value, not even `void`.
- **Automatically invoked** — Called automatically when you use the `new` keyword to create an object.
- **Used for initialization** — Typically used to initialize fields and set up the initial state of the object.
- **Can be overloaded** — A class can have multiple constructors with different parameters.

### Syntax:

```csharp
class ClassName
{
    // Constructor 
    public ClassName()         
    {
        // Initialization code  //Implicit constructor
    }
}
```

### Example:

```csharp
class Person
{
    public string Name;
    public int Age;

    // Constructor
    public Person()                 
    {
        Name = "Unknown";
        Age = 0;
        Console.WriteLine("Constructor called!");
    }
}

// Usage
Person p = new Person();  // Output: Constructor called!
```

---

## Default Constructor (Implicit Constructor)

If you do not define any constructor in a class, the C# compiler automatically provides a **default parameterless constructor**. This implicit constructor initializes all fields to their default values.

### Example:

```csharp
class Car
{
    public string Brand;
    public int Year;

    // No constructor defined explicitly
}

// Usage
Car myCar = new Car();  // Default constructor is called automatically
Console.WriteLine(myCar.Brand);  // Output: (null)
Console.WriteLine(myCar.Year);   // Output: 0
```

### Explanation:
- Even though no constructor is written in the `Car` class, the compiler generates a default constructor behind the scenes.
- When `new Car()` is called, the implicit constructor is invoked.
- Fields are initialized to their default values:
  - `string` → `null`
  - `int` → `0`
  - `bool` → `false`

> **Note:** If you define any constructor (with or without parameters), the compiler will **not** generate a default constructor automatically. 

---

## Fields vs. Local Variables: Default Initialization

### Important Distinction:
- **Fields** (class-level variables) are automatically initialized to their default values by the implicit constructor.
- **Local variables** (inside methods) are **not** initialized automatically and must be assigned before use.

### Example:

```csharp
class Test 
{
    int i;
    bool b;
    string s; // Only fields are initialized to default values

    public void Print()
    {
        int x;
        Console.WriteLine(x); // ❌ Invalid: local variable not initialized
    }
}
```

### After Compilation (Conceptual View):

The compiler treats the class as if the implicit constructor assigns default values to fields:

```csharp
class Test 
{
    int i;
    bool b;
    string s;

    // Implicit constructor
    public Test()
    {   
        i = 0;       // default value for int
        b = false;   // default value for bool
        s = null;    // default value for string
    }

    public void Print()
    {
        int x;                  // local variable - NOT initialized
        Console.WriteLine(x);   // ❌ Compile error: use of unassigned local variable
    }   
}
```

> **Key Takeaway:** The implicit constructor only initializes **fields**, not local variables. Always assign a value to local variables before using them.

If you dont want the implicit constructor to be created by the compiler, you can create your own parameterless constructor like below

Here is the syntax for creating your own parameterless constructor

```csharp
[<modifier>] <ClassName>([<ParameterList>])
{
    // Initialization code
}
```
Constrcutors are of two types
1. Parameterless Constructor (Default Constructor)
2. Parameterized Constructor

## Parameterless Constructor (Default Constructor)
A **parameterless constructor**, also known as a **default constructor**, is a constructor that does not take any parameters. It is used to initialize an object with default values when no specific values are provided during object creation.

A compiler always provides an implicit parameterless constructor if no constructors are defined by the user. But its also possible that the user can define any constructor (parameterized or parameterless)


## Parameterized Constructor

A **parameterized constructor** is a constructor that takes parameters, allowing you to initialize an object with specific values when it is created.

Example of Parameterized Constructor:

```csharp
class Person
{
    public string Name;
    public int Age;

    // Parameterized Constructor
    public Person(string name, int age)  
    {
        Name = name;
        Age = age;
    }
}
```

---

## Frequently Asked Questions

### Question: There is a predefined class with a default constructor. Is this an implicit constructor or a user-defined constructor?

**Answer:** We cannot determine if it is implicit or user-defined just by looking at the class usage. We need to see the class definition to determine if the default constructor was provided by the compiler (implicit) or explicitly defined by the user (user-defined).

> **Note:** All implicit constructors are parameterless, but there can be user-defined constructors that are parameterless as well.

### Question: There is a predefined class with a parameterized constructor. Is this an implicit constructor or a user-defined constructor?

**Answer:** All constructors provided by the compiler are parameterless. So, if a constructor has parameters, it is definitely a **user-defined constructor**.

Why do we need parameterized constructors?
- Implicit constructors will initialize field members with default values.
- That's why we use **parameterized constructors** to initialize field members with custom values every time an object is created.
- If you want to make a class dynamic, use **parameterized constructors**.
- Parameterized constructors allow you to create objects with different initial states by passing different arguments during object creation.
Example of Parameterized Constructor:

```csharp   
class Person
{
    public string Name;
    public int Age;

    // Parameterized Constructor
    public Person(string name, int age)  
    {
        Name = name;
        Age = age;
    }
}
// Usage
Person p1 = new Person("Alice", 30);
Person p2 = new Person("Bob", 25);
Console.WriteLine(p1.Name); // Output: Alice
Console.WriteLine(p2.Name); // Output: Bob
```

## Summary
Parameterized constructors allow you to create objects with different initial states by passing different arguments during object creation.





 



