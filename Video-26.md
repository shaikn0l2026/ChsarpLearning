### Pointers to Remember wrt Constructors

- `Implicit` constructors will initialize `field` members with default values.
- That's why we use **parameterized constructors** to initialize `field` members with custom values every time an object is created.
- If you want to make a `class` dynamic, use **parameterized constructors**.
- Every `class` requires some values for execution and the values that are required for a class to execute should be passed to the class with the help of a Constructor.
- Just like `parameters` of a `method` will make a method dynamic, `parameters` of a `constructor` will make a `class` dynamic.



### `this` keyword 

Fiels and Variables can have the same name as Constructor Parameters. In such cases, we use the `this` keyword to refer to the current instance of the class.

```csharp
class Person
{
    public string Name;  // Fields Name,Age
    public int Age;

    // Parameterized Constructor
    public Person(string Name, int Age)   // Variables Name,Age but are also parameters passed to constructor
    {
        this.Name = Name; // 'this.Name' refers to the field, 'Name' refers to the parameter
        this.Age = Age;   // 'this.Age' refers to the field, 'Age' refers to the parameter
    }
}
```
### Static vs  Non-Static 

Static Modifier: Its a keyword using which we can declar a class or its members as static. 

- Members of a class are divided into two types: Static Members and Non-Static Members.
- By default, all members of a class are Non-Static Members.
- If we want to declare any member of a class as static, we need to use the `static` keyword before the member declaration.

Example of Static Member:

```csharp
class Test                  //Non-Static Class
{
  int x = 10; // Non-Static Member Field
  static int y = 20; // Static Member Field
  
   public static Test()
   {
       // Static Constructor
   }
   public void Display()
   {
       // Non-Static Method
   }
   public static void Show()
   {
       // Static Method
   }

}
```
```csharp     
class Test                        //Non-Static Class
{
  int x = 10; // Non-Static Member Field
  static int y = 20; // Static Member Field
  
   public Test()
   {
       // Non-Static Constructor
   }
   public void Display()
   {
       // Non-Static Method
   }
   public static void Show()
   {
       // Static Method
   }

}
```
```csharp
static class Test                //Static Class
{
  static int y = 20; // Static Member Field
  
   static Test()
   {
       // Static Constructor                          // When you declare a class as static,                                     all its members must be static.
   }
   public static void Show()
   {
       // Static Method
   }

}
```
Non-Static Member of a class will be initialized when an object of the class is created. Static Member of a class does not require an object to be created. It will be initialized when the class is loaded into memory. We directly prefix the static member with the class name to access it. 

```csharp   
class Program
{
    static void Main(string[] args)
    {
        // Accessing Non-Static Member
        Test obj = new Test(); // Creating an object of Test class
        obj.Display(); // Calling Non-Static Method

        // Accessing Static Member
        Test.Show(); // Calling Static Method directly using class name
    }
}
```

## Non Static Fied vs Static Field

- By Default every field of a class is Non-Static Field. To make a field as Static Field we need to use `static` keyword before the field declaration.

- Non static fields are initialized when an object of the class is created, where as Static fields are initialized immediately once the execution of class starts.

Example of Non-Static Field and Static Field:

```csharp
class Sample
{
  int x = 10; // Non-Static Field
  static int y = 20; // Static Field

  static void Main()
  {
      Console.WriteLine("Non-Static Field x: " + x); // Error: Cannot access non-static field 'x' in a static context
      Console.WriteLine("Static Field y: " + y); // Valid
      Sample obj = new Sample(); // Creating an object to access Non-Static Field
      Console.WriteLine("Non-Static Field x via object: " + obj.x); // Valid
      Sample obj2 = new Sample();
      Console.WriteLine("Static Field y via class name: " + Sample.y); // Valid      
  }

}

```
### Memory Visualization: Static vs Non-Static Fields

When the program runs, here's how memory is allocated:

```
┌─────────────────────────────────────────────────────────────────┐
│                         HEAP MEMORY                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   ┌─────────────────────┐     ┌─────────────────────┐           │
│   │   obj (Instance 1)  │     │   obj2 (Instance 2) │           │
│   ├─────────────────────┤     ├─────────────────────┤           │
│   │   x = 10            │     │   x = 10            │           │
│   │   (Non-Static)      │     │   (Non-Static)      │           │
│   └─────────────────────┘     └─────────────────────┘           │
│                                                                 │
│   Each object gets its OWN copy of non-static field 'x'         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                     CLASS MEMORY (Static Area)                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   ┌─────────────────────────────────────────────┐               │
│   │           Sample Class                      │               │
│   ├─────────────────────────────────────────────┤               │
│   │   static int y = 20                         │               │
│   │   (Shared by ALL instances)                 │               │
│   └─────────────────────────────────────────────┘               │
│                                                                 │
│   Only ONE copy of static field 'y' exists for the entire class │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                         STACK MEMORY                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   ┌─────────────────────┐                                       │
│   │  obj  ──────────────┼──────► Points to Instance 1 on Heap   │
│   ├─────────────────────┤                                       │
│   │  obj2 ──────────────┼──────► Points to Instance 2 on Heap   │
│   └─────────────────────┘                                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```
In the LifeCycle of a program: A Static field is initialized only once when the class is loaded, whereas Non-Static fields are initialized each time an instance of the class is created , if no instance of a class is created then Non static field will never be initialized.

When you have non-static fields and each time you create an object of the class a new copy of non-static field is created in the memory for that object. When you have a default or Parameter less constructor , every time an object is created the non-static fields are initialized with same vales. Thats why we use Parameterized constructors to make the class dynamic by passing different values to non-static fields each time an object is created.

```csharp
class Sample
{
  int x = 10; // Non-Static Field
  static int y = 20; // Static Field
 
  public Sample(int x)
  {
      this.x = x; // Initialize non-static field with parameter value
  }
 
  static void Main()
  {   

      Console.WriteLine("Non-Static Field x: " + x); // Error: Cannot access non-static field 'x' in a static context
      Console.WriteLine("Static Field y: " + y); // Valid
      Sample obj = new Sample(10); // Creating an object to access Non-Static Field
      Console.WriteLine("Non-Static Field x via object: " + obj.x); // Valid
      Sample obj2 = new Sample(30);
      Console.WriteLine("Non-Static Field x via obj2: " + obj2.x); // Valid      
  }

}

```
Because non-static fields initilization is associated with constructor calling, the best place to initialize non-static fields is inside the constructor. so that for every instance of the class created the non-static fields are initialized with different values making the class dynamic. 

If you initialize a static field inside a constructor, the value will be overwritten each time an object is created, which is generally not the intended behavior for static fields. 

```csharp
class Sample
{
  int x = 10; // Non-Static Field
  static int y = 20; // Static Field
 
  public Sample(int x)
  {
      this.x = x; // Initialize non-static field with parameter value
      y = y + 10; // This will overwrite static field value each time an object is created
  }
 
  static void Main()
  {   

      Console.WriteLine("Non-Static Field x: " + x); // Error: Cannot access non-static field 'x' in a static context
      Console.WriteLine("Static Field y: " + y); // Valid
      Sample obj = new Sample(10); // Creating an object to access Non-Static Field
      Console.WriteLine("Non-Static Field x via object: " + obj.x); // Valid
      Sample obj2 = new Sample(30);
      Console.WriteLine("Non-Static Field x via obj2: " + obj2.x); // Valid      
      Console.WriteLine("Static Field y after creating two objects: " + y); // y will be 40 now     
  }

}
```
- In the above program x will have different values for different objects created but y will have the same value for all objects created because its a static field.

### Mental Model: Static Field Behavior in Constructor

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    PROGRAM EXECUTION TIMELINE                               │
└─────────────────────────────────────────────────────────────────────────────┘

Step 1: Class Loaded
┌─────────────────────────────────────────┐
│         STATIC AREA (Class Level)       │
│         ┌───────────────────┐           │
│         │   y = 20          │           │
│         └───────────────────┘           │
└─────────────────────────────────────────┘

Step 2: new Sample(10) called
┌─────────────────────────────────────────┐     ┌─────────────────────────────┐
│         STATIC AREA                     │     │   HEAP: obj                 │
│         ┌───────────────────┐           │     │   ┌─────────────────┐       │
│         │   y = 20 + 10     │ ◄─────────┼─────│   │   x = 10        │       │
│         │     = 30          │           │     │   └─────────────────┘       │
│         └───────────────────┘           │     └─────────────────────────────┘
└─────────────────────────────────────────┘

Step 3: new Sample(30) called
┌─────────────────────────────────────────┐     ┌─────────────────────────────┐
│         STATIC AREA                     │     │   HEAP: obj    obj2         │
│         ┌───────────────────┐           │     │   ┌─────┐     ┌─────┐       │
│         │   y = 30 + 10     │ ◄─────────┼─────│   │x=10 │     │x=30 │       │
│         │     = 40          │           │     │   └─────┘     └─────┘       │
│         └───────────────────┘           │     └─────────────────────────────┘
└─────────────────────────────────────────┘


┌─────────────────────────────────────────────────────────────────────────────┐
│                           KEY TAKEAWAY                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   NON-STATIC (x)                     STATIC (y)                             │
│   ┌─────┐ ┌─────┐                    ┌─────────────┐                        │
│   │ 10  │ │ 30  │                    │     40      │                        │
│   └──┬──┘ └──┬──┘                    └──────┬──────┘                        │
│      │       │                              │                               │
│      ▼       ▼                              ▼                               │
│   obj.x   obj2.x                      Sample.y                              │
│                                                                             │
│   ✓ Each object has                  ✗ Only ONE copy                       | 
│     its OWN copy                       shared by ALL                        │
│                                                                             │
│   ✓ Different values                 ✗ Modified by every                   | 
│     per instance                       constructor call                     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Remember:** Static = **S**ingle copy, **S**hared | Non-Static = **N**ew copy per i**N**stance

A class contains four types of fields 
1. Non-Static Field
2. Static Field
3. Constant Field
4. Readonly Field

### Constant Field
A **Constant** field is a field which is declared using `const` keyword. 

Constant fields must be initialized at the time of declaration and their values cannot be changed later.

The behavior of constant fields is similar to static fields in that they are shared across all instances of the class. However, constant fields are implicitly static, meaning you do not need to use the `static` keyword when declaring them. Once you declare a constant field, its value is fixed and cannot be modified. It will be same throughout the lifetime of the program.


```csharp
class Sample
{
  const int z = 30; // Constant Field
 
  static void Main()
  {   
      Console.WriteLine("Constant Field z: " + z); // Valid
      // z = 40; // Error: Cannot modify a constant field
  }

}
```
The only difference between Static field and Constant field is that Static field can be initialized and modified inside a constructor where as Constant field must be initialized at the time of declaration and its value cannot be changed later.

### Readonly Field
A **readonly field** is a field that can only be assigned a value during its declaration or within the constructor of the class in which it is declared. Once assigned, the value of a readonly field cannot be changed.

The difference between a `const` field and a `readonly` field is that a `const` field must be initialized at the time of declaration and its value cannot be changed later, whereas a `readonly` field can be initialized either at the time of declaration or within a constructor, allowing for more flexibility in setting its value.

`constant` fields will have same value throughout the lifetime of the program, whereas `readonly` fields can have different values for different instances of the class if they are initialized in a parameterized constructor.

The behavior of readonly fields is similar to non-static fields in that they can have different values for different instances of the class if initialized in a parameterized constructor. However, once assigned, the value of a readonly field cannot be modified outside of the constructor.


```csharp
class Sample
{
  readonly int r; // Readonly Field

  public Sample(int value)
  {
      r = value; // Initialize readonly field in constructor
  }

  static void Main()
  {   
      Sample obj = new Sample(50);
      Console.WriteLine("Readonly Field r: " + obj.r); // Valid
      // obj.r = 60; // Error: Cannot modify a readonly field outside constructor
  }

}
```

### Mental Model: Four Types of Fields in C#

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                          FIELD TYPES COMPARISON                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────┐
│  FIELD TYPE     │  WHEN INITIALIZED      │  CAN MODIFY?     │  MEMORY LOCATION     │
├─────────────────┼────────────────────────┼──────────────────┼──────────────────────┤
│  Non-Static     │  Object creation       │  ✓ Yes, anytime  │  Heap (per object)   │
│  Static         │  Class loading         │  ✓ Yes, anytime  │  Static area         │
│  Const          │  Declaration only      │  ✗ Never         │  Compiled inline     │
│  Readonly       │  Declaration/Ctor      │  ✗ After ctor    │  Heap/Static         │
└─────────────────┴────────────────────────┴──────────────────┴──────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────┐
│                           VISUAL MEMORY MODEL                                       │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                     │
│   NON-STATIC              STATIC                CONST              READONLY         │
│   ┌─────┐ ┌─────┐        ┌─────┐               ┌─────┐            ┌─────┐           │
│   │ x=5 │ │ x=8 │        │y=20 │               │z=30 │            │r=50 │           │
│   └──┬──┘ └──┬──┘        └──┬──┘               └──┬──┘            └──┬──┘           │
│      │       │              │                     │                  │              │
│   obj1.x   obj2.x      Class.y              Baked into           obj.r             │
│                                              compiled code                          │
│                                                                                     │
│   📦 NEW box            🌍 ONE globe         🔒 LOCKED           🔐 LOCK after     │
│   for each              for everyone         at birth               birth          │
│   customer                                                                          │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────┐
│                          EASY MEMORY TRICKS                                         │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                     │
│   NON-STATIC  →  "Personal Diary"     📓  Each person has their own                │
│                                                                                     │
│   STATIC      →  "Classroom Clock"    🕐  One clock, everyone looks at same        │
│                                                                                     │
│   CONST       →  "Carved in Stone"    🪨  Decided at birth, never changes          │
│                                                                                     │
│   READONLY    →  "Birth Certificate"  📜  Set once at birth, then permanent        │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────┐
│                          QUICK DECISION GUIDE                                       │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                     │
│   "Value different per object?"           → NON-STATIC                              │
│   "Value shared, but may change?"         → STATIC                                  │
│   "Value known at compile time, fixed?"   → CONST                                   │
│   "Value set at runtime, then fixed?"     → READONLY                                │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

**Mnemonic:** **N**ew **S**hared **C**arved **R**egistered → Non-Static, Static, Const, Readonly

### Visual: All Four Field Types with Two Instances

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                     TWO INSTANCES OF Sample CLASS                                   │
└─────────────────────────────────────────────────────────────────────────────────────┘

class Sample
{
    int x = 10;              // Non-Static
    static int y = 20;       // Static
    const int z = 30;        // Constant
    readonly int r;          // Readonly

    public Sample(int val) { r = val; }
}

Sample obj1 = new Sample(100);
Sample obj2 = new Sample(200);

┌─────────────────────────────────────────────────────────────────────────────────────┐
│                              COMPILE TIME                                           │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                     │
│   ┌─────────────────────────────────────────┐                                       │
│   │         CONST: z = 30                   │                                       │
│   │   (Embedded directly in compiled code)  │                                       │
│   │   ┌─────────────────────────────────┐   │                                       │
│   │   │  "30" replaces every 'z' usage  │   │                                       │
│   │   └─────────────────────────────────┘   │                                       │
│   │        NO memory allocation!            │                                       │
│   └─────────────────────────────────────────┘                                       │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────┐
│                              RUNTIME MEMORY                                         │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                     │
│   ┌───────────────────────────────────────────────────────────────────────────┐     │
│   │                    STATIC AREA (Class Level)                              │     │
│   │   ┌─────────────────────────────────────────────────────────────────┐     │     │
│   │   │                      Sample Class                               │     │     │
│   │   │   ┌─────────────────────────────────────────────────────────┐   │     │     │
│   │   │   │   static int y = 20     ◄── ONE COPY for entire class   │   │     │     │
│   │   │   └─────────────────────────────────────────────────────────┘   │     │     │
│   │   │                                                                 │     │     │
│   │   │   • obj1 sees y = 20                                            │     │     │
│   │   │   • obj2 sees y = 20  (same value, same memory)                 │     │     │
│   │   └─────────────────────────────────────────────────────────────────┘     │     │
│   └───────────────────────────────────────────────────────────────────────────┘     │
│                                                                                     │
│   ┌───────────────────────────────────────────────────────────────────────────┐     │
│   │                         HEAP MEMORY (Objects)                             │     │
│   │                                                                           │     │
│   │   ┌─────────────────────────┐     ┌─────────────────────────┐             │     │
│   │   │   obj1 (Instance 1)     │     │   obj2 (Instance 2)     │             │     │
│   │   ├─────────────────────────┤     ├─────────────────────────┤             │     │
│   │   │   x = 10                │     │   x = 10                │             │     │
│   │   │   (Non-Static)          │     │   (Non-Static)          │             │     │
│   │   │   ┌─────────────────┐   │     │   ┌─────────────────┐   │             │     │
│   │   │   │  OWN COPY       │   │     │   │  OWN COPY       │   │             │     │
│   │   │   └─────────────────┘   │     │   └─────────────────┘   │             │     │
│   │   ├─────────────────────────┤     ├─────────────────────────┤             │     │
│   │   │   r = 100               │     │   r = 200               │             │     │
│   │   │   (Readonly)            │     │   (Readonly)            │             │     │
│   │   │   ┌─────────────────┐   │     │   ┌─────────────────┐   │             │     │
│   │   │   │  OWN COPY 🔒    │   │     │   │  OWN COPY 🔒    │   │             │     │
│   │   │   │  (but locked)   │   │     │   │  (but locked)   │   │             │     │
│   │   │   └─────────────────┘   │     │   └─────────────────┘   │             │     │
│   │   └─────────────────────────┘     └─────────────────────────┘             │     │
│   │                                                                           │     │
│   └───────────────────────────────────────────────────────────────────────────┘     │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────┐
│                           COPIES SUMMARY                                            │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                     │
│   FIELD TYPE    │  obj1 VALUE  │  obj2 VALUE  │  TOTAL COPIES  │  CAN DIFFER?      │
│   ──────────────┼──────────────┼──────────────┼────────────────┼───────────────     │
│   Non-Static x  │     10       │     10       │      2         │  ✓ Yes            │
│   Static y      │     20       │     20       │      1         │  ✗ No (shared)    │
│   Const z       │     30       │     30       │      0*        │  ✗ No (inlined)   │
│   Readonly r    │    100       │    200       │      2         │  ✓ Yes            │
│                                                                                     │
│   * Const has 0 runtime copies - value is embedded at compile time                  │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────┐
│                           VISUAL ANALOGY                                            │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                     │
│                    obj1                              obj2                           │
│                   ┌─────┐                           ┌─────┐                         │
│   NON-STATIC  x   │ 📓  │ Personal notebook         │ 📓  │ Different notebook     │
│                   ├─────┤                           ├─────┤                         │
│   READONLY    r   │ 📜  │ Birth cert (100)          │ 📜  │ Birth cert (200)       │
│                   └──┬──┘                           └──┬──┘                         │
│                      │                                 │                            │
│                      │         ┌───────────┐           │                            │
│   STATIC      y      └─────────┤  🕐 = 20  ├───────────┘                            │
│                                │  (shared) │                                        │
│                                └───────────┘                                        │
│                                                                                     │
│   CONST       z                🪨 = 30 (carved into the program itself)             │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘
```