# Static vs Non-Static Methods 

By default every method is non-static, to make a method static we need to use `static` keyword while declaring the method.

## Member Access Rules

### Accessing Members from SAME Class

| Member Type | Block Type | Access |
|-------------|------------|--------|
| Static Member → Static Block | ✅ Direct Access |
| Static Member → Non-Static Block | ✅ Direct Access |
| Non-Static Member → Non-Static Block | ✅ Direct Access |
| Non-Static Member → Static Block | ❌ Requires instance |

### Accessing Members from ANOTHER Class

| Member Type | How to Access |
|-------------|---------------|
| Non-Static Members | Use instance (object) |
| Static Members | Use class name |

## this Keyword

Use `this` only when there is a naming conflict between class fields and method parameters or local variables. 

Example:
```csharp
class Sample {
    int value; // class field

    void SetValue(int value) { // method parameter
        this.value = value; // 'this' refers to class field
    }
}
```
# Static vs Non-Static Constructors

By default every constructor is non-static, to make a constructor static we need to use `static` keyword while declaring the constructor.

We know that cosntructors must be explicitly called for execution but this rule is only applicable for non-static constructors. Static constructors are called automatically by the .NET runtime before the first instance is created or any static members are referenced.

for example:

```csharp
class Example {
    private static int counter;

    // Static constructor - called once automatically
    static Example() {
        counter = 0;
        Console.WriteLine("Static constructor called");
    }

    // Non-static constructor - called when creating new instance
    public Example() {
        counter++;
        Console.WriteLine($"Instance constructor called. Count: {counter}");
    }

    static void Main() {
        Example obj1 = new Example();
        // Output:
        // Static constructor called
        // Instance constructor called. Count: 1
        
        Example obj2 = new Example();
        // Output:
        // Instance constructor called. Count: 2
    }
}
```

**Key Points:**

## Non-Static Constructor Vs Static Constructor

- A Constructor if explicitly declared by using static modifier is a static Constructor whereas rest of the other are non-static only and till now every Constructor, we defined is non-static only.

- Static Constructors are implicitly called whereas non-static Constructors must be explicitly called.

- As we are aware that Constructors are responsible for initializing fields in a class; Non-Static Constructor will initialize Non-Static and Readonly Fields, whereas Static Constructor will initialize Static and Constant fields.

- Static Constructor executes immediately once the execution of class starts and more over it is the first block of code to execute in a class, whereas Non-Static Constructor gets executed only after creating the instance of class as well as each and every time a new instance is created i.e., Static Constructor executes 1 and only 1 time in the life cycle of a class whereas Non-Static Constructor get executed for "0" times if no instances are created and "n" times if "n" instances are created.

- Static Constructor can't be parameterized because they are implicitly called and more over it's the first block of code to execute in a class, so we don't have any chance of sending values to its parameter's whereas parameterized Non-Static Constructors can be defined.

### Note: Implicit Constructor Rules

Every class will contain an implicit constructor if not defined explicitly and those implicit constructors are defined based on the following criteria:

1. Non-static constructor will be defined in every class except in a static class.
2. Static constructor will be defined only if the class contains any static fields.

#### Case 1
```csharp
class Test
{
}
```
*After compilation there will be a non-static constructor in class.*

#### Case 2
```csharp
class Test
{
    int i = 10;
}
```
*After compilation there will be a non-static constructor in class.*

#### Case 3
```csharp
class Test
{
    static int i = 100;
}
```
*After compilation there will be both static and non-static constructors also.*

#### Case 4
```csharp
static class Test
{
}
```
*After compilation there will not be any constructor in class.*

#### Case 5
```csharp
static class Test
{
    static int i = 100;
}
```
*After compilation there will be a static constructor in class.*

## Static Class

These are introduced in C# 2.0. If a class is explicitly declared by using static modifier, we call it as a static class and this class can contain only static members in it. We can't create the instance of static class and more over it is not required also.

```csharp
static class Class1
{
    //Define only static members here.
}
```

**Note:** Console is a static class in our Libraries so every member of Console class is a static member only and to check that, right click on Console class in Visual Studio and choose the option "Go to definition" which will open "Metadata" or "Source Code" of that class.

