## Variables 

Variable come in two flavors, mutable and immuatble.
Immutable variables once declared, cannot be re-assigned to.

```vyse
const myvar = 10
myvar = 20 -- Error: Attempt to mutate a variable declared 'const'.

let my_other_var = 10
my_other_var = 20 -- Ok
```

Note however, that variables that are `const` can still be mutated
if they are not primitive data types. Only re-assignment is forbidden.

```vyse
const my_table = { my_key: 'my_value' }
my_table.my_key = 123 -- ok

my_table = {} -- Error: Attempt to mutate a variable declared 'const'.
```

## Globals and Locals.

Another way to categorize variables is either as 'locals' or 'globals'.
A global variable is accessible everywhere and is shared across modules.
A local variable is scoped to it's surrounding block.


```vyse
global x = 'global'
let y = 'local'

-- Both globals and locals display similar
-- behavior when shadowed.
{
  x = 123
  y = 456
  z = 789
  print(x, y, z) -- 123 456 789
}

print(x, y, z) -- global local nil
```

All global variables in vyse can be found in special predefined table called '`_G`'.
They can therefore me modified and accessed from the table itself.

```vyse
_G.x = 42
print(x) -- 42
```

At this point, you might be wondering why bother with global variables at all since
they're nearly the same as locals. To answer this, we will explore global variables
further in a later section.
