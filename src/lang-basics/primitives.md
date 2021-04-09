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

## Lists
Lists are similar to arrays in other programming languages.