# Sublime Text C/C++ Auto completion with `EasyClangComplete`

## [Package Control Link for `EasyClangComplete`](https://packagecontrol.io/packages/EasyClangComplete)

<https://packagecontrol.io/packages/EasyClangComplete>

## [Sources for `EasyClangComplete`](https://github.com/niosus/EasyClangComplete)

<https://github.com/niosus/EasyClangComplete>

## Dependencies needed for `EasyClangComplete`

```sh
sudo apt install clang clang-format
```

In case of Debian based system.
There is also an issue with system unable to locate the `libclang`

Hence in the settings for `EasyClangComplete` we modify the following:

File `EasyClangComplete.sublime-settings` -

```json
{
	  "libclang_path": "/usr/lib/x86_64-linux-gnu/libclang-14.so",
}
```

**Note:** The location of `libclang-*.so` will change based on distribution. And the `*` that is the version of `clang` will also change. Hence this line needs to be updated as per that.

## Optional `.clang_complete` file for `EasyClangComplete`

Normally using the `SublimeText` indexing all files and header files
are located easily. However if you wish to help `EasyClangComplete` to work faster the you can add the `.clang_complete` file.

```
-ILibraries/CMSIS/Device/WIZnet/W7500/Include
-ILibraries/startup
-ILibraries/W7500x_StdPeriph_Driver/inc
```

These lines show that the particular directories need to be included.
Additionally other attributes like `-l<package>` and `-D<define>` can also be used to further target better completion.


----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)
