### Using the `params` keyword
When a method's last parameter is declared with the `params` keyword, callers can pass zero or more arguments without explicitly creating an array. The C# compiler collects those arguments into an array at call time.

Example:

```csharp
void PrintNumbers(params int[] numbers)
{
    foreach (var n in numbers) Console.WriteLine(n);
}

// Calls:
PrintNumbers(1, 2, 3);         // compiler creates int[] { 1, 2, 3 }
PrintNumbers();                // compiler creates an empty int[] { }
PrintNumbers(new int[] { 4 }); // explicit array still allowed
```

Notes:
- `params` must be the last parameter in the method signature.
- A method can have at most one `params` parameter.
- The compiler creates the array when you omit it at the call site.
- `params` can be used with any array type (e.g., `int[]`, `string[]`).

Example from the BCL:

```csharp
// Console.WriteLine has an overload that accepts params object[]
public static void WriteLine(string format, params object[] args);
```

Console example:

```csharp
Console.WriteLine("Values are: {0}, {1}, {2}", 10, 20, 30);
```

Optional Parameters
-------------------

C# allows defining optional parameters by providing default values in the signature. Callers can omit those arguments and the defaults are used.

Example:

```csharp
void DisplayInfo(string name, int age = 30, string city = "Unknown")
{
    Console.WriteLine($"Name: {name}, Age: {age}, City: {city}");
}

// Calls:
DisplayInfo("Alice");                    // Uses default age and city
DisplayInfo("Bob", 25);                  // Uses default city
DisplayInfo("Charlie", 28, "New York");  // No defaults used
```

Notes:
- Optional parameters must come after all required parameters.
- Specify default values directly in the method signature.

Summary
-------
- Use `params` to accept a variable number of arguments as an array.
- Use optional parameters to provide defaults so callers can omit arguments.
- `params` must always be the last parameter in the method signature.

Instance (Object) Creation in C#
--------------------------------

When you create an object with `new`, the runtime performs these steps:

1. Memory allocation
   - CLR allocates space on the managed heap for the instance fields and zero-initializes the memory.
2. Constructor invocation
   - The appropriate constructor runs to initialize the instance.
3. Reference return
   - A reference to the heap object is returned and typically stored on the stack (local variable) or in another heap object (field).
4. Lifetime and cleanup
   - The object remains on the managed heap until it becomes unreachable; the GC reclaims it later.
   - Static members live in per-type storage, not per-instance.

Notes and important details
- Declaration vs initialization:
  - Declaration (e.g., `Person p;`) creates a variable; it does not allocate the instance and is null until assigned.
  - Initialization (`p = new Person();`) allocates the instance and runs the constructor.
- Reference types vs value types:
  - Reference types (classes) are allocated on the heap and accessed via references.
  - Value types (structs) are stored inline (stack or containing object) unless boxed.
- If a reference is a field of another object, the reference itself is stored inside the containing object (on the heap), while the referred object's data is elsewhere on the heap.
- Large objects (>= LOH threshold) may be allocated on the Large Object Heap (LOH) with different GC behavior.
- Accessing a null reference causes a NullReferenceException.

Examples
--------

Declaration only (no allocation):

```csharp
Person p; // p is declared; unassigned local variables must be initialized before use
```

Separate initialization:

```csharp
p = new Person();  // memory allocated, constructor executed, p now references the instance
p.Name = "John";
p.Age  = 30;
```

Declaration + initialization:

```csharp
Person p = new Person();
Person q = new Person { Name = "Amy" }; // object initializer syntax
```

Parameterized constructor:

```csharp
public class Person
{
    public string Name;
    public int Age;
    public Person(string name, int age) { Name = name; Age = age; }
}

Person p = new Person("John", 30);
```

Common pitfalls
---------------
- Forgetting to call `new` leaves a reference null → NullReferenceException.
- Frequently creating short-lived large objects can pressure the GC (consider pooling).
- Reuse expensive objects (e.g., avoid repeatedly creating heavy resources); prefer DI or singletons where appropriate.

Terminology
-----------
- Variable of a class: a variable declaration (e.g., `Person p;`) that holds a reference but does not allocate the instance.
- Instance of a class: the actual object allocated with `new` that occupies memory and whose members can be accessed.
- Reference of a class: when we initialize of a class by using an existing instance of that class, the variable holds a reference to that instance.

Simple example:

```csharp
class Person
{
    public string Name;
}

// Variable of a class (no object created yet)
Person p1;

// Instance of a class (object created on the heap)
p1 = new Person();
p1.Name = "Alice";

// Reference of a class (p2 points to the same instance as p1)
Person p2 = p1;

Console.WriteLine(p2.Name); // Output: Alice

// Changing via p2 affects p1 (same object)
p2.Name = "Bob";
Console.WriteLine(p1.Name); // Output: Bob
```

- `Person p1;` → **Variable**: declares a reference, no object exists.
- `new Person()` → **Instance**: creates the actual object in memory.
- `Person p2 = p1;` → **Reference**: `p2` now refers to the same instance as `p1`.

```csharp
First f = new First();
f = null;
// Creates a new First instance and assigns it to f, then clears that reference.
// new First() allocates an object on the heap and returns a reference stored in f.
// f = null removes the reference from the variable; the object becomes eligible for GC
// only if no other live references refer to it. Assigning null does not immediately
// destroy the object or force garbage collection.
```

De-referencing an Instance
--------------------------

You can **de-reference** an instance of any class by assigning `null` to it. Once `null` is assigned to a reference variable, you can no longer use that variable to access members of the class. Attempting to do so causes a **runtime error** (`NullReferenceException`).

Example:

```csharp
First f = new First();
Console.WriteLine(f.x); // Valid
f = null;
Console.WriteLine(f.x); // Invalid — causes NullReferenceException
Console.ReadLine();
```

**Note:** Assigning `null` to a reference does not immediately de-allocate the memory for the object. Instead, the object is marked as unreachable. The **Garbage Collector (GC)** reclaims memory from unreachable objects when it runs, not at the moment `null` is assigned.



ASCII Diagram: Variable, Instance, Reference, and Null
-------------------------------------------------------

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              STACK                                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────┐                                                              │
│   │ p1       │──────────────────────────┐                                   │
│   │ (ref)    │                          │                                   │
│   └──────────┘                          │                                   │
│                                         ▼                                   │
│   ┌──────────┐                  ┌───────────────────┐                       │
│   │ p2       │─────────────────►│  HEAP             │                       │
│   │ (ref)    │                  │  ┌─────────────┐  │                       │
│   └──────────┘                  │  │ Person      │  │                       │
│                                 │  │ Instance    │  │                       │
│   ┌──────────┐                  │  │ ─────────── │  │                       │
│   │ p3       │                  │  │ Name: "Bob" │  │                       │
│   │ (null)   │───► X (nothing)  │  │ Age: 25     │  │                       │
│   └──────────┘                  │  └─────────────┘  │                       │
│                                 └───────────────────┘                       │
└─────────────────────────────────────────────────────────────────────────────┘

LEGEND:
─────────────────────────────────────────────────────────────────────────────

    Person p1;              → Variable (unassigned, cannot use yet)
    p1 = new Person();      → Instance created on heap, p1 references it
    Person p2 = p1;         → Reference (p2 points to same instance as p1)
    Person p3 = null;       → Null reference (points to nothing)

─────────────────────────────────────────────────────────────────────────────

STEP-BY-STEP VISUALIZATION:

    1. VARIABLE ONLY (no instance)
         ┌──────────┐
         │ p1       │───► ? (undefined/unassigned)
         └──────────┘

    2. INSTANCE CREATED
         ┌──────────┐         ┌─────────────┐
         │ p1       │────────►│ Person Obj  │  ← Heap
         └──────────┘         └─────────────┘

    3. REFERENCE COPY (p2 = p1)
         ┌──────────┐
         │ p1       │────┐
         └──────────┘    │    ┌─────────────┐
                                         ├───►│ Person Obj  │  ← Same instance!
         ┌──────────┐    │    └─────────────┘
         │ p2       │────┘
         └──────────┘

    4. NULL REFERENCE
         ┌──────────┐
         │ p3       │───► null (nothing)
         └──────────┘

         Accessing p3.Name → NullReferenceException!

─────────────────────────────────────────────────────────────────────────────

MEMORY LIFECYCLE:

    new Person()          GC runs
             │                   │
             ▼                   ▼
    ┌─────────┐         ┌─────────┐
    │ Allocate│         │ Reclaim │
    │ on Heap │         │ Memory  │
    └─────────┘         └─────────┘
             │                   ▲
             ▼                   │
    ┌─────────┐         ┌─────────┐
    │ Return  │         │ Object  │
    │ Ref     │         │Unreached│
    └─────────┘         └─────────┘
             │                   ▲
             ▼                   │
    ┌─────────┐         ┌─────────┐
    │ Use     │────────►│ ref=null│
    │ Object  │         │ or out  │
    └─────────┘         │ of scope│
                        └─────────┘
```

Mind Map: Multiple References to the Same Instance
---------------------------------------------------

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         MIND MAP: REFERENCE SURVIVAL                        │
└─────────────────────────────────────────────────────────────────────────────┘

    SCENARIO: f1 and f2 reference the same object; f1 set to null

    ═══════════════════════════════════════════════════════════════════════════

    STEP 1: Both f1 and f2 reference the same instance
    ───────────────────────────────────────────────────

         STACK                              HEAP
        ┌──────────┐                 ┌─────────────────┐
        │ f1       │────────────────►│  First Instance │
        └──────────┘            ┌───►│  ───────────────│
                                │    │  x = 10         │
        ┌──────────┐            │    │  y = 20         │
        │ f2       │────────────┘    └─────────────────┘
        └──────────┘

        First f1 = new First();
        First f2 = f1;           // f2 now points to same object

    ═══════════════════════════════════════════════════════════════════════════

    STEP 2: f1 is set to null — f2 STILL works!
    ────────────────────────────────────────────

         STACK                              HEAP
        ┌──────────┐                 ┌─────────────────┐
        │ f1       │───► null        │  First Instance │
        └──────────┘                 │  ───────────────│
                                     │  x = 10         │
        ┌──────────┐                 │  y = 20         │
        │ f2       │────────────────►│                 │
        └──────────┘                 └─────────────────┘

        f1 = null;               // Only f1's reference is removed
        Console.WriteLine(f2.x); // ✓ VALID — prints 10

    ═══════════════════════════════════════════════════════════════════════════

    KEY INSIGHT:
    ┌─────────────────────────────────────────────────────────────────────────┐
    │  Setting f1 = null does NOT affect f2.                                  │
    │  The object remains alive because f2 still references it.               │
    │  GC will NOT collect the object while any live reference exists.        │
    └─────────────────────────────────────────────────────────────────────────┘

    ═══════════════════════════════════════════════════════════════════════════

                        ┌───────────────┐
                        │   new First() │
                        └───────┬───────┘
                                │
                    ┌───────────┴───────────┐
                    ▼                       ▼
              ┌──────────┐           ┌──────────┐
              │    f1    │           │    f2    │
              └────┬─────┘           └────┬─────┘
                   │                      │
                   ▼                      ▼
              ┌─────────┐           ┌─────────────┐
              │ f1=null │           │ f2 still    │
              │ ✗ lost  │           │ ✓ valid    │
              └─────────┘           └─────────────┘
                                          │
                                          ▼
                                   ┌─────────────┐
                                   │ Object ALIVE│
                                   │ (reachable) │
                                   └─────────────┘
```

Code Example:

```csharp
class First
{
    public int x = 10;
}

First f1 = new First();  // Instance created
First f2 = f1;           // f2 references the same instance

f1 = null;               // f1 no longer references the object

Console.WriteLine(f2.x); // ✓ Output: 10 — f2 still works!
// Console.WriteLine(f1.x); // ✗ NullReferenceException — f1 is null
```

**Takeaway:** An object is only eligible for garbage collection when **all** references to it are removed or go out of scope.

