# C# Programming Concepts Glossary

## Compilation & Execution Models

| Language | Compilation Process | Output |
|----------|-------------------|--------|
| C, C++ | Compiled directly to machine code | Platform-dependent executable |
| C#, Java, Python | Compiled to intermediate code (bytecode) | Platform-independent bytecode (interpreted/JIT) |

### Runtime Environments

- **C/C++**: No runtime environment
- **Java**: JVM (Java Virtual Machine)
- **C#**: CLR (Common Language Runtime)

---

## Types & Classes

**Class** = **Type** = Blueprint for creating objects

### Type Categories

```
Types
├── Predefined Types
│   ├── Value Types: int, float, double, char, struct, enum
│   └── Reference Types: string, object, class, interface
└── User-Defined Types
    ├── class
    ├── struct
    ├── enum
    └── interface
```

---

## Memory Management

| Type | Memory Location | Examples |
|------|----------------|----------|
| **Value Types** | Stack | int, float, double, char, struct, enum |
| **Reference Types** | Heap | string, object, class, interface |

---

## Static vs Non-Static

| Modifier | Memory Allocation | Scope | Copies |
|----------|------------------|-------|--------|
| **Static** | Once (at class load) | Belongs to the class | Single copy shared by all instances |
| **Non-Static** | Per instance | Belongs to each instance | Unique copy per instance |

Static means belongs to class, non-static means belongs to instance/object.

---

## Scope: Fields vs Variables

| Concept | Scope | Location | Declaration Context |
|---------|-------|----------|-------------------|
| **Fields** | Global/Class/Namespace | Outside methods (class level) | Before `Main()` method |
| **Variables** | Local/Method/Block | Inside methods or blocks | Within method body |

## Fields, Static Fields, Non-Static Fields, Constants, Readonly Fields
| Field Type | Memory Location | Mutability | Declaration Context |
|------------|----------------|------------|---------------------|
| **Static Fields** | Static memory (once per class) | Mutable | Declared with
| **Non-Static Fields** | Instance memory (per object) | Mutable | Declared without static |
| **Constants** | Static memory (once per class) | Immutable (compile-time) | Declared with `const` |
| **Readonly Fields** | Instance memory (per object) | Immutable (runtime) | Declared with `readonly` | `static` |

---

## Member Access Rules

### Accessing Members from SAME Class

| Member Type → Block Type | Access |
|---------------------------|--------|
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

---

## Constructor Types in C#

The main job of Constructor is to initialize Fields 

| Constructor Type | Syntax | When to Use | Key Characteristics | Called |
|-----------------|--------|-------------|---------------------|--------|
| **Default** | `public MyClass() { }` | Basic object creation with default values | Parameterless; auto-generated if no constructor defined | Implicitly (auto-generated) / Explicitly (if defined) |
| **Parameterized** | `public MyClass(int x, string y) { }` | Initialize object with specific values | Takes parameters to set fields/properties | Explicitly |
| **Static** | `static MyClass() { }` | Initialize static members, one-time setup | Runs once; no access modifier; no parameters | Implicitly (by CLR) |
| **Private** | `private MyClass() { }` | Singleton pattern; prevent instantiation | Restricts object creation from outside | Explicitly (from within class only) |

### How Many Constructors Can a Class Have?

| Constructor Type | Count Allowed |
|-----------------|---------------|
| **Static** | Only 1 (cannot overload) |
| **Instance** (Default, Parameterized, Private) | Unlimited (can overload with different parameters) |

