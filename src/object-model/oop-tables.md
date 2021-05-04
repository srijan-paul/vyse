# OOP with tables

Equipped with the knowledge of [prototypes](./prototype.html) and [methods](./methods.html),
we are now ready to explore vyse's object oriented programming capabilities.

To demonstrate, we will start off by designing a simple 2D Vector class.
For now, let's just assume the following simple features:

- Create a 2D vector with `Vec2:make(x, y)`
- Access `x` and `y` properties as `v.x` and `v.y`.
- Calculate a vector's magnitude with `v:mag()`.

```vyse
const Vec2 = {
  make(x, y) {
    const v = {x: x, y: y}
    setproto(v, self)
    return v
  }

  mag() {
    return math.sqrt(self.x ** 2 + self.y ** 2)
  }
}
```

Writing simple tests for the vector class doesn't take a lot of effort.

```vyse
let pt = Vec2:make(2, 3) -- 1
assert(pt.x == 2 and pt.y == 3) -- 2
assert(pt:mag() == 13) -- 3
```

The `assert` builtin throws an error if the first argument is falsy (either `false` or `nil`).
Given the implementation of `Vec2` class we described, the above assertions should pass.

`Vec2` is a table with 2 member functions, `make` and `mag`.
The `make` method first creates an empty table `v` and sets it's `x` and `y` fields to the provided
parameters. Next, the prototype of `x` is set to `Vec2` itself.

We then create `pt`, an 'instance' of `Vec2` (line 1).

The table `pt` itself doesn't have any immediate member called 'mag', so when the lookup is performed
for a method with the name `mag` in line 3, the `mag` method from the original `Vec2` class is instead used.

### Inheritance

Inheritance can similarly be modelled with prototypes and the `setproto` builtin.
Imagine you're writing code for your command line roguelike game.

```vyse
const Enemy = {
  make(x, y, hp) {
    const e = {}
    e.pos = Vec2:make(x, y)
    e.hp = hp
    return setproto(e, self)
  }

  log() {
    print(self.pos.x, self.pos.y)
  }
}
```

This table is now ready to serve as our base enemy class that other
classes can derive from. An enemy is capable of holding some data and
displaying it's position.

```vyse
const Goblin = {
  make(x, y, hp, dmg) {
    const gob = Enemy:make(x, y, hp)
    gob.damage = dmg
    return setproto(gob, self)
  }

  attack(target) {
    print("stole ", damage, "gold from", target)
  }
}

setproto(Goblin, Enemy)
```

The call to `setproto` on the last line sets `Goblin`'s base class (prototype) to `Enemy`.

```vyse
const spleen = Goblin(0, 0, 10, 2)
spleen:log() -- 0 0 
spleen:attack('squee') -- stole 2 gold from squee
```

Our character spleen is now able to exhibit the behavior of both an Enemy and a Goblin.
This simple object modelling strategy can be expanded to multiple facets of software
architechture in vyse.
