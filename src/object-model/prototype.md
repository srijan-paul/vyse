# Prototypes 

Protoypes are the core feature of Snap's object model. Every table has 
a "prototype" table (also called proto-table).
By default, the prototype is `nil`.
When a queried property is missing from a table, it's prototype chain is queried bottom up for the same key.

```snap
const tbl   = { a: 1, b: 2 }
const proto = { c: 3, d: 4 }

setproto(tbl, proto) -- set tbl's meta table to meta

print(tbl.a, tbl.b, tbl.c, tbl.d) -- 1 2 3 4
```

The `setproto` builtin function can be used to set a table's prototype.
When a property field is not found in a table itself, it's prototype is
queried for the same.