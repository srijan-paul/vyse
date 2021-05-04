# Syntax


### Comments
Comments are ignored by the interpreter completely.
Single line comments begin with `--` and Multiline comments
are between `/*` and `*/`.

```vyse
-- Single line comment
/* multi
   line
   comment
*/
```

### Blocks

Blocks demarcate chunks of code. Variable declarations inside a block will shadow
the declarations in the outer scope.

```vyse
const pet = 'rabbit'

{
  const pet = 'cat'
  print(pet) -- cat
}

print(pet) -- 'rabbit'

```

### Strings

Strings in Vyse are surrounded either in single quote or double quotes,
and may contain newlines. Note that strings can only contain ASCII characters
at the moment, and you will have to use utf8 library to work with strings containing
utf8 characters.

```vyse
const mystring = "Hello! This is a string";
const myotherstring = " This
  string
  spans
  multiple
  lines";
```

### Keywords

Vyse has very few keywords that you'll need to keep in mind.
These words are reserved and cannot be used as variable names.

```
let const while for in fn break 
class true false if else
```
