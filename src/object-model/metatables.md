# Metatables

Metatables are the core feature of Snap's object model. Every table has 
a "metatable". Be default, the metatable is `nil`. When a queried property
is missing from a table, it's metatable chain is queried bottom up for the
same key.

```snap
const tbl  = { a: 1, b: 2 }
const meta = { c: 3, d: 4 }

setmeta(tbl, meta) -- set tbl's meta table to meta

print(tbl.a, tbl.b, tbl.c, tbl.d) -- 1 2 3 4
```

The `setmeta` builtin function can be used to set a table's metatable.
When a property field is not found in a table itself, it's metatable is
queried for the same.