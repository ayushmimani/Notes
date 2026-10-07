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

## Why are they used?

`call()`, `apply()`, and `bind()` are used to **explicitly control the `this` value** of a function.

---

## 1. call()

`call()` **immediately executes** the function with a specified `this`.

Arguments are passed **individually**.

```js
function greet(city, age) {
  console.log(this.name, city, age);
}

const user = {
  name: "Ayush"
};

greet.call(user, "Mumbai", 26);
```

### Remember

**call = Call now + arguments individually**

---

## 2. apply()

`apply()` also **immediately executes** the function with a specified `this`.

Arguments are passed as an **array**.

```js
function greet(city, age) {
  console.log(this.name, city, age);
}

const user = {
  name: "Ayush"
};

greet.apply(user, ["Mumbai", 26]);
```

### Remember

**apply = Call now + arguments as Array**

---

## 3. bind()

`bind()` **does not execute the function immediately**.

It returns a **new function** with `this` permanently bound to the specified object.

```js
function greet(city) {
  console.log(this.name, city);
}

const user = {
  name: "Ayush"
};

const newGreet = greet.bind(user, "Mumbai");

newGreet();
```

### Remember

**bind = Bind now + execute later**

---

## Difference

| Method    | Executes immediately? | Arguments                |
| --------- | --------------------- | ------------------------ |
| `call()`  | ✅ Yes                 | Individually             |
| `apply()` | ✅ Yes                 | Array                    |
| `bind()`  | ❌ No                  | Individually / partially |

---

## Common Use Case: Function Borrowing

One object can use another object's method:

```js
const person1 = {
  name: "Ayush",

  greet() {
    console.log(this.name);
  }
};

const person2 = {
  name: "Rahul"
};

person1.greet.call(person2);
```

Output:

```text
Rahul
```

Here, `person2` **borrows** the `greet()` method from `person1`.

---

## Interview Answer

> **“`call()`, `apply()`, and `bind()` are used to explicitly control the `this` value of a function. `call()` and `apply()` execute the function immediately, while `bind()` returns a new function for later execution. The difference between `call()` and `apply()` is that `call()` accepts arguments individually, whereas `apply()` accepts them as an array.”**

## 🧠 Quick Memory

```text
call  → NOW + individual arguments
apply → NOW + array arguments
bind  → LATER + returns function
```

### Map, Filter and Reduce
Interview Answer

“map() is used to transform every element and returns a new array. filter() is used to select elements based on a condition and returns a new array. reduce() is used to accumulate array elements into a single result such as a sum, object, or another value.”


### Currying
# Currying in JavaScript

## What is Currying?

**Currying** ka matlab hai ek function jo **multiple arguments ek saath leta hai**, usko aise **functions ki chain** mein convert karna jahan har function **ek-ek argument leta hai**.

> **Multiple arguments → One-by-one functions**

---

## Normal Function

```js
function add(a, b, c) {
  return a + b + c;
}

add(1, 2, 3); // 6
```

## Curried Function

```js
function add(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}

add(1)(2)(3); // 6
```

### Arrow Function

```js
const add = a => b => c => a + b + c;

add(1)(2)(3); // 6
```

---

## How It Works

```text
add(1)
   ↓
returns function(b)

(2)
   ↓
returns function(c)

(3)
   ↓
returns result

1 + 2 + 3 = 6
```

---

## Why Use Currying?

* Function reuse
* Partial application
* Create specialized functions
* Useful in functional programming

### Example

```js
const multiply = a => b => a * b;

const double = multiply(2);
const triple = multiply(3);

double(5); // 10
triple(5); // 15
```

Here:

```text
multiply(2) → creates double function
multiply(3) → creates triple function
```

---

## 🧠 Remember

> **Currying = Ek function ko one-argument functions ki chain mein convert karna.**

## Interview Answer

> **“Currying is a technique of converting a function that takes multiple arguments into a sequence of functions, where each function takes one argument and returns another function until all arguments are provided.”**

### CORS
- CORS is a browser security mechanism that controls whether a web application from one origin can access resources from another origin.


