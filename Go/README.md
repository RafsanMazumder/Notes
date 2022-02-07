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
Go enforces the opening brace **{** is on the same line as the **func** keyword, 
whereas the closing brace **}** is on its own line. The Go compiler automatically will
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

