# The build system

Quip's build system is embedded into the compiler itself. That means you don't have to install and use separate build tools.

The build system relies heavly on standard library and `build.quip` script located in the project root. Here I will show only the basic usage, to read more about it, please read [build documentation]().

## Creating a new project

Quip compiler allows you to initialize a new project using simple commnad.

Navigate to your projects directory and run the following commands on any OS:
```sh
quipc init hello_build
cd hello_build
```

The first command initializes a new project with the name `hello_build`. Next command enters the newly created project directory. You can list the files and see that the compiler has created project structure for you.

```
hello_build/
  - .gitignore
  - build.quip
  - src/
    - main.quip
```

Open `build.quip` in the editor of your choice. It should contain a default `build.quip` script that looks like in Listing 1-1.

```quip
// build.quip

@pure @const {
    make std: unit = @import "std/pkg.quip"
}

@pub @entry
make build (argc: int, argv: ptr<char>[]) -> int {
    make b = std::Build.from_args(argv) catch {
        std::progress::fail("invalid build arguments")
        std::progress::finish(true)
        return 1
    }

    std::progress::begin("Project build", b.progress_enabled, b.options.show_quipc_debug)
    std::progress::phase("Configure", 0, 1, "project")

    // b.options.hide_warnings = true

    make exe = std::Executable.default()
    exe.add_import("std", "~/.quip/current/lib/std/pkg.quip") // creates global alias to standard library

    b.add_executable(exe)

    b.proceed() catch {
        std::progress::fail("failed to build the project")
        std::progress::finish(false)
        return 1
    }

    std::progress::finish(true)
    return 0
}
```
*Listing 1-1: Default `build.quip` script.*

This script may look a little overwhelming but this is becuase a lot of it is boilerplate code that you don't need to worry about. The script is fully customizable and you can add your logic or remove parts of it as needed. 

You can also get simplified build script that does the same but contains less boilerplate (Listing 1-2). To use it, just add a flag `--simple-build` during project initialization.

```quip
// build.quip

@pure @const {
    make std: unit = @import "std/pkg.quip"
}

@pub @entry
make build (argc: int, argv: ptr<char>[]) -> int {
    make b = std::Build.from_args(argv) catch {
        return 1
    }
    
    // b.options.hide_warnings = true

    make exe = std::Executable.default()
    exe.add_import("std", "~/.quip/current/lib/std/pkg.quip") // creates global alias to standard library

    b.add_executable(exe)

    b.proceed() catch {
        return 1
    }

    return 0
}
```
*Listing 1-2: Simplified `build.quip` script.*

Let's focus on the `build()` function in more detail. After running `quipc build`, the compiler finds the build script, compiles and executes it with `build()` as entry point.

The `b` variable is an instance of `std::Build` which holds informations about the build process and allows you to customize the build behavior. Next the `exe` variable is an instance of `std::Executable` which holds informations about the executable to be built. A lot the boilerplate is filled in for you by the `.default()` function, but you can still access the underyling fields to customize the executable. For more details check [build documentation](). Next the `.add_import()` creates a global alias to the standard library path, so you can use `@import "std"` instead of the full path. You can do it for any package you want to use. The `.add_executable()` function takes the instance of `exe` and adds it to the build process. You can create multiple executable targets by creating multiple instances of `std::Executable` and adding them to the build process. The build will automatically compile and link them for you as separate executables in specified output directories (the defualt one is `target/<profile>/<executable name>`).

If you want to build and run the executable use `quipc run`. It will use the build script and the run the executable. If multiple executable targets are defined, the build system will tell you to set the default executable to run using `Build.set_default_executable()`. Or you can specifiy which to run using `--name <executable name>`. 

> **Note:** The executable name must match the name of the executable target defined in the build script.
