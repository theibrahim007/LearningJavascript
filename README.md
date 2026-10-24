# LearningJavascript

# JavaScript Notes: `var`, `let`, and `const`

## 1. What are Variables in JavaScript?

A **variable** is a container used to store data in a program.

Example:

```javascript
let name = "Ali";
let age = 20;

console.log(name);
console.log(age);
```

**Output:**
```text
Ali
20
```

JavaScript provides three main keywords to declare variables:

- `var`
- `let`
- `const`

---

## 2. Difference Between `var`, `let`, and `const`

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Reassignment | Allowed | Allowed | Not allowed |
| Redeclaration in same scope | Allowed | Not allowed | Not allowed |
| Scope | Function scope | Block scope | Block scope |
| Initialization required | No | No | Yes |
| Hoisting | Initialized as `undefined` | Temporal Dead Zone | Temporal Dead Zone |

### Easy way to remember

- `var` — older way to declare variables.
- `let` — use when the value needs to change.
- `const` — use when the variable should not be reassigned.

---

# 3. The `var` Keyword

`var` is an older keyword used to declare variables in JavaScript.

### Example 1: Declaring a variable

```javascript
var name = "Ali";

console.log(name);
```

**Output:**
```text
Ali
```

### Example 2: Changing a value (Reassignment)

```javascript
var age = 20;
age = 25;

console.log(age);
```

**Output:**
```text
25
```

**Explanation:** We first assign `20` to `age`. Then we change its value to `25`.

### Example 3: Redeclaring a variable

```javascript
var age = 20;
var age = 30;

console.log(age);
```

**Output:**
```text
30
```

**Explanation:** `var` allows the same variable to be declared again in the same scope.

### Example 4: Function scope

```javascript
function test() {
    var x = 10;
    console.log(x);
}

test();
```

**Output:**
```text
10
```

**Explanation:** The variable `x` is accessible inside the function where it is declared.

### Example 5: `var` inside a block

```javascript
if (true) {
    var x = 10;
}

console.log(x);
```

**Output:**
```text
10
```

**Explanation:** `var` is not limited to the `if` block. It is scoped to the surrounding function, or globally if declared outside a function.

---

# 4. The `let` Keyword

`let` is used to declare variables whose values may change.

### Example 1: Declaring a variable

```javascript
let city = "Mumbai";

console.log(city);
```

**Output:**
```text
Mumbai
```

### Example 2: Changing a value

```javascript
let score = 50;
score = 100;

console.log(score);
```

**Output:**
```text
100
```

**Explanation:** You can change the value of a variable declared with `let`.

### Example 3: Redeclaration

```javascript
let age = 20;
let age = 30;

console.log(age);
```

**Output:** `SyntaxError`

**Explanation:** You cannot declare the same `let` variable twice in the same scope.

However, reassignment is allowed:

```javascript
let age = 20;
age = 30;

console.log(age);
```

**Output:**
```text
30
```

### Example 4: Block scope

A **block** is a section of code enclosed in curly braces `{ }`.

```javascript
if (true) {
    let number = 10;
    console.log(number);
}

console.log(number);
```

**Output:**
```text
10
ReferenceError
```

**Explanation:** The variable `number` exists only inside the `if` block. It cannot be accessed outside that block.

---

# 5. The `const` Keyword

`const` is used to declare variables that cannot be reassigned.

### Example 1: Declaring a constant

```javascript
const country = "India";

console.log(country);
```

**Output:**
```text
India
```

### Example 2: Reassignment is not allowed

```javascript
const price = 500;
price = 1000;

console.log(price);
```

**Output:** `TypeError`

**Explanation:** You cannot assign a new value to a variable declared with `const`.

### Example 3: Initialization is required

```javascript
const age;
```

**Output:** `SyntaxError`

**Explanation:** A `const` variable must receive a value when it is declared.

Correct example:

```javascript
const age = 20;
```

### Example 4: Block scope

```javascript
if (true) {
    const number = 30;
    console.log(number);
}

console.log(number);
```

**Output:**
```text
30
ReferenceError
```

**Explanation:** Like `let`, `const` is limited to the block where it is declared.

---

# 6. What Is Scope?

**Scope** determines where a variable can be accessed in a program.

There are three common scope concepts to understand.

### A. Global scope

A variable declared outside functions and blocks can generally be accessed throughout its applicable global scope.

```javascript
let name = "Ali";

function greet() {
    console.log(name);
}

greet();
console.log(name);
```

**Output:**
```text
Ali
Ali
```

### B. Function scope

A variable declared with `var` inside a function is accessible within that function, but not outside it.

```javascript
function test() {
    var x = 10;
    console.log(x);
}

test();
console.log(x);
```

**Output:**
```text
10
ReferenceError
```

### C. Block scope

Variables declared with `let` and `const` inside a block are accessible only within that block.

```javascript
if (true) {
    let a = 10;
    const b = 20;

    console.log(a);
    console.log(b);
}
```

**Output:**
```text
10
20
```

Trying to access `a` or `b` outside the block causes a `ReferenceError`.

---

# 7. Understanding Objects with `const`

An **object** stores related data as properties.

Example:

```javascript
const student = {
    name: "Ali",
    age: 20
};

console.log(student.name);
console.log(student.age);
```

**Output:**
```text
Ali
20
```

### Example 1: Changing an object's property

```javascript
const student = {
    name: "Ali",
    age: 20
};

student.age = 21;

console.log(student.age);
```

**Output:**
```text
21
```

**Explanation:** This works because we are changing the `age` property, not reassigning the `student` variable.

The object now contains:

```javascript
{
    name: "Ali",
    age: 21
}
```

### Example 2: Reassigning the object

```javascript
const student = {
    name: "Ali",
    age: 20
};

student = {
    name: "Ahmed",
    age: 25
};
```

**Output:** `TypeError`

**Explanation:** A variable declared with `const` cannot be reassigned to a different object.

### Important rule

- You can modify an object's properties declared using `const`.
- You cannot reassign the variable to a different object.
- `const` does not automatically make an object immutable.

---

# 8. What Is `Object.freeze()`?

JavaScript provides `Object.freeze()` to prevent changes to an object's existing properties.

Example:

```javascript
const student = Object.freeze({
    name: "Ali",
    age: 20
});

student.age = 21;

console.log(student.age);
```

**Output:**
```text
20
```

**Explanation:** The object is frozen, so its `age` property cannot be changed.

Note: `Object.freeze()` is shallow. Properties of nested objects can still change unless those objects are frozen separately.

---

# 9. What Is Hoisting?

**Hoisting** is JavaScript's handling of declarations before code execution.

### Example 1: `var`

```javascript
console.log(x);
var x = 10;
```

**Output:**
```text
undefined
```

**Explanation:** The `var` declaration is hoisted and initialized with `undefined`.

### Example 2: `let`

```javascript
console.log(x);
let x = 10;
```

**Output:** `ReferenceError`

### Example 3: `const`

```javascript
console.log(x);
const x = 10;
```

**Output:** `ReferenceError`

**Explanation:** `let` and `const` are also hoisted, but they cannot be accessed before their declarations are evaluated. This period is called the **Temporal Dead Zone (TDZ)**.

---

# 10. Comparison of All Three

```javascript
var a = 10;
a = 20;

let b = 30;
b = 40;

const c = 50;

console.log(a);
console.log(b);
console.log(c);
```

**Output:**
```text
20
40
50
```

**Explanation:**

- `a` changes from `10` to `20`.
- `b` changes from `30` to `40`.
- `c` remains `50` because it cannot be reassigned.

---

# 11. When Should You Use Each Keyword?

### Use `const` by default

```javascript
const pi = 3.14159;
const username = "Ali";
```

Use it when you do not need to reassign the variable.

### Use `let` when a value needs to change

```javascript
let score = 0;

score = score + 10;

console.log(score);
```

**Output:** `10`

### Avoid `var` in most new JavaScript code

Use `let` and `const` instead because their block-scoping behavior makes code easier to understand and helps avoid certain mistakes.

---

# 12. Practice Questions

### Question 1

```javascript
var x = 5;
x = 15;

console.log(x);
```

Answer: `15`

### Question 2

```javascript
let a = 10;
let a = 20;
```

Answer: `SyntaxError`

### Question 3

```javascript
const pi = 3.14;
pi = 4;
```

Answer: `TypeError`

### Question 4

```javascript
if (true) {
    let x = 100;
}

console.log(x);
```

Answer: `ReferenceError`

### Question 5

```javascript
const user = {
    name: "Ali"
};

user.name = "Ahmed";

console.log(user.name);
```

Answer: `"Ahmed"`

### Question 6

```javascript
var x = 10;

if (true) {
    var x = 20;
}

console.log(x);
```

Answer: `20`

Explanation: Both declarations refer to the same function-scoped or global variable.

---

# 13. Final Summary

| Keyword | Main rule |
|---|---|
| `var` | Can be reassigned and redeclared; function-scoped |
| `let` | Can be reassigned, but cannot be redeclared in the same scope; block-scoped |
| `const` | Cannot be reassigned or redeclared in the same scope; block-scoped |

**Best practice for modern JavaScript:**

1. Use `const` when you do not need to reassign a variable.
2. Use `let` when you need to reassign a variable.
3. Avoid `var` in most new code.

Remember: **`const` prevents reassignment, not all changes to the data stored in an object.**
