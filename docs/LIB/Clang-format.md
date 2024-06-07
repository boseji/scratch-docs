# `clang-format` LLVM C/C++ Code formatter

## Installing `clang-format`

### Installing `clang-format` under Debian based Linux 

```sh
sudo apt install clang clang-format clang-tidy
```

## Installing `clang-format` under Windows

Install [LLVM](https://llvm.org/) Compiler.

```bat
winget install -e --id LLVM.LLVM -y
```

Make sure to add the `c:\Program Files\LLVM\bin\` path to environment.

## Formatting using default LLVM style in `clang-format`

```sh
clang-format -i *.c *.cpp *.h src/*.c inc/*.h
```

This would update the formatting in place.

## Generate the `.clang-format` file

```sh
clang-format -style=llvm -dump-config > ./.clang-format
```

This helps VS Code and other IDEs to figure out what kind of auto format
is needed for C/C++ code.

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)

