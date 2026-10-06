## `var` vs `let` vs `const`

| Feature                   | `var`    | `let` | `const` |
| ------------------------- | -------- | ----- | ------- |
| Scope                     | Function | Block | Block   |
| Redeclare                 | ✅ Yes    | ❌ No  | ❌ No    |
| Reassign                  | ✅ Yes    | ✅ Yes | ❌ No    |
| Initialize at declaration | ❌ No     | ❌ No  | ✅ Yes   |

### Example

```js
var a = 10;
var a = 20; // ✅ Redeclare
a = 30;     // ✅ Reassign

let b = 10;
b = 20;     // ✅ Reassign
// let b = 30; // ❌ Redeclare

const c = 10;
// c = 20;    // ❌ Reassign
// const c = 30; // ❌ Redeclare
```

### Remember

`var` → **Redeclare + Reassign**
`let` → **Reassign**
`const` → **Neither**

### Interview Trap

`const` objects/arrays can still be modified. The variable itself cannot be reassigned.


## closure
- A closure is created when an inner function remembers and can access variables from its outer lexical scope even after the outer function has finished execution.
