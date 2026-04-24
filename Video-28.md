# DBMS Concepts: Entity-Attribute-Table Model

A table is representation of entity. A entity is a living or non living object with set of attributes. When dealing with application creation you will first identify the entities of that application, then you will find the attributes of that entities. Create a table in DB, each table in DB will be each entity and all the columns are attributes of that entity. And each record you enter will be unique value of that entity.

## Mental Model Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    APPLICATION DOMAIN                           │
│                                                                 
│  ┌──────────────┐        ┌──────────────┐      ┌──────────────┐ │
│  │   ENTITY 1   │        │   ENTITY 2   │      │   ENTITY 3   │ │
│  │   (Student)  │        │   (Course)   │      │  (Teacher)   │ │
│  │              │        │              │      │              │ │
│  │  Attributes: │        │  Attributes: │      │  Attributes: │ │
│  │  • ID        │        │  • Code      │      │  • EmpID     │ │
│  │  • Name      │        │  • Name      │      │  • Name      │ │
│  │  • Age       │        │  • Credits   │      │  • Subject   │ │
│  │  • Email     │        │  • Duration  │      │  • Salary    │ │
│  └──────┬───────┘        └──────┬───────┘      └──────┬───────┘ │
│         │                       │                     │         │
│         │ Maps to               │ Maps to             │ Maps to │
│         ▼                       ▼                     ▼         │
└─────────────────────────────────────────────────────────────────┘
          │                       │                     │
          ▼                       ▼                     ▼
┌─────────────────────────────────────────────────────────────────┐
│                      DATABASE SCHEMA                            │
│                                                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  TABLE: Students                                         │   │
│  ├──────────┬────────────┬─────────┬─────────────────────┐  │   │
│  │   ID     │    Name    │   Age   │       Email         │  │   │
│  │ (Column) │  (Column)  │(Column) │     (Column)        │  │   │
│  ├══════════╪════════════╪═════════╪═════════════════════┤  │   │
│  │   101    │   Alice    │   20    │ alice@email.com     │◄─┼───┤ Record 1
│  │   102    │   Bob      │   22    │ bob@email.com       │◄─┼───┤ Record 2
│  │   103    │   Charlie  │   19    │ charlie@email.com   │◄─┼───┤ Record 3
│  └──────────┴────────────┴─────────┴─────────────────────┘  │   │
│                                                             │   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  TABLE: Courses                                          │   │
│  ├──────────┬────────────┬──────────┬───────────────────┐   │   │
│  │   Code   │    Name    │ Credits  │    Duration       │   │   │
│  ├══════════╪════════════╪══════════╪═══════════════════┤   │   │
│  │   CS101  │   DBMS     │    4     │   15 weeks        │   │   │
│  │   CS102  │   DSA      │    3     │   12 weeks        │   │   │
│  └──────────┴────────────┴──────────┴───────────────────┘   │   │
└─────────────────────────────────────────────────────────────────┘

KEY CONCEPTS:
═══════════════════════════════════════════════════════════════════

    ENTITY              →    TABLE
    (Real-world object)      (Database structure)

    ATTRIBUTES          →    COLUMNS
    (Properties)             (Field definitions)

    INSTANCE            →    RECORD/ROW
    (Specific object)        (Data entry)


VISUAL LEGEND:
══════════════

    ┌───── ┐
    │Entity│  →  Living/Non-living object in your domain
    └───── ┘

    ┌──────────────────┐
    │  Table Header    │  →  Column names (Attributes)
    ├══════════════════┤
    │  Data Row        │  →  Each row = One unique instance
    └──────────────────┘
```

## Summary

This diagram illustrates how real-world entities (like Student, Course, Teacher) with their attributes (properties) map directly to database tables where:
- Each **column** represents an **attribute**
- Each **row** represents a **unique instance** of that entity

By following this model, you can effectively design a database schema that accurately reflects the structure of your application domain.

---

# OOP Concepts: Entity-Class-Object Model

Just like in the database model above, in application development using Object-Oriented Programming (OOP), every entity becomes a **class**, every attribute becomes a **field** (or property), and every instance of a class becomes a **unique object** representing that entity.

## OOP Mental Model Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    APPLICATION DOMAIN                           │
│                                                                 │
│  ┌──────────────┐        ┌──────────────┐      ┌──────────────┐ │
│  │   ENTITY 1   │        │   ENTITY 2   │      │   ENTITY 3   │ │
│  │   (Student)  │        │   (Course)   │      │  (Teacher)   │ │
│  │              │        │              │      │              │ │
│  │  Attributes: │        │  Attributes: │      │  Attributes: │ │
│  │  • ID        │        │  • Code      │      │  • EmpID     │ │
│  │  • Name      │        │  • Name      │      │  • Name      │ │
│  │  • Age       │        │  • Credits   │      │  • Subject   │ │
│  │  • Email     │        │  • Duration  │      │  • Salary    │ │
│  └──────┬───────┘        └──────┬───────┘      └──────┬───────┘ │
│         │                       │                     │         │
│         │ Maps to               │ Maps to             │ Maps to │
│         ▼                       ▼                     ▼         │
└─────────────────────────────────────────────────────────────────┘
          │                       │                     │
          ▼                       ▼                     ▼
┌─────────────────────────────────────────────────────────────────┐
│                      OOP CLASS DESIGN                           │
│                                                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  CLASS: Student                                          │   │
│  ├──────────────────────────────────────────────────────────┤   │
│  │  FIELDS/PROPERTIES:                                      │   │
│  │  • int ID                                                │   │
│  │  • string Name                                           │   │
│  │  • int Age                                               │   │
│  │  • string Email                                          │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                 │
│  INSTANCES (Objects):                                           │
│  ┌─────────────────────────────────────────────────┐            │
│  │ student1 = new Student()                        │            │
│  │   ID = 101, Name = "Alice",                     │◄───────────┼─ Object 1
│  │   Age = 20, Email = "alice@email.com"           │            │
│  └─────────────────────────────────────────────────┘            │
│                                                                 │
│  ┌─────────────────────────────────────────────────┐            │
│  │ student2 = new Student()                        │            │
│  │   ID = 102, Name = "Bob",                       │◄───────────┼─ Object 2
│  │   Age = 22, Email = "bob@email.com"             │            │
│  └─────────────────────────────────────────────────┘            │
│                                                                 │
│  ┌─────────────────────────────────────────────────┐            │
│  │ student3 = new Student()                        │            │
│  │   ID = 103, Name = "Charlie",                   │◄───────────┼─ Object 3
│  │   Age = 19, Email = "charlie@email.com"         │            │
│  └─────────────────────────────────────────────────┘            │
│                                                                 │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  CLASS: Course                                           │   │
│  ├──────────────────────────────────────────────────────────┤   │
│  │  FIELDS/PROPERTIES:                                      │   │
│  │  • string Code                                           │   │
│  │  • string Name                                           │   │
│  │  • int Credits                                           │   │
│  │  • string Duration                                       │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                 │
│  INSTANCES (Objects):                                           │
│  ┌─────────────────────────────────────────────────┐            │
│  │ course1 = new Course()                          │            │
│  │   Code = "CS101", Name = "DBMS",                │◄───────────┼─ Object 1
│  │   Credits = 4, Duration = "15 weeks"            │            │
│  └─────────────────────────────────────────────────┘            │
└─────────────────────────────────────────────────────────────────┘

KEY CONCEPTS IN OOP:
═══════════════════════════════════════════════════════════════════

    ENTITY              →    CLASS
    (Real-world object)      (Blueprint/Template)

    ATTRIBUTES          →    FIELDS/PROPERTIES
    (Properties)             (Variables in class)

    INSTANCE            →    OBJECT
    (Specific object)        (Actual memory allocation)


VISUAL LEGEND:
══════════════

    ┌───────────────┐
    │ CLASS         │  →  Blueprint defining structure
    │ ┌───────────┐ │
    │ │  Fields   │ │  →  Data members (attributes)
    │ └───────────┘ │
    └───────────────┘

    ┌───────────────┐
    │  object1      │  →  Instance with actual values
    │  (Instance)   │
    └───────────────┘
```

## Comparison: Database vs OOP

| Concept | Database | OOP Application |
|---------|----------|-----------------|
| **Entity** | Table | Class |
| **Attribute** | Column | Field/Property |
| **Instance** | Record/Row | Object |
| **Unique ID** | Primary Key | Object Reference |

## Code Example in C#

```csharp
// Entity: Student → Class: Student
public class Student
{
    // Attributes → Fields/Properties
    public int ID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
    public string Email { get; set; }
}

// Creating Instances → Objects with unique identifiers
Student student1 = new Student 
{ 
    ID = 101, 
    Name = "Alice", 
    Age = 20, 
    Email = "alice@email.com" 
};

Student student2 = new Student 
{ 
    ID = 102, 
    Name = "Bob", 
    Age = 22, 
    Email = "bob@email.com" 
};

// Each object (student1, student2) is a unique instance representing
// a specific student entity with its own set of attribute values
```

## Summary

In application development with OOP:
- **Every Entity** in your domain becomes a **Class** in your code
- **Every Attribute** of an entity becomes a **Field or Property** in the class
- **Every Instance** of the class becomes a **unique Object** with its own identifier and state

This parallel structure between databases and OOP makes it natural to:
1. Design your domain entities
2. Create corresponding classes in your application
3. Store instances in database tables
4. Retrieve database records as objects in your application

This is the foundation of **Object-Relational Mapping (ORM)** patterns used in modern application development!

# ATM Application Example
Consider an ATM application where we have entities like User, Account, and Transaction.

Step 1: Identify Entities ==========> Customer 
Step 2: Identify Attributes ==========> Customer (CustomerID, Name, Balance)
Step 3: Databse design 

TABLE: Customers
| CustomerID | Name       | Balance  |
|------------|------------|----------|
| 1001       | John Doe   | 5000.00  |  
| 1002       | Jane Smith | 3000.00  |
| 1003       | Alice Brown| 7000.00  |
| 1004       | Bob White  | 4500.00  |

Step 4: OOP Class Design

   - Define Class Customer
   - Define Fields/Properties: CustomerID, Name, Balance

      public class Customer
      {
          public int CustomerID 
          public string Name 
          public decimal Balance 

          public Customer(int CustomerID)
            {
                this.CustomerID = CustomerID;
                //Connect to DB and fetch other details 
                this.Name = Load <Name> value based on CustomerID from DB Table 
                this.Balance = Load <Balance> value based on CustomerID from DB Table
            }

      }





