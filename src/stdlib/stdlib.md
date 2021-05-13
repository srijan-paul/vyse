# Standard Library

This section covers the Vyse standard library.
Note that this section will be updated frequently as new versions of Vyse are released.
The standard library is split into 3 separate categories:
  - Base
  - Prototypes
  - Modules

## Base
The base standard library contains common functions that are needed very often. All functions
in this library are available as global variables and can be accessed from any Vyse script. Examples
include `print`, `input`, `byte` etc.

## Prototypes
Whenever indexing a value that isn't a table, it's prototype is used instead.
This is how `"abcd":code_at(0)` is able to return the ascii code of 'a'.

When using the `:` operator on strings, the lookup is instead performed on the `String` table,
which is the prototype to all strings. Similarly, there exist the following prototypes for non-table
values:

- [List](./list.md)
- [String](./string.md)
- [Number](./number.md)
- [Bool](./bool.md)

All these prototypes are available globally. So the snippet below prints true
```vyse
print("abc":code_at(0) == String.code_at("abc", 0)) -- true
```

## Modules
Apart from the base library and primitives, there exist some code modules that can be imported
using the `import` builtin. The modules supported as of now are listed below.

| Module            | Description                                                                        |
|-------------------|------------------------------------------------------------------------------------|
| [os](./os.md)     | The OS library, providing some common utilities like telling the time.             |
| [io](./io.md)     | The I/O library, has utilities for reading/writing files and crawling directories. |
| [math](./math.md) | Has `random`, `sqrt`, `cos`, `sin` and other math utility functions.               |
