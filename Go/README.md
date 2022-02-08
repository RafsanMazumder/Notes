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

### ASCII to Integer
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