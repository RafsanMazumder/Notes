# Head First Java
## [Chapter-1] Breaking the Surface
### The way Java works
* **Source**: Create a source document. Use an established protocol. (In this case, the Java language)
* **Compiler**: Run your document through a source code compiler. The compiler checks for errors and won't let you compile unless it's satisfied that everything will run correctly.
* **Output (Code)**: The compiler creates a new document coded into Java bytecode. Any device capable of running Java will be able to interpret/translate this file into something it can run. The compiled bytecode is platform independent. 
* **Virtual Machines**: The virtual machines reads and runs the bytecode.
<br/><br/>
![Flow](flow.drawio.svg)

### Compaitability between boolean and int
* Not compaitable in Java

### Static vs Dynamic Binding
1. Static binding in Java occurs during compile time while dynamic binding occurs during runtime. 
2. **private**, **final** and **static** methods and variables use static bonding and are bounded by compiler while virtual methods are bonded during runtime based upon runtime object. 
3. Static bonding uses **Type** (**class** in Java) information for binding while dynamic binding uses object to resolve binding. 
4. Overloaded methods are bonded using static binding while overriden methods are bonded using dynamic binding at runtime. 

#### Static binding example in Java
```java
public class StaticBindingTest {  
    public static void main(String args[]) {
        Collection c = new HashSet();
        StaticBindingTest et = new StaticBindingTest();
        et.sort(c);
    }
    //overloaded method takes Collection argument
    public Collection sort(Collection c) {
        System.out.println("Inside Collection sort method");
        return c;
    }
    //another overloaded method which takes HashSet argument which is sub class
    public Collection sort(HashSet hs) {
        System.out.println("Inside HashSet sort method");
        return hs;
    }
}
```
#### Dynamic binding example in Java
```java
public class DynamicBindingTest {   
    public static void main(String args[]) {
        Vehicle vehicle = new Car(); //here Type is vehicle but object will be Car
        vehicle.start(); //Car's start called because start() is overridden method
    }
}

class Vehicle {
    public void start() {
        System.out.println("Inside start method of Vehicle");
    }
}

class Car extends Vehicle {
    @Override
    public void start() {
        System.out.println("Inside start method of Car");
    }
}
```
### Is JVM compiler or interpreter?
JVM runs/interprets/translates bytecode into native machine code. JVM is interpreter.

## [Chapter-2] A Trip to Objectville
### Difference between Class and Object
* A class is a blueprint for an object. It tells the virtual machine to make an object of that particular type. 
* Things an object knows about itself are called instance variables / state.
* Things an object can do are called methods.

### Garbage Collectible Heap
Each time an object is created in Java, it goes into an area of memory known as the 'the heap'. All objects no matter when, where or how they're created, live on the heap. The Java heap is actually called the Garbage-Collectible Heap. When you create an object, Java allocates memory space on the heap according to how much that particular object needs.<br/><br/>
When the JVM can 'see' that an object can never be used again, that object becomes eligible for garbage collection. And if you're runnning low on memory, the garbage collector will run, throw the unreachable objects, and free up the space, so that the space can be reused.

### Global Variables & Constants
* **public static** -> global variable
* **public static final** -> global constant

## [Chapter-3] Know Your Variables
### Primitive and Reference Variables
* Variables are of two types: primitive and reference
* Variables must always be declared with a name and a type.
* A primitive variable value is the bits representing the value.
* A reference varibale value is the bits representing a way to get to an object on the heap.
* A reference variable has a value of null when it is not referencing any object.
* An array is always an object, even if the array is declared to hold primitives. 

### Bit Depth of Primitive Types
<table><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>Type</span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>Bit Depth</span></p></div></div></td></tr><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>boolean</span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>JVM specific</span></p></div></div></td></tr><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>char</span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>16 bits</span></p></div></div></td></tr><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>byte</span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>8 bits</span></p></div></div></td></tr><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>short</span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>16 bits</span></p></div></div></td></tr><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>int</span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>32 bits</span></p></div></div></td></tr><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>long </span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>64 bits</span></p></div></div></td></tr><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>float </span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>32 bits</span></p></div></div></td></tr><tr><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>double </span></p></div></div></td><td class="selected" style="text-align: left; vertical-align: top;"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>64 bits</span></p></div></div></td></tr></table>

### 'f' Suffix for Float
Floats should have 'f' suffix, because Java thinks anything with a floating point is a double, unless you use 'f'.

### Type Casting
#### Widening / Implicit casting
Both types are compaitable and target type is larger than source type. 
```java
    byte i = 40;
    short j = i;
```
#### Narrowing / Explicit casting
Assigning a larget type to smaller type.
```java
    double d = 30.0;
    float f = d;
```

### Variable Naming
* Start with a letter, underscore(_) or dollar sign($). Can't start with number or other charcters. 
* Cannot be reserved keywords. 

### Size of Reference Variables
All references for a given JVM will be the same size regardless of the objects they reference, but each 
JVM might have a different way of representing references, so references on one JVM may be smaller or
larger than references on another JVM.

### Storing variables on Stack/Heap
* All data for primitive type variables is stored on the stack.
* For reference type, the stack holds a pointer to the object on the heap.
* When setting a reference type variable equal to another reference type variable,
a copy of only the pointer is made.
* Certain object types (e.g. **Immutable**) can't be manipulated on the heap.

```java
    int a = 3;
    int b = a;

    int[] c = {1, 2, 3, 4};
    int[] d = c;
```
![Storing Variables](storing.drawio.svg)

## [Chapter-4] How Objects Behave

### Pass by value or pass by reference?
Java is always pass by value

### Do I have to return the exact type I declared?
You can return anything that can be implicitly promoted to that type. You must use an explicit cast when
 the declared type is smaller than what you're trying to return.

### Encapsulation
* Mark instance variables private
* Mark getters and setters public

### Instance and Local Variables
* Instance variables are declared inside a class but not within a method.
* Local variables are declared within a method. 
* Local variables do not get a default value. So local variables must be initialized before use. 
* Method parameters are the same as local variables, as they're declared inside the method.

### Comparing Variables
* **Primitives**: To comapre two primitives, use the **==** operator.
* **References**: To see if two references are the same (which means if they refer to the same object on the heap)
 use the **==** operator.

## [Chapter-6] Using the Java Library
### Packages
In the Java Libray/API, classes are grouped into packages. To use a class in the API, you have to know which package the class is in. 
Every class in the Java library belongs to a package. 

![Package](package.drawio.svg)

### Why do we have to use the full name of a package?
* Better organization of a project or library
* Name scoping, to help prevent collisions
* Level of security, because you can restrict the code you write so that only classes in the same package can access it. 

### What does it mean when a package starts with **javax**?
* In the first and second versions of Java, all classes that shipped with Java were in packages, that begin with **java**.
e.g. **java.lang**, **java.util**, **java.net**
* There are other packages not included in the standard library. These classes were known as extensions and two types: 
Standard and non-standard. Standard extensions were those that **Sun** considered official, as opposed to experimental.
* Standard extensions, by convention, all began with an **'x'** appended to the regular java package starter. e.g. **javax.swing**

### **java.lang** package
You must tell Java the full name of every class you use, unless that class is in the **java.lang** package. An import
statement for the class is the easy way. Otherwise, you have to type the full name of the class, everywhere you use it.

## [Chapter-7] Better Living in Objectville
### What if JVM cannot find the method in the inheritence tree?
The compiler gurantees that a particular method is callable for a specific reference type, but it doesn't say/care
from which class that method actually comes from at runtime. 

### Using both superclass & subclass method
```java
    public void roam() {
        super.roam();
        // my own roam stuff
    }
```

### Subclass & Superclass
* A subclass extends a superclass.
* A subclass inherits all public instance variables and methods of the superclass, but does not inherit the private
instance variables and methods of the superclass. 
* Inherited methods can be overriden, but instance variables cannot be overriden (although they can be redefined in the subclass, 
but that's not the same thing and there's almost never a need to do it).
* The IS-A relationship works in only one direction.
* When a method is overriden in a subclass, and that method is invoked on an instance of the subclass, the overriden version 
of the method is called. 

### When to use Inheritance
* Do use inheritance when one class is a more specific type of a superclass.
* Do consider inheritance when you have behaviour that should be shared among multiple classes of the same generatl type. Be aware, 
however, that while inheritance is one of the key features of OOP, it's not necessarily the best way to achieve behaviour reuse. 
Design patterns will help you see other more subtle and flexible options. 
* Do not use inheritance just so that you can reuse code from another class, if the relationship between the superclass and subclass
 violate either of the above two rules.
* Do not use inheritance if the subclass and superclass do not pass the IS-A test. 

### Advantages of Inheritance
* Avoid duplicate code
* Gurantee that all classes grouped under a certain supertype have all the methods that the supertype has. 
* Get to take advantage of polymorphism. 

### Polymorphism
* With polymorphism, the reference type can be a superclass of the actual object type.
```java
    Animal myDog = new Dog();
    // Animal (reference type) is a superclass of Dog 
```
* You can have polymorphic arguments and return types.
* With polymorphism, you can write code that doesn't have to change when you introduce new subclass types into the program. 

### Can you extend any class?
There are three things that can prevent a class from being subclassed.
1. **Access Control**: Even though a class can't be marked **private**, a class can be non-public (what you get, if you 
don't declare the class as public). A non-public class can be subclassed only by classes in the same package as the class. 
2. **final** Keyword Modifier: A final class mean that it's the end of the inheritance tree.
3. **Private Constructor**: If a class only has private constructors, it can't be subclassed. 
### Why would you ever want to make a final class?
**Security**: The security of knowing that the methods will always work the way that you wrote them, because they can't be
overriden. A lot of classes in the Java API are final for that reason. e.g. the **String** class.
### Can you make a method final?
If you want to protect a specific method from being overrident, mark the method with the **final** modifier. 

### Rules for overriding method
* Arguments must be the same, and return type must be the same type, or a subclass type.
* The method can't be less accessible. 

### Method overloading
* Method overloading is nothing more than having two methods with the same name but different argument lists. 
* There is no polymorphism involved with overloaded methods. 
* An overloaded method is not the same as an overriden method. 

### Rules for method overloading
* The return types can be different, but can't change only return type.
* You can vary the access levels in any direction. 
