## Data Types 

In total, snap provides the following native data types:
1. number
2. boolean
3. nil 
4. string 
5. list
6. table 
7. function

From the above, only the first 4 are considered *primitive* data types.

## Numbers
A number in snap is a 64-bit double precision IEEE float.
All numeric values in snap are represented using this type.
There are a variety of ways you can write numbers in snap source
code, but they all behave the same way and use the same representation
underneath.

```snap
123
12.3
0xff -- Hex (255)
0b101 -- Binary (5)
1e2 -- Scientific notation (100)
```

## Booleans
Booleans are as simple as you would expect. A boolean can
take up two values, 'true' or 'false'. A value is called
'truthy' if it is considered *"true"* under certain contexts.
For example, an if statement.

```snap
let is_truthy = \x -> {
  if x print('yes')
  else print('no')
} 

is_truthy('a')   -- yes 
is_truthy('')    -- yes
is_truthy(0)     -- yes
is_truthy(1)     -- yes
is_truthy(true)  -- yes
is_truthy({})    -- yes
is_truthy([])    -- yes
is_truthy(false) -- no
is_truthy(nil)   -- no
```

One can run the code snippet above to verify that only
a `false` boolean value or a `nil` value are considered 'falsy'. 
All other values evaluate to `true` when truthy-ness is concerned.

## Nil
The `nil` data type referes to a single `nil` value. It is used to signal 
the absence of any data.

```snap
fn substring(s, from, len) {
  if (strlen(s) < from) return nil
  sub = ''
  for i = 0, len {
    sub = sub .. s[from + len]
  }
  return sub
}
```

Notice how when no other suitable value is found, we return `nil` in the above function.

## String
Strings are a contiguous buffer of ascii characters.
Strings are immutable.
Once created, the contents of a string cannot be changed.

```snap
const s = 'abxde'
print(s[0]) -- a
s[2] = 'c' -- Error: Cannot mutate a string literal.
```

To get a modified string, you have to create a new string.

```snap
const new_s = s:slice(0, 2) .. 'c' .. s:slice(3, 2)
print(new_s) -- abcde
```

The `slice(start, length)` method is used to 'slice' a string by extracting
a substring from it. The original string `s` is left unchanged throughout this
commotion.

Note that while creating strings at runtime can be somewhat expensive compared to 
numbers, booleans and nils, comparing strings with the `==` operator is nearly as
fast as comparing numbers. 
This is because Snap performs string interning to keep
string comparisons fast and efficient.

## List
Lists are similar to dynamic arrays in other programming languages.
A list is declared by putting comma separated elements inside of `[`
and `]`.

- The `#` operator is used to get the length of a list.
- Lists are indexed from `0`.
- The size of lists can change at runtime.
- Indexing a list with an invalid index (-1 or a value greater than it's length) will throw an error.

```snap
let arr = [1, 2, 3]
for el in arr {
  print(el)
}
```

__Common methods and functions on lists__:

- `list:push(item)`: Appends `item` to the end of the list.
- `list:pop()`: Removes the last item from the list and returns it.
- `len(list)`:  Returns the length of the list.
- `list:map(fn)`: Creates a new list `ls` where `ls[i]` is `fn(list[i])`

For more methods and free functions to operate on lists, refer to the standard library
documentation.

## Table
Tables are Snap's core data structure used to store key-value pairs. 
They're similar to `Map`s in JavaScript or tables in Lua.

```snap
const point = { x: 1, y: 2 }
print(point['x'], point.y) -- 1 2
```

Tables are rather simple data structures in terms of usage, but they can
prove to be very powerful. We will see in the coming sections how tables
can be used to model OOP like encapsulation.



