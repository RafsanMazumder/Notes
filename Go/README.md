# Get Programming With Go
## [Chapter-1] Get ready, get set, Go
### Gophers
The community of people who have adopted Go call themselves **gophers**

### Compiled Language
Go is a compiled programming language. Before you run a program, the compiler
compiles all your code into a single executable for you to run or distribute. 
Python, Ruby, and several other popular languages use an interpreter to translate 
one statement at a time as a program is running.

### The Go Playground
**play.golang.org** will compile your code and then execute your code on Google
servers.

### Packages and functions
```go
    package main // Declares the package this code belongs to                                 

    import (
        "fmt" // Makes the fmt (format) package available for use                                    
    )

    func main() { // Declares a function named main                                 
        fmt.Println("Hello, playground")         
    }
```

### main Identifier
The **main** identifier is special. When you run a program written in Go, execution 
begins at the **main** function in the **main** package. Without **main**, the Go
compiler will report an error, because it doesn't know where the program should start.

### Brace style
Go enforces the opening brace **{** to be on the same line as the **func** keyword, 
whereas the closing brace **}** to be on its own line. The Go compiler automatically will
insert semicolons on your behalf. 

```go
    func main() // missing function body
    { // unexpected semicolon or new line before {                
    }
```

The semicolon was inserted in the wrong place and the compiler throws error. 

## [Chapter-2] A glorified calculator
* For comment, you can use double slash **//**.
* The **Print**, **Println**, **Printf** functions display text and numbers on the screen.
* With **Printf** and the **%v format verb**, values can be placed anywhere in the displayed text. 
* Constants are declared with the **const** keyword and can't be changed.
* Variables are declared with the **var** keyword and can be assigned new values
while a program is running. Variables must be declared before you can use them. Go will report an error if you assign a value to a variable that hasn’t been declared with var—for example, speed = 16.
* Declare multiple variables at once
```go
    var (
        distance = 56000000
        speed = 100800
    )
```
```go
    var distance, speed = 56000000, 100800
```
* Increment operator **++**. Go does not support the prefix increment **++count** like C and Java.

## [Chapter-3] Loops and branches
### Definition of true and false
Some programming languages have a loose definition of truth. In Python and JavaScript the absence of text ("") is considered false, as is the number zero. In Go, the only true value is true and the only false value is false. Another way to arrive at a true or false value is by comparing two values. 

```go
    var minor = age < 18
```

### Switch statement
One unique feature of **switch** is the **fallthrough** keyword, which is used to execute the body of the next case. Falling through happens by default in C, Java, and JavaScript, whereas Go takes a safer approach, requiring an explicit fallthrough keyword.
```go
    switch room {
    case "cave":
        fmt.Println("You find yourself in a dimly lit cavern.")
    case "lake":
        fmt.Println("The ice seems solid enough.")
        fallthrough
    case "underwater":
        fmt.Println("The water is freezing cold.")
    }
```

## [Chapter-4] Variable scope
### Short declaration
```go
    var count = 10
    count := 10
```
```go
    for count := 10; count > 0; count-- {
        fmt.Println(count)
    }
```
```go
    if num := rand.Intn(3); num == 0 {
        fmt.Println("Space Adventures")
    } else if num == 1 {
        fmt.Println("SpaceX")
    } else {
        fmt.Println("Virgin Galactic")
    }   
```
```go
    switch num := rand.Intn(10); num {
    case 0:
        fmt.Println("Space Adventures")
    case 1:
        fmt.Println("SpaceX")
    case 2:
        fmt.Println("Virgin Galactic")
    default:
        fmt.Println("Random spaceline #", num)
    }
```
### Introducing new scope
An opening curly brace **{** introduces a new scope that ends with a closing brace }. The **case** and **default** keywords also introduce a new scope even though no curly braces are involved.

## [Chapter-6] Real numbers
### Declaring floating point variables
Go can infer types for you. In particular, Go will infer float64 for variables initialized with real numbers.
```go
    days := 365.2425                     
    var days = 365.2425
    var days float64 = 365.2425
```

### **golint** tool
The golint tool provides hints for coding style.
```go
    var days float64 = 365.2425
    // "should omit type float64 from declaration of var days;
    // it will be inferred from the right-hand side"
```

### Single & Double precision floating-point numbers
Go has two floating-point types. The default floating-point type is float64, a 64-bit floating-point type that uses eight bytes of memory. Some languages use the term double precision to describe the 64-bit floating-point type.<br/><br/>
The float32 type uses half the memory of float64 but offers less precision. This type is sometimes called single precision. To use float32, you must specify the type when declaring a variable.<br/><br/>
Functions in the math package operate on float64 types, so prefer float64 unless you have a good reason to do otherwise.

### The zero value
In Go, each type has a default value, called the zero value. The default applies when you declare a variable but don’t initialize it with a value.
```go
    var price float64
    fmt.Println(price) // This prints 0
```

### Displaying floating-point types
When using **Print** or **Println** with floating-point types, the default behavior is to display as many digits as possible. If that’s not what you want, you can use **Printf** with the **%f** formatting verb to specify the number of digits.

```go
    third := 1.0 / 3
    fmt.Println(third)               
    fmt.Printf("%v\n", third)        // Prints 0.3333333333333333
    fmt.Printf("%f\n", third)        // Prints 0.333333
    fmt.Printf("%.3f\n", third)      // Prints 0.333
    fmt.Printf("%4.2f\n", third)     // Prints 0.33
    // "%4.2f" -> width.precision
```

### Width & Precision
Precision specifies how many digits should appear after the decimal point. Width specifies the minimum number of characters to display, including the decimal point and the digits before and after the decimal (for example, 0.33 has a width of 4). If the width is larger than the number of characters needed, Printf will pad the left with spaces. If the width is unspecified, Printf will use the number of characters necessary to display the value. To left-pad with zeros instead of spaces, prefix the width with a zero.

```go
    fmt.Printf("%05.2f\n", third)  // Prints 00.33
```

### Floating-point accuracy
Floating-point numbers suffer from rounding errors, except floating-point hardware uses a binary representation (using only 0s and 1s) instead of decimal (using 1–9). The consequence is that computers can accurately represent ⅓ but have rounding errors with other numbers.

```go
    third := 1.0 / 3.0
    fmt.Println(third + third + third) // Prints 1

    piggyBank := 0.1
    piggyBank += 0.2
    fmt.Println(piggyBank) // Prints 0.30000000000000004
```

### Comparing floating-point numbers
```go
    piggyBank := 0.1
    piggyBank += 0.2
    fmt.Println(piggyBank == 0.3) // Prints false
```
Instead of comparing floating-point numbers directly, determine the absolute difference between two numbers and then ensure the difference isn’t too big. To take the absolute value of a float64, the math package provides an **Abs** function:
```go
    fmt.Println(math.Abs(piggyBank-0.3) < 0.0001) // Prints true    
```

### Machine epsilon
The upper bound for a floating-point error for a single operation is known as the machine epsilon, which is 2<sup>-52</sup> for float64 and 2<sup>-23</sup> for float32. Unfortunately, floating-point errors accumulate rather quickly.

```go
    piggyBank := 0.0
    for i := 0; i < 11; i++ {
        piggyBank += 0.1
    }
    fmt.Println(piggyBank) // Prints 1.0999999999999999
```

## [Chapter-7] Whole numbers
### Signed and Unsigned integers
Go offers 10 different types for whole numbers, collectively called integers. Five integer types are signed, meaning they can represent both positive and negative whole numbers. The other five integer types are unsigned, meaning they’re for positive numbers only. When using type inference, Go will always pick the int type for a literal whole number. The following three lines are equivalent:
```go
    year := 2018
    var year = 2018
    var year int = 2018
```

### Architecture independent integer types
Integers, whether signed or unsigned, come in a variety of sizes. The size affects their minimum and maximum values and how much memory they consume. There are eight architecture-independent types suffixed with the number of bits they need.
| Type | Bit Depth |
|---|---|
| int8 | 8 bits |
| uint8 | 8 bits |
| int16 | 16 bits |
| uint16 | 16 bits |
| int32 | 32 bits |
| uint32 | 32 bits |
| int64 | 64 bits |
| uint64 | 64 bits |

### Architecture dependent integer types
The int and uint types are optimal for the target device. The Go Playground, Raspberry Pi 2, and older mobile phones provide a 32-bit environment where both int and uint are 32-bit values. Any recent computer will provide a 64-bit environment where int and uint will be 64-bit values. <br/> <br/>

Although it’s tempting to think of int as an int32 on some devices and an int64 on other devices, these are three distinct types. The int type isn’t an alias for another type.

### Showing type inference
```go
    a := "text"
    fmt.Printf("Type %T for %[1]v\n", a) // Prints Type string for text

    b := 42
    fmt.Printf("Type %T for %[1]v\n", b) // Prints Type int for 42

    c := 3.14
    fmt.Printf("Type %T for %[1]v\n", c) // Prints Type float64 for 3.14

    d := true
    fmt.Printf("Type %T for %[1]v\n", d) // Prints Type bool for true
```

### Hexadecimal in Go
To distinguish between decimal and hexadecimal, Go requires a 0x prefix for hexadecimal. These two lines of code are equivalent:
```go
    var red, green, blue uint8 = 0, 141, 213
    var red, green, blue uint8 = 0x00, 0x8d, 0xd5
```

### Integers wrap around
All integer types have a limited range. When that range is exceeded, integer types in Go wrap around. An 8-bit unsigned integer (uint8) has a range of 0–255. Incrementing beyond 255 will wrap back to 0.

### min/max constants in **math** package
The math package defines **math.MaxUint16** as 65535 and similar min/max constants for each architecture-independent integer type. Remember that int and uint could be either 32-bit or 64-bit, depending on the underlying hardware.

### Wrapping around time
On Unix-based operating systems, time is represented as the number of seconds since January 1, 1970 UTC (Coordinated Universal Time). In the year 2038, the number of seconds since January 1, 1970 will exceed two billion, the capacity of an int32.

## [Chapter-8] Big numbers
### The **big** package
The **big** package provides three types:
* **big.Int** is for big integers, when 18 quintillion isn’t enough.
* **big.Float** is for arbitrary-precision floating-point numbers.
* **big.Rat** is for fractions like ⅓.
```go
    distance := new(big.Int)
    distance.SetString("24000000000000000000", 10)
```

### Constants of unusual size
Constants can be declared with a type, just like variables. And just like variables, a **uint64** constant can’t possibly contain a number like 24 quintillion:

```go
    const distance uint64 = 24000000000000000000 // overflows uint64
```
It gets interesting when you declare a constant without a type. For variables, Go uses type inference to determine the type, and in the case of 24 quintillion, overflows the int type. Constants are different. Rather than infer a type, constants can be untyped. The following line doesn’t cause an overflow error:

```go
    const distance = 24000000000000000000
```
Constants are declared with the **const** keyword, but every literal value in your program is a constant too. That means unusually sized numbers can be used directly, as shown in the following listing.

```go
    fmt.Println("Andromeda Galaxy is", 24000000000000000000/299792/86400, "light days away.") // Prints Andromeda Galaxy is 926568346 light days away
```

Calculations on constants and literals are performed during compilation rather than while the program is running. The Go compiler is written in Go. Under the hood, untyped numeric constants are backed by the **big** package.

```go
    const distance = 24000000000000000000
    const lightSpeed = 299792
    const secondsPerDay = 86400

    const days = distance / lightSpeed / secondsPerDay

    fmt.Println("Andromeda Galaxy is", days, "light days away.") // Prints Andromeda Galaxy is 926568346 light days away
```

Though the Go compiler utilizes the **big** package for untyped numeric constants, constants and **big.Int** values aren’t interchangeable. The following line displayed a **big.Int** containing 24 quintillion, but you can’t display the distance constant due to an overflow error. Because untyped constants must be converted to typed variables when passed to functions.

```go
    fmt.Println("Andromeda Galaxy is", distance, "km away.") // Prints constant 24000000000000000000 overflows int
```

Very large constants are certainly useful, but they aren’t a replacement for the big package.

## [Chapter-9] Multilingual text

### Declaring string variables
Literal values wrapped in quotes are inferred to be of the type string, so the following three lines are equivalent:
```go
    peace := "peace"
    var peace = "peace"
    var peace string = "peace"
```
If you declare a variable without providing a value, it will be initialized with the zero value for its type. The zero value for the string type is an empty string (""):
```go
    var blank string
```

### Characters, code points, runes and bytes
The **Unicode Consortium** assigns numeric values, called **code points**, to over one million unique characters. For example, 65 is the code point for the capital letter A. </br></br>
To represent a single Unicode code point, Go provides **rune**, which is an alias for the **int32** type.</br></br>
A **byte** is an alias for the **uint8** type. It’s intended for binary data, though byte can be used for English characters defined by **ASCII**, an older 128-character subset of Unicode.

### Type aliases
An alias is another name for the same type, so **rune** and **int32** are interchangeable.
```go
    type byte = uint8
    type rune = int32
```

### Character literals
Rather than memorize Unicode code points, Go provides a character literal. Just enclose a character in single quotes 'A'. If no type is specified, Go will infer a **rune**, so the following three lines are equivalent:
```go
    grade := 'A'
    var grade = 'A'
    var grade rune = 'A'
```

### Immutable strings
A variable can be assigned to a different string, but strings themselves can’t be altered:
```go
    peace := "shalom"
    peace = "salām"
```
Strings in Go are immutable, as they are in Python, Java, and JavaScript. Unlike strings in Ruby and character arrays in C, you can’t modify a string in Go:
```go
    message[5] = 'd' // Cannot assign to message[5]
```
### built-in functions
Go has a handful of built-in functions that don’t require an import statement. The len function can determine the length for a variety of types. In this case, len returns the length of a string in bytes.
```go
    fmt.Println(len(message)) // Prints 30
```

### Decoding strings into runes
Strings in Go are encoded with UTF-8, one of several encodings for Unicode code points. UTF-8 is an efficient variable length encoding where a single code point may use 8 bits, 16 bits, or 32 bits. By using a variable length encoding, UTF-8 makes the transition from ASCII straightforward, because ASCII characters are identical to their UTF-8 encoded counterparts.

### Supporting other languages
The first step to supporting other languages is to decode characters to the rune type before manipulating them. Fortunately, Go has functions and language features for decoding UTF-8 encoded strings.</br></br>
The utf8 package provides functions to determine the length of a string in runes rather than bytes and to decode the first character of a string. The **DecodeRuneInString** function returns the first character and the number of bytes the character consumed.

```go
    package main

    import (
        "fmt"
        "unicode/utf8"
    )

    func main() {
        question := "¿Cómo estás?"

        fmt.Println(len(question), "bytes") // Prints 15 bytes
        fmt.Println(utf8.RuneCountInString(question), "runes") // Prints 12 runes

        c, size := utf8.DecodeRuneInString(question)
        fmt.Printf("First rune: %c %v bytes", c, size) // Prints First rune: ¿ 2 bytes
    }
```

### decode UTF-8 encoded strings with **range** keyword
The Go language provides the **range** keyword to iterate over a variety of collections. It can also decode UTF-8 encoded strings, as shown in the following listing.

```go
    question := "¿Cómo estás?"
    for _, c := range question {
        fmt.Printf("%c ", c) // Prints ¿ C ó m o e s t á s ?
    }
```

## [Chapter-10] Converting between types
### Mixing types
When presented with two or more different types, some programming languages make a best effort to guess the programmer’s intentions. Both JavaScript and PHP can subtract 1 from the string "10". Whereas the Go compiler rejects "10" - 1 with a mismatched types error.</br></br>
Another example of mismatched types occurs when attempting a calculation with a mix of integer and floating-point types.
```go
    age := 41
    marsDays := 687
    earthDays := 365.2425
    fmt.Println("I am", age*earthDays/marsDays, "years old on Mars.") // Invalid operation: mismatched types
```

### Numeric type conversions
Type conversion is straightforward. If you need the integer age to be a floating-point type for a calculation, wrap the variable with the new type:
```go
    age := 41
    marsAge := float64(age)
```

### Checking variable within the range of a type
These min/max constants are untyped, allowing the comparison of v, to MaxUint8.
```go
    v := 42
    if v >= 0 && v <= math.MaxUint8 {
        v8 := uint8(v)
    }
```

### String conversion
#### Converting rune to string
```go
    var pi rune = 960
    var alpha rune = 940
    var omega rune = 969
    var bang byte = 33

    fmt.Print(string(pi), string(alpha), string(omega), string(bang)) // Prints πάω!
```

#### Integer to ASCII
**Itoa** is short for integer to ASCII.
```go
    countdown := 10

    str := "Launch in T minus " + strconv.Itoa(countdown) + " seconds."
    fmt.Println(str) // Prints Launch in T minus 10 seconds.
```

Another way to convert a number to a string is to use **Sprintf**, a cousin of Printf that returns a string rather than displaying it:
```go
    countdown := 9
    str := fmt.Sprintf("Launch in T minus %v seconds.", countdown)
    fmt.Println(str)
```

#### ASCII to Integer
The **strconv** package provides the **Atoi** function (ASCII to integer). Because a string may contain gibberish or a number that’s too big, the **Atoi** function may return an error:
```go
    countdown, err := strconv.Atoi("10")
    if err != nil {
        // oh no, something went wrong
    }
    fmt.Println(countdown) // Prints 10
```

### Static types
In Go, once a variable is declared, it has a type and the type cannot be changed. This is known as static typing, which is easier for the compiler to optimize, so your programs run fast. But attempting to use a variable with a value of a different type will cause the Go compiler to report an error. </br></br>
Languages such as JavaScript, Python, and Ruby use dynamic typing instead of static typing. In those languages, each value has an associated type, and variables can hold values of any type.</br></br>
Go does have an escape hatch for situations where the type is uncertain. For example, the Println function will accept both strings and numeric types.

### Numeric equivalent of boolean
In programming languages without a dedicated bool type, the values 1 and 0 often stand in for true and false, respectively. Booleans in Go don’t have a numeric equivalent.

## [Chapter-12] Functions
### Summary
* In Go, the functions, variables, and other identifiers that begin with an uppercase letter are exported and become available to other packages. 
* Parameter and argument are terms from mathematics, with a subtle distinction. A function accepts parameters and is invoked with arguments, though at times people may use the terms interchangeably.
* Each parameter or result is a name followed by a type, though types may be elided when multiple named parameters or results have the same type. Results can also be listed as types without names.
```go
    func Unix(sec int64, nsec int64) Time
    func Unix(sec, nsec int64) Time
    func Atoi(s string) (i int, err error)
    func Atoi(s string) (int, error)
```
* Function calls are prefixed with the name of the package where the function is declared, unless the function is declared in the same package it’s called from.
* Functions are called with arguments that correspond to the parameters they accept. Results are returned to the caller with the **return** keyword.

### Println function
You can pass the **Println** function a variable number of arguments, a feature indicated by the ellipsis (...). There’s a special term for this: **Println** is said to be a variadic function. The parameter a is a collection of the arguments passed to the function.
```go
    func Println(a ...interface{}) (n int, err error)
```
The type of the a parameter is **interface{}**, known as the empty interface type. This special type is what enables **Println** to accept an **int**, **float64**, **string**, **time.Time**, or any other type without the Go compiler reporting an error. The combination of variadic functions and the empty interface, written together as **...interface{}**, means you can pass **Println** any number of arguments of any type.

## [Chapter-13] Methods
### Declaring new types
The type keyword declares a new type with a name and an underlying type. 
```go
    type celsius float64
    var temperature celsius = 20
```
The numeric literal 20, like all numeric literals, is an **untyped** constant. It can be assigned to a variable of type **int**, **float64**, or any other numeric type. The celsius type is a new numeric type with the same behavior and representation as a **float64**, so the assignment in the previous listing works.

### Mismatched types
Types can't be mixed. 
```go
    type celsius float64
    var temperature celsius = 20

    var warmUp float64 = 10
    temperature += warmUp // Invalid operation: mismatched types
```
To add warmUp, it must first be converted to the celsius type. This version works:
```go
    var warmUp float64 = 10
    temperature += celsius(warmUp)
```

### Methods
Methods are like functions associated to a type by way of a receiver specified before the method name. Methods can accept multiple parameters and return multiple results, just like functions, but they must always have exactly one receiver. Within the method body, the receiver behaves just like any other parameter.
```go
    func kelvinToCelsius(k kelvin) celsius {
        return celsius(k - 273.15)
    }

    func (k kelvin) celsius() celsius {
        return celsius(k - 273.15)
    }
```

### Calling methods
The calling syntax for methods uses dot notation, with a variable of the appropriate type followed by a dot, the method name, and any arguments.
```go
    var k kelvin = 294.0
    var c celsius

    c = kelvinToCelsius(k)
    c = k.celsius()
```

## [Chapter-14] First-class functions
In Go you can assign functions to variables, pass functions to functions, and even write functions that return functions. Functions are first-class—they work in all the places that integers, strings, and other types work.


### Assigning functions to variables
Function and method calls always have parentheses (for example, fn()) whereas the function itself can be assigned by specifying a function name without parentheses.
```go
    type kelvin float64

    func fakeSensor() kelvin {
        return kelvin(rand.Intn(151) + 150)
    }

    func realSensor() kelvin {
        return 0
    }

    func main() {
        sensor := fakeSensor
        fmt.Println(sensor())

        sensor = realSensor
        fmt.Println(sensor())
    }
```
The **sensor** variable is of type function, where the function accepts no parameters and returns a **kelvin** result. When not relying on type inference, the sensor variable would be declared like this:
```go
    var sensor func() kelvin
```

### Passing functions to other functions
```go
    type kelvin float64

    func measureTemperature(samples int, sensor func() kelvin) {
        for i := 0; i < samples; i++ {
            k := sensor()
            fmt.Printf("%v° K\n", k)
            time.Sleep(time.Second)
        }
    }

    func fakeSensor() kelvin {
        return kelvin(rand.Intn(151) + 150)
    }

    func main() {
        measureTemperature(3, fakeSensor)
    }
```

### Declaring function types
```go
    type sensor func() kelvin
    func measureTemperature(samples int, s sensor)
```

### Anonymous functions
An **anonymous function**, also called a **function literal** in Go, is a function without a name. Unlike regular functions, function literals are **closures** because they keep references to variables in the surrounding scope. </br> </br>
You can assign an anonymous function to a variable and then use that variable like any other function.
```go
    func main() {
        f := func(message string) {
            fmt.Println(message)
        }

        f("Go to the party.")
    }
```

You can even declare and invoke an anonymous function in one step.
```go
    func main() {
        func() {
            fmt.Println("Functions anonymous")
        }()
    }
```

### Closures
```go
    type kelvin float64

    // sensor function type
    type sensor func() kelvin

    func realSensor() kelvin {
        return 0
    }

    func calibrate(s sensor, offset kelvin) sensor {
        return func() kelvin {
            return s() + offset
        }
    }

    func main() {
        sensor := calibrate(realSensor, 5)
        fmt.Println(sensor())
    }
```
The anonymous function in the preceding listing makes use of closures. It references the s and offset variables that the calibrate function accepts as parameters. Even after the calibrate function returns, the variables captured by the closure survive, so calls to sensor still have access to those variables. The anonymous function encloses the variables in scope, which explains the term closure.</br></br>
A closure keeps a **reference** to surrounding variables rather than a copy of their values, changes to those variables are reflected in calls to the anonymous function:
```go
    var k kelvin = 294.0

    sensor := func() kelvin {
        return k
    }
    fmt.Println(sensor()) // Prints 294

    k++
    fmt.Println(sensor()) // Prints 295
```

## [Chapter-16] Arrayed in splendor
### Declaring arrays and accessing their elements
```go
    var planets [8]string

    planets[0] = "Mercury"
    planets[1] = "Venus"
    planets[2] = "Earth"
```

### Zero value
Elements of an array are initially the zero value for the array’s type, which means 0 for integer arrays.

### Initialize arrays with composite literals
A composite literal is a concise syntax to initialize any composite type with the values you want. Rather than declare an array and assign elements one by one, Go’s composite literal syntax will declare and initialize an array in a single step.
```go
    dwarfs := [5]string{"Ceres", "Pluto", "Haumea", "Makemake", "Eris"}
```
You can ask the Go compiler to count the number of elements in the composite literal by specifying the ellipsis **...** instead of a number. But the **trailing comma** is required.
```go
    planets := [...]string{
        "Mercury",
        "Venus",
        "Earth",
        "Mars",
        "Jupiter",
        "Saturn",
        "Uranus",
        "Neptune",
    }
```

### Iterating through an array with range
```go
    dwarfs := [5]string{"Ceres", "Pluto", "Haumea", "Makemake", "Eris"}

    for i, dwarf := range dwarfs {
        fmt.Println(i, dwarf)
    }
```
You can use the blank identifier (underscore) if you don’t need the index variable provided by range.

### Arrays are copied
Assigning an array to a new variable or passing it to a function makes a complete copy of its contents. Arrays always pass by value.

### Length is part of array's type
It’s important to recognize that the length of an array is part of its type. The type **[8]string** and type **[5]string** are both collections of strings, but they’re two different types. The Go compiler will report an error when attempting to pass an array of a different length:

```go
    func terraform(planets [8]string) {
        for i := range planets {
            planets[i] = "New " + planets[i]
        }
    }

    func main() {
        dwarfs := [5]string{"Ceres", "Pluto", "Haumea", "Makemake", "Eris"}
        terraform(dwarfs) // Can’t use dwarfs (type [5]string) as type [8]string in argument to terraform
    }
```
For these reasons, **arrays** aren’t used as function parameters nearly as often as **slices**.

## [Chapter-17] Slices: windows into arrays
### Slicing an array
Slicing is expressed with a half-open range. 
```go
    planets := [...]string{
        "Mercury",
        "Venus",
        "Earth",
        "Mars",
        "Jupiter",
        "Saturn",
        "Uranus",
        "Neptune",
    }

    terrestrial := planets[0:4]
    gasGiants := planets[4:6]
    iceGiants := planets[6:8]
```

### Slicing a slice
You can also slice an array, and then slice the resulting slice:
```go
    giants := planets[4:8]
    gas := giants[0:2]
    ice := giants[2:4]
    fmt.Println(giants, gas, ice)
```

### Slice modifies underlying array
Assigning a new value to an element of a slice modifies the underlying planets array. The change will be visible through the other slices:
```go
    planets := [...]string{
        "Mercury",
        "Venus",
        "Earth",
        "Mars",
        "Jupiter",
        "Saturn",
        "Uranus",
        "Neptune",
    }

    terrestrial := planets[0:4]
    gasGiants := planets[4:6]
    iceGiants := planets[6:8]    
    iceGiantsMarkII := iceGiants
    iceGiants[1] = "Poseidon"
    fmt.Println(planets) // Prints [Mercury Venus Earth Mars Jupiter Saturn Uranus Poseidon]
    fmt.Println(iceGiants, iceGiantsMarkII, ice) // Prints [Uranus Poseidon] [Uranus Poseidon] [Uranus Poseidon]
```

### Slicing strings
The result of slicing a string is another string. Be aware that the indices indicate the number of bytes, not runes:
```go
    question := "¿Cómo estás?"
    fmt.Println(question[:6]) // Prints ¿Cóm
```

### Declaring slice directly
A slice of strings has the type **[]string**, with no value between the brackets. This differs from an array declaration, which always specifies a fixed length or ellipsis between the brackets.
```go
    dwarfs := []string{"Ceres", "Pluto", "Haumea", "Makemake", "Eris"}
```
There is still an underlying array. Behind the scenes, Go declares a five-element array and then makes a slice that views all of its elements.

### %T format verb with slice and array
```go
    dwarfArray := [5]string{"Ceres", "Pluto", "Haumea", "Makemake", "Eris"}
    dwarfs := []string{"Ceres", "Pluto", "Haumea", "Makemake", "Eris"}

    fmt.Printf("array %T\n", dwarfArray) // Prints array [5]string
    fmt.Printf("slice %T\n", dwarfs) // Prints slice []string
```

### Slices vs arrays
**Arrays** are rarely used directly. Gophers prefer **slices** for their versatility, especially when passing arguments to functions.

## [Chapter-21] A little structure
### Declaring a structure 
```go
    var curiosity struct {
        lat  float64
        long float64
    }

    curiosity.lat = -4.5895
    curiosity.long = 137.4417

    fmt.Println(curiosity.lat, curiosity.long) // Prints -4.5895 137.4417
    fmt.Println(curiosity) // Prints {-4.5895 137.4417}
```

### Reusing structures with types
```go
    type location struct {
        lat  float64
        long float64
    }

    var spirit location
    spirit.lat = -14.5684
    spirit.long = 175.472636

    var opportunity location
    opportunity.lat = -1.9462
    opportunity.long = 354.4734

    fmt.Println(spirit, opportunity) // Prints {-14.5684 175.472636} {-1.9462 354.4734}
```

### Initialize structures with composite literals
Composite literals for initializing structures come in two different forms.</br></br>
Fields may be in any order, and fields that aren’t listed will retain the zero value for their type. This form tolerates change and will continue to work correctly even if fields are added to the structure or if fields are reordered.
```go
    type location struct {
        lat, long float64
    }

    opportunity := location{lat: -1.9462, long: 354.4734}
    fmt.Println(opportunity) // Prints {-1.9462 354.4734}

    insight := location{lat: 4.5, long: 135.9}
    fmt.Println(insight) // Prints {4.5 135.9}
```
Another form doesn't specify field names. Instead, a value must be provided for each field in the same order in which they’re listed in the structure definition. This form works best for types that are stable and only have a few fields.
```go
    spirit := location{-14.5684, 175.472636}
    fmt.Println(spirit) // Prints {-14.5684 175.472636}
```

### Printing keys of structures
You can modify the **%v** format verb with a plus sign + to print out the field names, as shown in the next listing.
```go
    curiosity := location{-4.5895, 137.4417}
    fmt.Printf("%v\n", curiosity) // Prints {-4.5895 137.4417}
    fmt.Printf("%+v\n", curiosity) // Prints {lat:-4.5895 long:137.4417}
```

### Structures are copied
```go
    bradbury := location{-4.5895, 137.4417}
    curiosity := bradbury

    curiosity.long += 0.0106

    fmt.Println(bradbury, curiosity) // Prints {-4.5895 137.4417} {-4.5895 137.4523}
```

### Slice of structures
A slice of structures, **[]struct** is a collection of zero or more values (a slice) where each value is based on a structure instead of a primitive type like float64.

```go
    type location struct {
        name string
        lat  float64
        long float64
    }

    locations := []location{
        {name: "Bradbury Landing", lat: -4.5895, long: 137.4417},
        {name: "Columbia Memorial Station", lat: -14.5684, long: 175.472636},
        {name: "Challenger Memorial Station", lat: -1.9462, long: 354.4734},
    }
```

### Encoding structures to JSON
JavaScript Object Notation, or JSON (json.org), is a standard data format. It’s based on a subset of the JavaScript language but it’s widely supported in other programming languages. JSON is commonly used for web APIs (Application Programming Interfaces). </br></br>
The Marshal function from the json package is used to encode the data into JSON format. Marshal returns the JSON data as bytes, which can be sent over the wire or converted to a string for display.
```go
    type location struct {
        Lat, Long float64
    }

    curiosity := location{-4.5895, 137.4417}

    bytes, _ := json.Marshal(curiosity)

    fmt.Println(string(bytes)) // Prints {“Lat”:-4.5895,“Long”:137.4417}
```
Notice that the JSON keys match the field names of the location structure. For this to work, the json package requires fields to be exported. If Lat and Long began with a lowercase letter, the output would be {}.

### Customizing JSON with struct tags
Go’s json package requires that fields have an initial uppercase letter and multiword field names use CamelCase by convention. You may want JSON keys in snake_case. The fields of a structure can be tagged with the field names you want the json package to use.
```go
    type location struct {
        Lat  float64 `json:"latitude"`
        Long float64 `json:"longitude"`
    }

    curiosity := location{-4.5895, 137.4417}

    bytes, _ := json.Marshal(curiosity)

    fmt.Println(string(bytes)) // Prints {“latitude”:-4.5895,“longitude”:137.4417}
```
Struct tags are ordinary strings associated with the fields of a structure. Raw string literals (``) are preferable, because quotation marks don’t need to be escaped with a backslash, as in the less readable **"json:\"latitude\""**.</br></br>
To customize the Lat field for both JSON and XML, the struct tag would be **`json:"latitude" xml:"latitude"`**.

## [Chapter-22] Go’s got no class
### No classes
The Go language has types, methods on types, and structures. Together, these provide much of the functionality that classes do for other languages, without needing to introduce a new concept into the language.

### Attaching methods to structures
```go
    // coordinate in degrees, minutes, seconds in a N/S/E/W hemisphere.
    type coordinate struct {
        d, m, s float64
        h       rune
    }

    // decimal converts a d/m/s coordinate to decimal degrees.
    func (c coordinate) decimal() float64 {
        sign := 1.0
        switch c.h {
        case 'S', 'W', 's', 'w':
            sign = -1
        }
        return sign * (c.d + c.m/60 + c.s/3600)
    }
```

### Constructor functions
Classical languages provide constructors as a special language feature to construct objects. Python has **_init_**, Ruby has **initialize**, and PHP has **__construct()**. Go doesn’t have a language feature for constructors. Instead **newLocation** is an ordinary function with a name that follows a convention.
```go
    type location struct {
        lat, long float64
    }

    // newLocation from latitude, longitude d/m/s coordinates.
    func newLocation(lat, long coordinate) location {
        return location{lat.decimal(), long.decimal()}
    }    
```
Functions in the form **newType** or **NewType** are used to construct a value of said type. Whether you name it **newLocation** or **NewLocation** depends on whether the function is exported for other packages to use.</br></br>
Sometimes constructor functions are named **New**, as is the case with the **New** function in the errors package. Because function calls are prefixed with the package they belong to, naming the function **NewError** would be read as **errors.NewError** rather than the more concise and preferable **errors.New**.

## [Chapter-23] Composition and forwarding
In the world of object-oriented programming, objects are composed of smaller objects in the same way. Computer scientists call this object composition or simply composition. Gophers use composition with structures, and Go provides a special language feature called embedding to forward methods.

### Composition over inheritance
Designing hierarchies can be difficult. A hierarchy of the animal kingdom would attempt to group animals with the same behaviors. Some mammals walk on land while others swim, yet blue whales also nurse their young. How would you organize them? It can be difficult to change hierarchies too, as even a small change can have a wide impact.</br></br>
Composition is a far simpler and more flexible approach: implement walking, swimming, nursing, and other behaviors and associate the appropriate ones with each animal.

### Composing structures
```go
    type report struct {
        sol         int
        temperature temperature
        location    location
    }

    type temperature struct {
        high, low celsius
    }

    type location struct {
        lat, long float64
    }

    type celsius float64
```

### Forwarding methods
Go will do method forwarding for you with struct embedding. To embed a type in a structure, specify the type without a field name.
```go
    type report struct {
        sol         int
        temperature
        location
    }
```
All the methods on the temperature type are automatically made accessible through the report type.
```go
    func (t temperature) average() celsius {
        return (t.high + t.low) / 2
    }
    report := report{
        sol:         15,
        location:    location{-4.5895, 137.4417},
        temperature: temperature{high: -1.0, low: -78.0},
    }

    fmt.Printf("average %v° C\n", report.average()) // Prints average -39.5° C
```
Embedding doesn’t only forward methods. Fields of an inner structure are accessible from the outer structure. In addition to **report.temperature.high**, you can access the high temperature with **report.high** as follows:
```go
    fmt.Printf("%v° C\n", report.high) // Prints -1° C
    report.high = 32
    fmt.Printf("%v° C\n", report.temperature.high) // Prints 32° C
```

### Name collisions
If multiple embedded types implement a method of the same name, The Go compiler only reports an error if the method is being used.

### Inheritance vs Composition
Inheritance is a different way of thinking about designing software. With inheritance, a rover is a type of vehicle and thereby inherits the functionality that all vehicles share. With composition, a rover has an engine and wheels and various other parts that provide the functionality a rover needs. A truck may reuse several of those parts, but there is no vehicle type or hierarchy descending from it.</br></br>
Composition is generally considered more flexible, allowing greater reuse and easier changes than software built with inheritance.
> Favor object composition over class inheritance.
>
> -- <cite>Gang of Four, Design Patterns: Elements of Reusable Object-Oriented Software</cite>

> Use of classical inheritance is always optional; every problem that it solves can be solved another way.
>
> -- <cite>Sandi Metz, Practical Object-Oriented Design in Ruby</cite>

## [Chapter-24] Interfaces
Typically interfaces are declared as named types that can be reused. There’s a convention of naming interface types with an -er suffix: a talker is anything that talks, as shown in the following listing.
```go
    type talker interface {
        talk() string
    }
```
> Used together, composition and interfaces make a very powerful design tool.
>
> -- <cite>Bill Venners, JavaWorld</cite>
### Discovering the interface
With Go you can begin implementing your code and discover the interfaces as you go. Any code can implement an interface, even code that already exists.

### Satisfying interfaces
The standard library exports a number of single-method interfaces that you can implement in your code.
> Go encourages composition over inheritance, using simple, often one-method interfaces ... that serve as clean, comprehensible boundaries between components.
>
> -- <cite>Rob Pike, “Go at Google: Language Design in the Service of Software Engineering”</cite>
As an example, the fmt package declares a Stringer interface as follows:
```go
    type Stringer interface {
        String() string
    }
```
The following listing provides a String method to control how the fmt package displays a location.
```go
    package main

    import "fmt"

    // location with a latitude, longitude in decimal degrees.
    type location struct {
        lat, long float64
    }

    // String formats a location with latitude, longitude.
    func (l location) String() string {
        return fmt.Sprintf("%v, %v", l.lat, l.long)
    }

    func main() {
        curiosity := location{-4.5895, 137.4417}
        fmt.Println(curiosity) // Prints -4.5895, 137.4417
    }
```

