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
## Is JVM compiler or interpreter?
JVM runs/interprets/translates bytecode into native machine code. JVM is interpreter.