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



  ##Debounce
 # Debouncing

## What is Debouncing?

**Debouncing** is a technique that delays function execution until the user stops triggering an event for a specified amount of time.

> **Debounce = Wait until the event stops.**

## Example

```js
function debounce(fn, delay) {
  let timer;

  return function (...args) {
    clearTimeout(timer);

    timer = setTimeout(() => {
      fn(...args);
    }, delay);
  };
}

const search = debounce((value) => {
  console.log("API Call:", value);
}, 500);
```

## How It Works

```text
User types
   ↓
Timer starts
   ↓
User types again
   ↓
Previous timer cancelled
   ↓
New timer starts
   ↓
User stops typing
   ↓
500ms passes
   ↓
Function executes
```

## Real-World Example

Search box:

```text
A → Ay → Ayu → Ayus → Ayush
```

Without debounce:

```text
5 API calls
```

With debounce:

```text
1 API call
```

## Common Use Cases

* Search/autocomplete
* API calls
* Input validation
* `keyup`
* `resize`

## Debounce vs Throttle

| Debounce               | Throttle                   |
| ---------------------- | -------------------------- |
| Runs after events stop | Runs at fixed intervals    |
| Search input           | Scroll events              |
| Waits for inactivity   | Limits execution frequency |

## Interview Answer

> **“Debouncing is a technique that delays function execution until a specified time has passed since the last event. If the event occurs again before that time, the previous timer is cancelled. It is commonly used for search inputs to prevent unnecessary API calls.”**

## Remember

**Debounce → User stops → Wait → Execute**


### call(), apply() and bind()
call() and apply() both invoke a function immediately with a specified this value. The difference is that call() accepts arguments individually, while apply() accepts them as an array. bind() does not execute the function immediately; it returns a new function with this bound to the specified object
