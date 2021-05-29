# Notes on Kotlin

Link to the course: https://www.udemy.com/course/kotlin-for-java-developers/

## Getting to know Kotlin

### Facts Kotlin
- runs on the JVM
- statically typed
- OOP 
- functional programming

### Guiding Principles: 
- conciseness (less code for same functionality in Java)
- safety (protect against null pointer exceptions ) 
- pragmatic (serves to solve real-world problem, more ways to solve one problem)- interoperability w/ Java  

### Kotlin vs Java 
- more concise  
- protection against nullpointers

#### How it is compiled 
- kotlinc (compiler) takes .kt files and generates bytecode in .class files 
- the JVM can run the .class files 
- to run kotlin apps we need a kotlin runtime

#### Variable declarations

**top-level function**: no need to define func in a class -> the compiler does that under the hood

**val**: like final keyword = set once, then immutable 

**var**: mutable variable 

-> **always use val unless you have a good reason not to** 


```
class Employee(var name: String, val id: Int) {
}

val employee1 = Employee("Jennifer Parak", 500)
// immutable instance can have mutable instance variables
employee.name = "Jennifer Something"
// but we cannot reassign 
// COMPILE ERROR
employee1 = Employee("Tim Watson", 100)
```

#### Type aliases
= letting you use another name for an existing type e.g. if you're using `StringBuilder` you will actually use `java.lang.StringBuilder` 

```
typealias EmployeeSet = Set<Employee>

val employees: EmployeeSet

class Employee(var name: String, val id: Int) {
}
```

#### Quick Differences: Kotlin vs Java
- no semicolons
- use of wrappers (e.g `println` instead of `System.out.println`)
- soft keywords
	- in Java you cannot use a reserved keyword for anything else such as a variable name 
	- soft keywords are allowed to be used 
- use [ ] to access indices from collections 

```
val names = arrayListOf("John", "Jane", "Mary")
println(names[1])
```
- kotlin has its own string class 
- kotlin doesn't have a ternary operator 
- there's no for loop in kotlin as we know it from java 
- static keyword is gone syntectically (still exists under the hood) 

#### Equality in Kotlin 

in Java: 
- `==` looking for referential equality, true if both instances are the same
- `.equals` if content is equal 

in Kotlin: 
- `===` looks for referential equality
- `==` and `.equals` will check for equal content

### Data Types
- same built in types as in Java 
- Arrays
```
// initialise the array -> no need to specify the type if initliased with values
val names = arrayOf("John", "Jane", "Jill", "Joe")

// need to specify long, otherways we would get an array of Ints 
val longs2 = arrayOf<Long>(1, 2, 3, 4)

// initialise an array with 16 elements with even numbers
val evenNumbers = Array(16) { i -> i * 2  } 

// initialise an array with 100 elements of 0's 
val allZeroes = Array(100) { 0 } 

var someArray: Array<Int> 
someArray = arrayOf(1, 2, 3, 4)
```

**Note** : If you want to call a primitive type array in Java, you need to use a specific array that maps to the specific primitive type -> better performance if you use them if you're using primitive types

```
// better to use primitive type arrays 
var someOtherArray = IntArray(5)
```

#### Null References 

Kotlin has the notion of *nullable* types

```
// COMPILER ERROR
val str: String = null

// do this to make it nullable 
val str: String? = null

val str: String? = "test"
str?.toUpperCase() // to check if str is null and only if it isn't it will run toUpperCase()

// set a default value if a value is null -> ELVIS OPERATOR
val str2 = str ?: "This is the default value" 

// safe cast 
val something: Any = arrayOf(1, 2, 3, 4) 
val str3 = something as? String
println(str3) // null
println(str3?.toUpperCase()) // null

// if you want a null exception to be thrown 
val str4 = str!!.toUpperCase()

// use let in case you wanna call a lamdba function in case str isnt null
str?.let { printText(it) }
```