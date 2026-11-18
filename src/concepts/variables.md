# Variables

> **Keywords**
>
> A set of words that have special meaning for Quip, and any other programming language. You cannot use them as variable or function names. Most of them are used for various tasks in Quip.

In Quip every variable is mutable. That means you can change the value of the variable after it's been declared. To create a variable in Quip, use `make` keyword, followed by the variable name and value.

```quip
// src/main.quip

@pub @entry
make main () {
    make variable = 10
    std::io::println(variable.to_str())
}
```

Save and run the program using `quipc run`. You'll see `10` printed to the console.

## Constants

Constants are immutable variables that are declared using `make` keyword and `@const` tag before it. Their value cannot be changed after they're declared.

```quip
// src/main.quip

@pub @entry
make main () {
    @const make constant = 10
    constant = 20
    
    std::io::println(constant.to_str())
}
```

Save and run the program using `quipc run`. You'll see an error message:
```
error[E1015]: cannot mutate an `@const` binding
 --> src/main.quip:9:5
   |
 3 |     @const make variable = 10
 4 |     variable = 12
   |     ^^^^^^^^
 5 |
   |
```

The compiler throws errors when it sees you wrote a code that isn't safe. You might ask, "If compiler detects unsafe code, why doesn't it modify the code to mae it safe?". The answer is simple, compiler isn't there to secretly modify your code to make it safe, it is designed to strictly enforce safety. Fighting the compiler may be frustrating, but it's important to write safe code. It's about habit and good coding practices.

## Redeclaration

Quip doesn't support redeclaration of variables. Meaning you cannot create a new variable with the same name as an existing variable, function, Type, etc.

```quip
@pub @entry
make main () {

    make a = 10
    make a = "Hello, World!"
    
}
```

```
error[E1007]: duplicate symbol `a`
 --> src/main.quip:8:10
   |
 2 | make main () {
 4 |     make a = 10
   |          ------
   |          |
   |          previous binding declared here
 5 |     make a = "Hello, World!"
   |          ^^^^^^^^^^^^^^^^^^^
 7 | }
   |
  = help: rename the new binding, assign to the existing binding, or use `_` to discard the value
```
