# Hello, World!

Now that you've installed Quip, you can finally write your first program. It's a little traditional when learning a new programming language to write a little program that prints the text `Hello, World!` to the screen, we will continue with that tradition. 

## Project setup

To get started, create a new directory for your project and navigate to it in your terminal.

For Linux and macOS, enter this:
```sh
mkdir ~/projects
cd ~/projects
mkdir hello_world
cd hello_world
```

Now, create a new source file and call it *main.quip*. Quip files have the `.quip` extension. Now open the `main.quip` file you just created and enter the code below:
```quip
// main.quip (it's just a hint which file you should edit, don't write it)

@pure @const
make std = @import "std/pkg.quip"

@pub @entry
make main () {
    std::io::println("Hello, World!")
}
```

Save the file and return to your terminal. Follow these steps to compile and run your program:

On Linux and macOS:
```sh
quipc compile main.quip
./target/debug/main
```

> I'll use `>` to indicate the output of the program.
```
> Hello, World
```

On Windows:
```sh
quipc compile main.quip
.\target\debug\main.exe
```

The compiler automatically creates a `target` directory in your project. This helps to organize your project structure.
The `debug` directory indicates that the build is in debug mode. You can change to release mode using `--release`. The compilation will take a little longer though but you want to use release mode for production builds. In such case the compiler will create `target/release` directory.

## About the program

Let's take a look at the program in more detail.

```quip
@pure @const
make std = @import "std/pkg.quip"
```

These lines create a constant variable `std` that holds the standard library package. You can use this variable to access the standard library functions, Types and other variables. We'll skip `@pure` tag for now.

Next we have:

```quip
@pub @entry
make main () {
    
}
```

These lines define `main` function and mark it as the entry point of the program using `@entry` tag. The `@pub` tag makes the function public, so it can be called from other modules.

The `()` after `main` indicates that the function takes no arguments. The `{}` block contains the function body.

```quip
std::io::println("Hello, World!")
```

The body of this function uses `std` variable to access `io` unit which contains `println()` function. 
`"Hello, World!"` is a string which is passed as an argument to `println()` function, and the string is printed to the screen. 

Most languages use `;` to separate statements, Quip doesn't require it.

## Compilation

Quip is compiled programming language that means the source code must be "translated" into machine code before it can be executed. That is why, you had to run `quipc compile <source_file.quip>` commnad before running the program.

Many languages like Python or JavaScript are interpreted languages, they don't require compilation step. If you are more familiar with these languages, you might not be used to the concpet of compilation step. 

Compiling a simple program like this with regular `quipc compile` commnad is enough, but as your project grow, you might want to use the build system to automate the compilation process.
