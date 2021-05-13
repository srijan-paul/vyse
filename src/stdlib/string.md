# String
The globally available `String` table serves as the prototype to all string values in Vyse. Calling
a method on any string is equivalent to calling `String.method_name(str, ..args..)`

  - substr
  - byte
  - code_at
  - to_number
  - replace
  - repeat
  - reversed
  - split
  - index_of


<div class="doc-fn">

### substr(string, start, [len])
- **start**: number
- **len**: number
- **return**: string

Returns a substring of `string` starting from position `start` that is `len` characters long.
If `len` isn't provided, then the suffix of the string starting at `start` is returned.
```vyse
print("abcdef":substr(3, 2)) -- de
print("abcdef":substr(3)) -- def
```
</div>

<div class="doc-fn">

### code_at(string, index)
- **index**: number
- **return**: number

Returns the ascii code of the character present at position `index` in string.
```vyse
print("abcdef".code_at(0)) -- 97
```
</div>


<div class="doc-fn">

### to_number(string)
- **return** number

Returns the base 10 number representation of the string.

```vyse
print(10 + '10':to_number()) -- 20
```

</div>

<div class="doc-fn">

### replace(string, to_replace, with)
- **to_replace**: string
- **with**: number
- **return**: string

Replaces all occurences of `to_replace` with `with` in `string`.

```vyse
print("she sells sea shells on the sea shore":replace("she", "he"))
-- he sells sea hells on the sea shore
```
</div>