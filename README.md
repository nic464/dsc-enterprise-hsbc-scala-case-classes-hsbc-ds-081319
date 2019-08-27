
# Case Classes

## About Case Classes

* `case class`
  * Automatically creates a toString implementation
  * Automatically creates a hashCode implementation
  * Automatically creates a equals implementation
  * Automatically creates a copy implementation
  * Automatically sets up pattern matching based on the primary constructor
  * Gives us the ability to instantiate the classes without `new`
  * Makes all member variables a val
* A child class or parent class can be a case class **_but not both_**

## `case class` and automatic `toString`

Before:


```scala
class Employee(firstName:String, lastName:String)

val e = new Employee("Desmond", "Everett")
println(e)
```

    $line68.$read$$iw$$iw$Employee@2f580304
    




    defined class Employee
    e: Employee = Employee@2f580304
    warning: previously defined object Employee is not a companion to class Employee.
    Companions must be defined together; you may wish to use :paste mode for this.
    



After:


```scala
case class Employee(firstName:String, lastName:String)

val e = new Employee("Desmond", "Everett")
println(e)
```

    Employee(Desmond,Everett)
    




    defined class Employee
    e: Employee = Employee(Desmond,Everett)
    



## `case class` and automatic `hashCode`

Before:


```scala
class Employee(firstName:String, lastName:String)

val e1 = new Employee("Desmond", "Everett")
val e2 = new Employee("Desmond", "Everett")
println(e1.hashCode)
println(e2.hashCode)
```

    1619112567
    2010550115
    




    defined class Employee
    e1: Employee = Employee@6081b277
    e2: Employee = Employee@77d68f63
    warning: previously defined object Employee is not a companion to class Employee.
    Companions must be defined together; you may wish to use :paste mode for this.
    



After:


```scala
case class Employee(firstName:String, lastName:String)

val e1 = new Employee("Desmond", "Everett")
val e2 = new Employee("Desmond", "Everett")
println(e1.hashCode)
println(e2.hashCode)
```

    -2009758914
    -2009758914
    




    defined class Employee
    e1: Employee = Employee(Desmond,Everett)
    e2: Employee = Employee(Desmond,Everett)
    



## `case class` and automatic `equals`

Before:


```scala
class Employee(firstName:String, lastName:String)

val e1 = new Employee("Desmond", "Everett")
val e2 = new Employee("Desmond", "Everett")
println(e1 == e2) //same as equals in Java
```

    false
    




    defined class Employee
    e1: Employee = Employee@226c49dc
    e2: Employee = Employee@195d5c6b
    warning: previously defined object Employee is not a companion to class Employee.
    Companions must be defined together; you may wish to use :paste mode for this.
    



After:


```scala
case class Employee(firstName:String, lastName:String)

val e1 = new Employee("Desmond", "Everett")
val e2 = new Employee("Desmond", "Everett")
println(e1 == e2)
```

    true
    




    defined class Employee
    e1: Employee = Employee(Desmond,Everett)
    e2: Employee = Employee(Desmond,Everett)
    



## `case class` and automatic pattern matching

The following uses destructuring to take apart the elements for pattern matching


```scala
case class Employee(firstName:String, lastName:String)

val Employee(fn, ln) = new Employee("Desmond", "Everett")
println(fn)
println(ln)
```

    Desmond
    Everett
    




    defined class Employee
    fn: String = Desmond
    ln: String = Everett
    



## `case class` and `new` not required

Notice in the following that the `new` keyword is not required

There is a subtle trick that is happening that we will see later on.


```scala
case class Employee(firstName:String, lastName:String)

val emp = Employee("Desmond", "Everett")
```




    defined class Employee
    emp: Employee = Employee(Desmond,Everett)
    



## `case class` and `val` not required

* There is no requirement for `val` on a member variable when using a `case class`
* A Scala-Style getter is automatically created


```scala
case class Employee(firstName:String, lastName:String)

val emp = Employee("Desmond", "Everett")
println(emp.firstName)
println(emp.lastName)
```

    Desmond
    Everett
    




    defined class Employee
    emp: Employee = Employee(Desmond,Everett)
    



## `case class` and `copy`

Since `Employee` is immutable, `copy` will create `copy` of the object with new values

Simply name the properties you are changing


```scala
case class Employee(firstName:String, lastName:String)

val emp = Employee("Desmond", "Everett")
val empCopy = emp.copy(lastName = "Gillespie")
println(empCopy)
```

    Employee(Desmond,Gillespie)
    




    defined class Employee
    emp: Employee = Employee(Desmond,Everett)
    empCopy: Employee = Employee(Desmond,Gillespie)
    



## Case Classes Conclusion

* Automatically creates a `toString` implementation
* Automatically creates a `hashCode` implementation
* Automatically creates a `equals` implementation
* Automatically sets up pattern matching based on the primary constructor
* Gives us the ability to instantiate without `new`
* Makes all member variables a `val`
* Provides a `copy` method to generate a `copy`
* A child class or parent class can be a `case class` but not both
