# Installation

> **Note:** You'll need internet connection to install Quip.

The following steps install latest stable version of the compiler. Any newer version will be compatible with the content of this book.

Quip doesn't use any package managers or third-party tools. The only way to install the compiler is to use the installation script or download the binary from the repository. 

> Currently the second option is not implemented yet. Use the script to install the compiler.

## Installing Quip compiler on macOS

Open a terminal and enter the following command:

```sh
curl -fsSL https://raw.githubusercontent.com/quiplang/quipc/main/install.sh | sh
```

The command uses latest version of the script (located in the `main` branch if the repository). It will download and install the compiler. You may be prompted to enter your password.

You'll also need a *linker*, which is a program that stitches together all compiled outputs into one file. You may already have one installed. If you get
linker errors, you should install a C compiler, which typically include it. The C compiler may also be useful for other C/C++ projects or compiling dependencies.

On macOS, you can get a C compiler by running the following command in the terminal:

```sh
xcode-select --install
```

## Installing Quip compiler on Linux

Platform currently not tested. Check out the [roadmap](../roadmap.md)


## Installing Quip compiler on Windows

Platform currently not supported.

## Manual installation on macOS

Download appropriate binary for you system from the repository. Create a `.quip` directory inside your home directory and place the binary in the `~/.quip/current/bin/` directory. You'll also need to download the standard library and place it in the `~/.quip/current/lib/` directory.

Once you have downloaded the binary and the standard library, you can add the `~/.quip/current/bin/` directory to your `PATH` environment variable.

```sh
export PATH=~/.quip/current/bin:$PATH
```

Then restart your terminal or run `source ~/.bashrc` (if using Bash) or `source ~/.zshrc` (if using Zsh) to apply the changes.

> Next time you update the compiler by using `update` command, the compiler will replace the current version with the latest one and the PATH will be updated automatically. 

## Updating and uninstalling 

You can update the compiler using the same script used for installation or by running the following command in the terminal:
```sh
quipc update
```

To uninstall the compiler, run the following command in the terminal:
```sh
quipc uninstall
```

You'll be prompted to confirm the uninstallation.

> **Note:** Currently `update` and `uninstall` are not implemented yet.

## Text editors

You can use any editor of your choice to write Quip code.
