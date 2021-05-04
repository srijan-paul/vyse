# Cheatsheet 

This section contains a brief overview of the Vyse. If you have some prior experience with programming in C or JS like languages, this should help you cover the basics pretty quickly!

If not, consider this snippet an "Eagle eye view" of the territory. You can copy and paste the following snippet into a file and play around with it.

```vyse
-- comments begin with '--' and are ignored by 
-- the interpreter.
print("Welcome to Vyse!")

-- constants declared with the 'const' keyword
const pi = 3.1415162
-- mutable variables declared with 'let'
let r = input("Enter radius: ")

-- lambda functions
const area = /r -> pi * r ** 2
-- ** for exponents

if r <= 0 {
  print("Radius must be greater than zero!");
} else {
  print("Area = ", area(r)) 
}

-- Functions can alternatively be declared
-- with the 'fn' keyword.
fn make_adder(x) {
  -- Functions can return and recieve
  -- other functions too!
  return fn(y) {
    return x + y
  } 
}

const add10 = make_adder(10)
print('10 + 20 =', add10(20)) -- 10 + 20 = 30

-- Tables are data-structures
-- used to store key-value pairs of any
-- kind.

const Tom = {
  species: 'cat',
  age: 2
}

-- Tables can be indexed with the '.' or '[]' operators.
print('Tom is a', Tom.species)
print('Tom is', Tom['age'], 'years old'.)

-- Arrays are like tables, but they can
-- only be indexed with numeric keys and
-- are better for iterating on.

const my_array = ['ten', 10, false, [1, 2, 3]]

-- The looping syntax is similar to that of Lua
for i = 1, 4 {
  print(my_array[i])
}

-- for loops can take a 3rd operand 'step',
-- which is the amount to change the iterator variable
-- by every iteration. By default, it's value is 1.
for i = 4, 1, -1 {
  -- prints the array items in reverse
  print(my_array[i])
}

-- '#' operator returns the size of an array.
for i = 1, #my_array {
  print(i, my_array[i])
}

-- arrays are 'iterable' and can be iterated upon
-- with a more convinient syntax.
for el in array 
  print(el)


-- Prototypes are a concept that can help
-- simulate OOP in vyse.

const t = { a: 1, b: 2 }
print(t.c) -- nil

-- When a key is not found within the
-- set of the object's own properties,
-- vyse will search the object's 'prototype'
-- (if any) for the property.

const mt = { b: 10, c: 3 }
setproto(t, mt)
print(t.c) -- 3
print(t.b) -- 2

-- Note that a search for a key always begins at
-- the object itself and goes up the prototype chain,
-- so t.b is still 2.

-- OOP
-- Declaring and using classes
-- is very straightforward.
class Animal {
  init(sound) {
    self.sound = sound
  }

  make_sound() {
    print(self.sound)
  }
}

const spike = Animal("woof!")
-- methods are called with ':'
animal:make_sound()

-- classes can be extended with '<'
class Human < Animal {
  init(name) {
    super('hi!') -- super class constructor
    self.name = name
  }

  greet() {
    make_sound()
    print('I am ', self.name)
  }
}

const bob = Human('Bob')
bob:greet() 'Hi! I am Bob'
bob:make_sound() 'Hi!'

```

Note that the cheatsheet above is meant to be an 'overview' and therefore does not include all the features, constructs and details about Vyse.
