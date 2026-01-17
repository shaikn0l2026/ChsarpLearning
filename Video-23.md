## Code files in a project

When adding a new class to a project, use the "Add New Item" window and choose the "Class" item template. That creates a file with a class template. The "Code File" item template creates a blank file where you must write everything manually.

## Defining multiple classes in a file
It's possible to define multiple classes in a single `.cs` file. The `Main` method can be defined in only one class. While not mandatory, it's recommended to name the file after the class that contains `Main`.

## User-defined return types for methods
A method's return type can be any user-defined type (a class, struct, record, etc.), allowing methods to return complex data.

Example — add a `Code File` named `UserDefinedTypes.cs` and paste:

```csharp
namespace Oopsproject
{
    internal class Employee
    {
        public int? Id;
        public string? Name;
        public string? Job;
        public double? Salary;
    }

    internal class UserDefinedTypes
    {
        public Employee GetEmployeeData(int id)
        {
            var obj = new Employee
            {
                Id = id,
                Name = "Suresh",
                Job = "Manager",
                Salary = 50000
            };
            return obj;
        }

        static void Main()
        {
            var ud = new UserDefinedTypes();
            Employee emp = ud.GetEmployeeData(1);
            Console.WriteLine("ID: " + emp.Id);
            Console.WriteLine("Name: " + emp.Name);
            Console.WriteLine("Job: " + emp.Job);
            Console.WriteLine("Salary: " + emp.Salary);
        }
    }
}
```

## How to pass parameters to a method in a class
Syntax:
```
[<access>] <return-type> MethodName(<param-list>) { ... }
```
Parameter form: `<type> <name>` (comma-separated)

Three main ways to pass parameters in C#:
1. Input parameters (by value) — default behavior.
2. Output parameters (by reference) — using `out`.
3. Input/output parameters (by reference) — using `ref`.

### Why use `out` parameters?
- A method can return only one value directly. Use `out` to return additional values without creating a container type.
- Alternatively, return a tuple or a container object.

Example — unreachable code with multiple `return` statements:
```csharp
public int Math(int x, int y)
{
    int sum = x + y;
    int product = x * y;
    return sum;
    return product; // unreachable
}
```

Use `out` or tuple returns instead:
```csharp
// out parameters
public void MathOut(int x, int y, out int sum, out int product)
{
    sum = x + y;
    product = x * y;
}

// Until C# 7.0, use out parameters; from C# 7.0 onwards, prefer tuples because before C# 7.0, tuples were not natively supported.only one return type allowed. from C# 7.0 onwards, multiple return types allowed using tuples.
// tuple return
public (int Sum, int Product) MathTuple(int x, int y)
{
    return (x + y, x * y);
}
```

## Examples — parameter types
1) Simple input (by value)
```csharp
class Calculator { public int Add(int a, int b) => a + b; }
```

2) Default parameters
```csharp
public int Multiply(int x, int y = 2) => x * y;
```

3) params (variable number)
```csharp
public int Sum(params int[] numbers) => numbers.Sum();
```

4) ref and out
```csharp
void Increment(ref int value) { value++; }       // in/out
void GetCoordinates(out int x, out int y) { x = 0; y = 0; } // out
```

5) Reference types (objects)
```csharp
class Person { public string Name; }
void Rename(Person p) { p.Name = "Alex"; } // modifies same instance
```

6) Named arguments
```csharp
int result = calc.Add(b: 5, a: 2);
```

Notes:
- Value types are copied by default; use `ref`/`out` to modify the caller's variable.
- Reference types pass a reference to the object; modifying members affects the same instance.
- Default parameter values must follow non-default parameters.
- Use `params` for variable-length argument lists.
- Use named arguments for clarity or to change argument order.
