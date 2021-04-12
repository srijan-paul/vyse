# Operator Overloading

Snap has several logical and arithmetic operators.
The behavior of these operators are well defined when the operands
are of the expected data types (e.g `number` operands for `+`).

It is also possible to define the behavior of several of these 
operators for user-defined data types.

## Example

Let us recollect the implementation of a simple Vector class defined
[earlier](./oop-tables.html).

```snap
const Vec2 = {
  make(x, y) {
    const v = {x: x, y: y}
    setmeta(v, self)
    return v
  }

  mag() {
    return math.sqrt(self.x ** 2 + self.y ** 2)
  }
}
```
Vectors are very often used in data visualization and game programming.
We would like to include the functionality to add together two vectors.
This can very easily be done by attaching a method.

```snap
fn Vec2.add(a, b) {
  return Vec2:make(a.x + b.x, a.y + b.y)
}
```

We can now add together vectors by calling this method that behaves like a
static member.

```snap
const a = Vec2:make(1, 2)
const b = Vec2:make(2, 3)

const c = Vec2.add(a, b)
print(c.x, c.y) --  3 5
```

It is often advantageous to both the programmer and the reader to use the usual
mathematical symbols (here `+`) when defining such constructs. For instance, many
would prefer `a + b` over `Vec2.add(a, b)`. This is made possible in snap with the
help of meta methods. For the `+` operator, the `__add` metamethod is used.

```snap
fn Vec2.__add(a, b) {
  return Vec2:make(a.x + b.x, a.y + b.y)
}
```

Once a metamethod is defined on an object's metatable, this is called whenever
the event associated with the metamethod is invoked. Now, we can add together
vectors with the `+` operator. 

(Note that we use `Vec2.__add` when defining the method instead of `:`. We do not
want any hidden `self` parameter in the metamethod)

```snap
const a = Vec2:make(1, 2)
const b = Vec2:make(2, 3)

const c = a + b
print(c.x, c.y) -- 3 5
```

## Overloadable operators

A table representing all the overloadable operators
and the method names is listed below for reference:

| Operator          | Method     | Arity   |
| :---------------- | :--------- | :------ |
| +                 | \_\_add    | 2       |
| + (unary)         | \_\_unp    | 1       |
| -                 | \_\_sub    | 2       |
| - (unary)         | \_\_unm    | 1       |
| /                 | \_\_div    | 2       |
| %                 | \_\_mod    | 2       |
| \*\*              | \_\_exp    | 2       |
| >                 | \_\_gt     | 2       |
| <                 | \_\_lt     | 2       |
| >=                | \_\_gte    | 2       |
| <=                | \_\_lte    | 2       |
| !                 | \_\_not    | 1       |
| ^                 | \_\_xor    | 2       |
| &                 | \_\_band   | 2       |
| \|                | \_\_bor    | 2       |
| <<                | \_\_bsl    | 2       |
| >>                | \_\_bsr    | 2       |
| ~                 | \_\_bnot   | 1       |
| .                 | \_\_indx   | 2       |
| ==                | \_\_eq     | 2       |
| !=                | \_\_neq    | 2       |
| ..                | \_\_concat | 2       |
| ()                | \_\_call   | any     |
| [string coercion] | \_\_tostr  | 1       |