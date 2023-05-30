---
title: "Immutable.js Set Deeply Nested Valued with: setIn"
date: 2017-02-27
redirect_from: /immutable-js-set-deeply-nested-valued-with-setin/
---
Using Immutable.js you get to know its function set quite quickly in the beginning. **Set** completely overwrites a property but what if we want to just set a property inside that property?

```
{
  name: 'John',
  children: {
    1: {
      name: 'Lisa',
    }
    2: {
      name: 'Anna',
    },
  },
}
```

So imagine we have a object like that. We can simply use Immutable.**set** to change John to something else with

```
state.set('name', 'Richard')
```

But if we want to change name of one of John’s children? Then we have to go deeper into the tree with Immutable.**setIn**:

```
state.setIn(['children', 1, 'name'], 'Jennifer')
```

**Notice the array syntax!**

This way we can set as deep value as we want and we don’t have to completely overwrite the children object.