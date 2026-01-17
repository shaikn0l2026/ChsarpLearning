# Calling Class from Other Classes

There are two primary ways to consume methods of one class into another class in C#:
1. **Inheritance**: Creating a new class that derives from an existing class, thereby inheriting its methods and properties.
2. **Object Creation**: Creating an instance (object) of the class and using that object to call its methods.

### 1. Inheritance method
-----------------------  ------------------------



### 2. Object Creation method
----------------------  ------------------------
## Summary
To call a method defined in one class from another class in C#, you need to:
1. **Declare** an object variable of the class type
2. **Initialize** the object using the `new` keyword
3. **Call** the method using the dot (`.`) operator

## Syntax
```csharp
ClassName objectName = new ClassName();
objectName.MethodName();
```

## Example

```csharp
// Class with a method
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }
    
    public void DisplayMessage()
    {
        Console.WriteLine("Hello from Calculator class!");
    }
}

// Another class that uses the Calculator class
public class Program
{
    public static void Main()
    {
        // Step 1 & 2: Declaration and Initialization
        Calculator calc = new Calculator();
        
        // Step 3: Call methods from Calculator class
        calc.DisplayMessage();
        
        int result = calc.Add(10, 20);
        Console.WriteLine($"Sum: {result}");
    }
}
```

## Output
```
Hello from Calculator class!
Sum: 30
```

## Key Points
- The method must be **public** (or accessible) to be called from another class
- You need to create an **instance** (object) of the class to call instance methods
- For **static methods**, you can call directly using the class name without creating an object: `ClassName.StaticMethodName()`

if input is employee id and output is employee name then what is the signature of the method
The signature of the method would be:
```csharp
public string GetEmployeeName(int employeeId)
```
if input is employee name and output is employee id then what is the signature of the method
The signature of the method would be:
```csharp
public int GetEmployeeId(string employeeName)
```
if input is employee id and output is salay of the employee then what is the singature of the method 
The signature of the method would be:
```csharp
public decimal GetEmployeeSalary(int employeeId)
```
if the input is employee id and output is if the employee is active or not then what is the signature of the method
The signature of the method would be:
```csharp
public bool IsEmployeeActive(int employeeId)
```

if the input is employee id and output is employee details then what is the signature of the method
The signature of the method would be:

```csharp

public class Employee
{
    public int Id { get; set; };
    public string Name { get; set; };
    public decimal Salary { get; set; };
    public bool IsActive { get; set; };
    // Other employee details can be added here
}

```
```csharp

public Employee GetEmployeeDetails(int employeeId) //Employee is a user defined class representing employee details
```



