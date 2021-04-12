# Methods

Tables can have properties that are functions. Functions can either be invoked normally by
accessing them or by using the `:` operator. When called using `:`, the functions behave as methods.
```snap
const cat = {
  sound: 'meow'
  speak: fn (self) {
    print(self.sound)
  }
}

cat:speak() -- 'meow'
cat.speak(cat) -- 'meow'
```

Note that `table:method()` is equivalent to `table.method(table)`.
Methods have an extra first parameter that refers to the table
itself. By convention, this parameter is called 'self'. But any other name
also suffices.

### Shorthand Syntax

To make methods look more natural and convenient, there exists a short-hand
syntax.

```snap
const dog = {
  sound: 'woof!',
  speak() {
    print(self.sound)
  }
}

dog:bark() -- woof!
dog.bark(dog) -- woof!

-- Can also be called like a free function
-- on other objects.
dog.bark(cat) -- meow
```
The `self` parameter is implicit and hidden when a method is defined with the shorthand
syntax.

### Defining Methods Outside A Table.
Methods can be declared outside the table's body with the usual function
definition syntax.

```snap
const cat = { sound = 'meow' }

fn cat:meow() {
  print(self.sound)
}

cat:mow() -- 'meow'
```

Methods will later come in handy when we delve into the object oriented programming
model.