# Higher Order Functions

Functions in class enjoy first class privelege.
All functions can be passed around as arguments, declared in nested scopes
and returned from other functions just like string and number values.

```vyse
fn make_adder(x) {
  return fn(y) {
    return x + y
  }
}

const add10 = make_adder(10)
print(add10(20)) -- 30
print(add10(30)) -- 40
```

Notice how the anonymous function returned by `make_adder` is
able to use the variable `x` even after it goes out of scope.
Functions are able to capture their lexically enclosing environments
and therefore and use variables even after they go out of scope.

All functions in vyse have this property, and are therefore called
'Closures'.

```vyse
fn func() {
  let value = 10
  return {
    set(x) { value = x    },  
    get()  { return value }
   } 
}

const t = func()
print(t.get()) -- 10
t.set(20)
print(t.get()) -- 20
```

Note the consistent behavior of the `get` and `set` methods in
reading from and writing to the same storage location `value`.


Higher order functions can be immensely useful, especially if you
want to use functional programming paradigm and patterns.
