# JavaScript and TypeScript Concepts

Consolidated notes extracted from the uploaded Markdown files. Repeated topics may appear in more than one source section where the original examples or explanations differ.


---

## Source: JavaScript Basics: Workspace, Data Types and Operators

# JavaScript Notes – Workspace, Data Types & Operators

## 1. Create a JavaScript Workspace in VS Code

### Step 1: Create a Folder

Create a folder for the JavaScript practice.

Example:

```text
javascript-basics
```

### Step 2: Open the Folder in VS Code

1. Open **VS Code**.
2. Select **File → Open Folder**.
3. Select the `javascript-basics` folder.

### Step 3: Create a JavaScript File

Create a file:

```text
day01.js
```

### Step 4: Write JavaScript Code

```javascript
console.log("This is my first JavaScript program");
```

### Step 5: Open the Terminal

In VS Code:

```text
Terminal → New Terminal
```

### Step 6: Execute the JavaScript File

Run:

```bash
node day01.js
```

Output:

```text
This is my first JavaScript program
```

### Execution Flow

```text
Create Workspace
      ↓
Open Workspace in VS Code
      ↓
Create .js File
      ↓
Write JavaScript Code
      ↓
Open Terminal
      ↓
node filename.js
      ↓
View Output
```

---

# 2. `console.log()`

### Definition

`console.log()` is used to print information to the console.

```javascript
console.log("Hello JavaScript");
console.log(10);
```

Output:

```text
Hello JavaScript
10
```

---

# 3. Comments

Comments are used to explain code and are not executed by JavaScript.

### Single-Line Comment

```javascript
// This is a comment
console.log("Hello");
```

### Multi-Line Comment

```javascript
/*
This is a
multi-line comment
*/
```

---

# 4. Data Types

### Definition

A data type defines the kind of value stored in a variable.

JavaScript data types are broadly classified into:

```text
Primitive Data Types
        +
Non-Primitive Data Types
```

---

## 5. Primitive Data Types

Primitive data types represent a single value.

JavaScript has 7 primitive data types:

1. String
2. Number
3. Boolean
4. Undefined
5. Null
6. BigInt
7. Symbol

---

## 6. String

A string represents text.

```javascript
let name = "Playwright";
let course = 'JavaScript';
```

Strings can be written using:

- Single quotes `' '`
- Double quotes `" "`
- Backticks `` ` ` ``

---

## 7. Number

The `number` type represents both integer and floating-point numbers.

```javascript
let age = 25;
let price = 99.50;
```

JavaScript does not have separate `int` and `float` data types.

---

## 8. Boolean

Boolean represents one of two values:

```text
true
false
```

Example:

```javascript
let isLoggedIn = true;
let isAdmin = false;
```

Commonly used in conditions.

---

## 9. Undefined

A variable that has been declared but has not been assigned a value has the value `undefined`.

```javascript
let city;

console.log(city);
```

Output:

```text
undefined
```

---

## 10. Null

`null` represents an intentional absence of a value.

```javascript
let result = null;
```

### Important Point

```javascript
typeof null
```

returns:

```text
object
```

This is a historical behavior in JavaScript.

`null` is still classified as a **primitive data type**, even though `typeof null` returns `"object"`.

---

## 11. BigInt

`BigInt` is used to represent integers larger than the safe integer range of the `number` type.

```javascript
let largeNumber = 123456789012345678901234567890n;
```

The `n` at the end indicates a BigInt literal.

---

## 12. Symbol

`Symbol` creates a unique value.

```javascript
let id = Symbol("id");
```

Each Symbol is unique, even when the descriptions are the same.

```javascript
let a = Symbol("id");
let b = Symbol("id");

console.log(a === b);
```

Output:

```text
false
```

---

# 13. Non-Primitive Data Types

Objects are non-primitive values.

Common examples:

- Object
- Array
- Function

### Object

```javascript
let user = {
    name: "John",
    age: 30
};
```

### Array

```javascript
let browsers = ["Chrome", "Firefox", "Edge"];
```

### Function

```javascript
function greet() {
    console.log("Hello");
}
```

---

# 14. Primitive vs Non-Primitive

| Primitive | Non-Primitive |
|---|---|
| Stores a single value | Can represent collections/structured values |
| Immutable value behavior | Objects can be modified |
| String | Object |
| Number | Array |
| Boolean | Function |
| Undefined | |
| Null | |
| BigInt | |
| Symbol | |

---

# 15. `typeof` Operator

### Definition

`typeof` is used to identify the type of a value.

```javascript
console.log(typeof "Hello");
console.log(typeof 10);
console.log(typeof true);
```

Output:

```text
string
number
boolean
```

### Common Results

```javascript
typeof "Playwright"   // "string"
typeof 100            // "number"
typeof true           // "boolean"
typeof undefined      // "undefined"
typeof 10n            // "bigint"
typeof Symbol("id")   // "symbol"
typeof {}             // "object"
typeof []             // "object"
typeof function() {}  // "function"
typeof null           // "object"
```

### Important Interview Point

```javascript
typeof null
```

returns:

```text
object
```

But `null` is a **primitive data type**.

---

# 16. Operators

### Definition

An operator is a symbol or keyword used to perform an operation on values.

Example:

```javascript
let result = 10 + 5;
```

Here:

- `+` → Operator
- `10`, `5` → Operands

---

# 17. Arithmetic Operators

Used for mathematical calculations.

| Operator | Meaning | Example |
|---|---|---|
| `+` | Addition | `10 + 5` |
| `-` | Subtraction | `10 - 5` |
| `*` | Multiplication | `10 * 5` |
| `/` | Division | `10 / 5` |
| `%` | Remainder | `10 % 3` |
| `**` | Exponentiation | `2 ** 3` |

Example:

```javascript
let a = 10;
let b = 3;

console.log(a + b);
console.log(a - b);
console.log(a * b);
console.log(a / b);
console.log(a % b);
console.log(a ** b);
```

---

# 18. Assignment Operators

Used to assign or update values.

### Basic Assignment

```javascript
let a = 10;
```

### Compound Assignment

```javascript
a += 5;   // a = a + 5
a -= 5;   // a = a - 5
a *= 5;   // a = a * 5
a /= 5;   // a = a / 5
a %= 5;   // a = a % 5
```

---

# 19. Comparison Operators

Used to compare values.

| Operator | Meaning |
|---|---|
| `==` | Loose equality |
| `===` | Strict equality |
| `!=` | Loose inequality |
| `!==` | Strict inequality |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

Example:

```javascript
let a = 10;
let b = 20;

console.log(a < b);
console.log(a > b);
console.log(a === b);
```

---

# 20. `==` vs `===`

### `==` – Loose Equality

Compares values after type coercion.

```javascript
console.log(5 == "5");
```

Output:

```text
true
```

### `===` – Strict Equality

Compares both value and data type.

```javascript
console.log(5 === "5");
```

Output:

```text
false
```

### Recommendation

Prefer `===` when you need strict comparison.

---

# 21. Logical Operators

Used to combine or negate conditions.

| Operator | Meaning |
|---|---|
| `&&` | AND |
| `||` | OR |
| `!` | NOT |

### AND

```javascript
console.log(true && true);
```

Output:

```text
true
```

Both conditions must be true.

### OR

```javascript
console.log(true || false);
```

Output:

```text
true
```

At least one condition must be true.

### NOT

```javascript
console.log(!true);
```

Output:

```text
false
```

---

# 22. Increment and Decrement

### Increment `++`

Increases a value by 1.

```javascript
let count = 5;

count++;

console.log(count);
```

Output:

```text
6
```

### Decrement `--`

Decreases a value by 1.

```javascript
let count = 5;

count--;

console.log(count);
```

Output:

```text
4
```

---

# 23. Pre-Increment vs Post-Increment

### Post-Increment

```javascript
let a = 5;

console.log(a++);
console.log(a);
```

Output:

```text
5
6
```

The current value is used first, then incremented.

### Pre-Increment

```javascript
let a = 5;

console.log(++a);
console.log(a);
```

Output:

```text
6
6
```

The value is incremented first, then used.

---

# 24. Ternary Operator

The ternary operator is a short form of `if...else`.

### Syntax

```javascript
condition ? valueIfTrue : valueIfFalse;
```

Example:

```javascript
let age = 20;

let result = age >= 18 ? "Adult" : "Minor";

console.log(result);
```

Output:

```text
Adult
```

---

# 25. Type Coercion

### Definition

Type coercion is the conversion of a value from one data type to another during an operation or comparison.

Example:

```javascript
console.log(5 + "5");
```

Output:

```text
55
```

Here, the number is converted to a string during the operation.

Another example:

```javascript
console.log(5 == "5");
```

Output:

```text
true
```

---

# 26. Key Interview Points

- JavaScript is dynamically typed.
- A variable can hold values of different types at different times.
- `typeof` is used to identify the type of a value.
- `null` is primitive, although `typeof null` returns `"object"`.
- Arrays return `"object"` with `typeof`.
- Functions return `"function"` with `typeof`.
- `===` performs strict equality comparison.
- `==` allows type coercion.
- `&&`, `||`, and `!` are logical operators.
- `++` increments by 1.
- `--` decrements by 1.
- `%` returns the remainder.
- `**` performs exponentiation.



---

## Source: JavaScript Variables, Scope, Hoisting, Conditions and Loops

# JavaScript Notes – 3–5 Years

## 1. Variables – `var`, `let`, `const`

### `var`
- Function-scoped
- Can be redeclared
- Can be reassigned
- Hoisted and initialized with `undefined`

### `let`
- Block-scoped
- Cannot be redeclared in the same scope
- Can be reassigned
- Hoisted but remains in the **TDZ**

### `const`
- Block-scoped
- Cannot be redeclared
- Cannot be reassigned
- Hoisted but remains in the **TDZ**
- Must be initialized during declaration

### Redeclaration vs Reassignment
- **Redeclaration:** Declaring the same variable again.
- **Reassignment:** Changing the value of an existing variable.

```javascript
var name = "JavaScript";
var name = "Playwright"; // Redeclaration

let age = 20;
age = 30;                // Reassignment
```

---

## 2. Scope

### Scope
Scope defines **where a variable can be accessed** in a JavaScript program.

### Function Scope
- `var` is function-scoped.
- A `var` declared inside a function can be accessed throughout that function.

### Block Scope
- `let` and `const` are block-scoped.
- A block is defined using `{ }`.
- Examples: `if`, `for`, `while`, etc.

```javascript
function test() {

    var a = 10;
    let b = 20;

    if (true) {
        var a = 30;
        let b = 40;

        console.log(a); // 30
        console.log(b); // 40
    }

    console.log(a); // 30
    console.log(b); // 20
}
```

### Key Difference

| Keyword | Scope |
|---|---|
| `var` | Function |
| `let` | Block |
| `const` | Block |

---

## 3. Hoisting

### Definition
**Hoisting** is the JavaScript behavior where declarations are processed during the creation phase before the code is executed.

### Hoisting Behavior

| Declaration | Hoisted | Initial Value |
|---|---|---|
| `var` | Yes | `undefined` |
| `let` | Yes | TDZ |
| `const` | Yes | TDZ |
| Function declaration | Yes | Fully available |

### `var`

```javascript
console.log(num);

var num = 10;
```

Output:

```text
undefined
```

### `let`

```javascript
console.log(num);

let num = 10;
```

Output:

```text
ReferenceError
```

### Function Declaration

```javascript
sayHello();

function sayHello() {
    console.log("Hello");
}
```

Output:

```text
Hello
```

---

## 4. Temporal Dead Zone – TDZ

### Definition
The **Temporal Dead Zone** is the period between entering a scope and the point where a `let` or `const` variable is initialized.

During the TDZ:
- The variable exists in the scope.
- The variable cannot be accessed.
- Accessing it results in a `ReferenceError`.

```javascript
console.log(num); // ReferenceError

let num = 10;
```

### Important Points
- `let` → TDZ
- `const` → TDZ
- `var` → No TDZ
- TDZ ends when the variable is initialized.

### Easy Comparison

```text
var
↓
Hoisted
↓
undefined
↓
Can be accessed
```

```text
let / const
↓
Hoisted
↓
TDZ
↓
Initialization
↓
Can be accessed
```

---

## 5. Operators

### Assignment Operator

```javascript
let age = 20;
```

`=` assigns a value.

### Equality Operators

#### `==`
- Compares values after type coercion.

```javascript
5 == "5"; // true
```

#### `===`
- Compares value and data type.
- Preferred in most cases.

```javascript
5 === "5"; // false
```

### Comparison

```text
=    → Assignment
==   → Loose equality
===  → Strict equality
```

### Type Coercion
Type coercion is the automatic conversion of one data type into another during an operation or comparison.

```javascript
5 == "5";   // true
5 === "5";  // false
```

---

## 6. Conditional Statements

### `if`
Used to execute code when a condition is true.

```javascript
if (condition) {
    // code
}
```

### `if...else`

```javascript
if (condition) {
    // true
} else {
    // false
}
```

### `else if`
Used when multiple conditions need to be checked.

```javascript
if (number > 0) {
    console.log("Positive");
} else if (number < 0) {
    console.log("Negative");
} else {
    console.log("Zero");
}
```

### When to Use
- Use `if...else` for **conditions and ranges**.
- Use `switch` when comparing **one value against multiple fixed options**.

---

## 7. Switch Case

### Definition
`switch` is used to execute different blocks of code based on the value of an expression.

```javascript
switch (value) {

    case "Chrome":
        console.log("Chrome");
        break;

    case "Firefox":
        console.log("Firefox");
        break;

    default:
        console.log("Invalid browser");
}
```

### Keywords
- `switch` → Defines the expression.
- `case` → Defines possible values.
- `break` → Exits the switch.
- `default` → Executes when no case matches.

### Without `break`
Execution continues into the following cases. This is called **fall-through**.

### `switch(true)`
Allows conditions to be evaluated inside cases.

```javascript
switch (true) {

    case number > 0:
        console.log("Positive");
        break;

    case number < 0:
        console.log("Negative");
        break;

    default:
        console.log("Zero");
}
```

---

## 8. `for` Loop

### Definition
A `for` loop repeatedly executes a block of code while a condition is true.

### Syntax

```javascript
for (initialization; condition; update) {
    // code
}
```

### Three Components

```text
Initialization → Starting point
Condition      → Determines whether loop continues
Update         → Changes loop variable
```

### Example

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

### Execution Order

```text
Initialization
      ↓
Condition
      ↓
Loop Body
      ↓
Update
      ↓
Condition
      ↓
Loop Body
      ↓
...
```

### Infinite Loop

An infinite loop occurs when the loop condition never becomes false.

```javascript
for (let i = 1; i <= 5;) {
    console.log(i);
}
```

The update is missing, so `i` never changes.

---

## 9. `break`

### Definition
`break` immediately terminates the loop or switch statement.

```javascript
for (let i = 1; i <= 5; i++) {

    if (i === 3) {
        break;
    }

    console.log(i);
}
```

Output:

```text
1
2
```

### Key Point

```text
break
  ↓
Stops the entire loop
  ↓
Execution continues after the loop
```

---

## 10. `continue`

### Definition
`continue` skips the **current iteration** and moves to the next iteration.

```javascript
for (let i = 1; i <= 5; i++) {

    if (i === 3) {
        continue;
    }

    console.log(i);
}
```

Output:

```text
1
2
4
5
```

### Key Point

```text
continue
    ↓
Skip current iteration
    ↓
Move to next iteration
```

### `break` vs `continue`

| `break` | `continue` |
|---|---|
| Terminates the loop | Skips current iteration |
| Comes out of the loop | Continues with next iteration |
| Remaining iterations don't execute | Remaining iterations continue |

---

## 11. Practical Automation Usage

### Loop Through Test Data

```javascript
for (let i = 0; i < testData.length; i++) {
    // Execute validation
}
```

Useful when the same test operation needs to be performed against multiple test data records.

### Skip Invalid Data

Use `continue`.

```javascript
for (let i = 0; i < testData.length; i++) {

    if (!testData[i].isValid) {
        continue;
    }

    // Process valid data
}
```

### Stop on Critical Failure

Use `break`.

```javascript
for (let i = 0; i < testData.length; i++) {

    if (testData[i].criticalFailure) {
        break;
    }

    // Process test data
}
```

### Browser-Based Decision

For fixed browser values:

```javascript
switch (browser) {

    case "Chrome":
        // Chrome logic
        break;

    case "Firefox":
        // Firefox logic
        break;

    case "Edge":
        // Edge logic
        break;

    default:
        console.log("Unsupported browser");
}
```



---

## Source: JavaScript Concept Definitions, Arrays, Strings and Collections

# JavaScript - Important Concept Definitions

## 1. JavaScript

**Definition:**  
JavaScript is a high-level, dynamically typed programming language used to make web applications interactive and is also widely used for automation, backend development, and other applications.

---

## 2. Data Type

**Definition:**  
A data type defines the kind of value a variable can hold.

```javascript
let name = "Vineeth"; // string
let age = 25;         // number
let isActive = true;  // boolean
```

---

## 3. Primitive Data Types

**Definition:**  
Primitive data types represent single values and are immutable.

JavaScript has 7 primitive data types:

```text
String
Number
BigInt
Boolean
Undefined
Null
Symbol
```

Example:

```javascript
let name = "Vineeth";
let age = 25;
let isActive = true;
```

---

## 4. Non-Primitive Data Types

**Definition:**  
Non-primitive data types can store collections of values or more complex data and are reference-based.

Common examples:

```text
Object
Array
Function
```

Example:

```javascript
let scores = [70, 80, 90];

let employee = {
    name: "Vineeth",
    age: 25
};
```

---

## 5. Variable

**Definition:**  
A variable is a named storage location used to hold a value.

```javascript
let name = "Vineeth";
```

Here:

```text
name → variable
"Vineeth" → value
```

---

## 6. `var`

**Definition:**  
`var` is an older keyword used to declare variables. It is function-scoped and can be redeclared and reassigned.

```javascript
var name = "Vineeth";

var name = "Rajendran";

console.log(name);
```

---

## 7. `let`

**Definition:**  
`let` is used to declare a block-scoped variable that can be reassigned but cannot be redeclared within the same scope.

```javascript
let age = 25;

age = 30;
```

---

## 8. `const`

**Definition:**  
`const` is used to declare a block-scoped variable whose binding cannot be reassigned.

```javascript
const browser = "Chrome";

// browser = "Firefox"; // Error
```

---

## 9. Scope

**Definition:**  
Scope determines where a variable can be accessed in a program.

Common types:

```text
Global Scope
Function Scope
Block Scope
```

---

## 10. Array

**Definition:**  
An array is a non-primitive data type used to store multiple values in a single variable.

```javascript
let scores = [70, 80, 90];
```

---

## 11. Array Index

**Definition:**  
An array index represents the position of an element in an array. Array indexing starts from `0`.

```javascript
let scores = [70, 80, 90];

console.log(scores[0]); // 70
```

---

## 12. Array `length`

**Definition:**  
The `length` property returns the total number of elements in an array.

```javascript
let scores = [70, 80, 90];

console.log(scores.length); // 3
```

```text
Last index = length - 1
```

---

## 13. `push()`

**Definition:**  
`push()` adds one or more elements to the end of an array.

```javascript
scores.push(100);
```

**Important:** Modifies the original array.

---

## 14. `unshift()`

**Definition:**  
`unshift()` adds one or more elements to the beginning of an array.

```javascript
scores.unshift(50);
```

**Important:** Modifies the original array.

---

## 15. `pop()`

**Definition:**  
`pop()` removes the last element from an array.

```javascript
scores.pop();
```

**Important:** Modifies the original array.

---

## 16. `shift()`

**Definition:**  
`shift()` removes the first element from an array.

```javascript
scores.shift();
```

**Important:** Modifies the original array.

---

## 17. `slice()`

**Definition:**  
`slice()` extracts a portion of an array or string without modifying the original value.

```javascript
let result = scores.slice(1, 3);
```

```text
start → included
end   → excluded
```

---

## 18. `splice()`

**Definition:**  
`splice()` is used to add, remove, or replace elements in an array and modifies the original array.

```javascript
scores.splice(1, 2);
```

---

## 19. `sort()`

**Definition:**  
`sort()` sorts the elements of an array and modifies the original array.

For numbers:

```javascript
let marks = [20, 5, 100, 30];

marks.sort((a, b) => a - b);
```

---

## 20. String

**Definition:**  
A string is a sequence of characters used to represent text.

```javascript
let course = "Playwright";
```

---

## 21. String Literal

**Definition:**  
A string literal is a string created directly using quotes.

```javascript
let course = "Playwright";
```

Strings can use:

```javascript
"Playwright"
'Playwright'
`Playwright`
```

---

## 22. String Object

**Definition:**  
A String Object is an object created using the `String` constructor.

```javascript
let course = new String("Playwright");

console.log(typeof course); // object
```

---

## 23. Template Literal

**Definition:**  
A template literal is a string created using backticks (`) that allows variables and expressions to be embedded using `${}`.

```javascript
let name = "Vineeth";

console.log(`Hello ${name}`);
```

---

## 24. String `length`

**Definition:**  
The `length` property returns the number of characters in a string.

```javascript
let course = "Playwright";

console.log(course.length);
```

---

## 25. `charAt()`

**Definition:**  
`charAt()` returns the character at a specified index.

```javascript
let course = "Playwright";

console.log(course.charAt(1));
```

---

## 26. `indexOf()`

**Definition:**  
`indexOf()` returns the index of the first occurrence of a specified character or substring.

```javascript
let course = "Playwright";

console.log(course.indexOf("w"));
```

If the value is not found:

```text
-1
```

---

## 27. `substring()`

**Definition:**  
`substring()` extracts characters between two specified indexes.

```javascript
let username = "rajeshkumar@hotmail.com";

let name = username.substring(0, 6);
```

```text
start → included
end   → excluded
```

---

## 28. `split()`

**Definition:**  
`split()` divides a string into an array of substrings based on a specified separator.

```javascript
let batchName = "Playwright August 2026";

let result = batchName.split(" ");

console.log(result);
```

Output:

```text
["Playwright", "August", "2026"]
```

---

## 29. Function

**Definition:**  
A function is a reusable block of code designed to perform a specific task.

```javascript
function add() {
    let a = 10;
    let b = 20;

    console.log(a + b);
}
```

---

## 30. Parameter

**Definition:**  
A parameter is a variable defined in a function declaration to receive input.

```javascript
function login(username, password) {

}
```

Here:

```text
username → parameter
password → parameter
```

---

## 31. Argument

**Definition:**  
An argument is the actual value passed to a function when the function is called.

```javascript
login("Demo1", "Pass1");
```

Here:

```text
"Demo1" → argument
"Pass1" → argument
```

---

## 32. `return`

**Definition:**  
`return` sends a value from a function back to the place where the function was called.

```javascript
function add() {

    let a = 10;
    let b = 20;

    return a + b;
}

let result = add();

console.log(result);
```

---

## 33. `console.log()`

**Definition:**  
`console.log()` displays a value in the console. It does not return the value from the function.

```javascript
function add() {

    let a = 10;
    let b = 20;

    console.log(a + b);
}
```

---

## 34. Local Variable

**Definition:**  
A local variable is a variable declared inside a function or block and can generally be accessed only within that scope.

```javascript
function add() {

    let a = 10;

    console.log(a);
}
```

---

## 35. Loop

**Definition:**  
A loop is a programming construct used to execute a block of code repeatedly based on a condition.

Common JavaScript loops:

```text
for
while
do...while
for...of
forEach()
```

---

## 36. `for` Loop

**Definition:**  
A `for` loop is used to execute a block of code repeatedly while a specified condition is true.

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

---

## 37. `for...of`

**Definition:**  
`for...of` is used to iterate directly over the values of an iterable, such as an array or string.

```javascript
let scores = [70, 80, 90];

for (let score of scores) {
    console.log(score);
}
```

---

## 38. `forEach()`

**Definition:**  
`forEach()` executes a callback function once for each element in an array.

```javascript
let scores = [70, 80, 90];

scores.forEach((score) => {
    console.log(score);
});
```

---

## 39. Type Coercion

**Definition:**  
Type coercion is the automatic conversion of one data type into another by JavaScript during an operation.

```javascript
let a = "20";
let b = "10";

console.log(a + b); // "2010"
console.log(a - b); // 10
```

---

## 40. `==`

**Definition:**  
`==` is the loose equality operator. It compares values after performing type coercion when necessary.

```javascript
console.log("20" == 20); // true
```

---

## 41. `===`

**Definition:**  
`===` is the strict equality operator. It compares both the value and the data type without performing type coercion.

```javascript
console.log("20" === 20); // false
```

---

## 42. Object

**Definition:**  
An object is a non-primitive data type used to store data as key-value pairs.

```javascript
let employee = {
    name: "Vineeth",
    role: "SDET",
    experience: 5
};
```

---

## 43. Set

**Definition:**  
A `Set` is a collection that stores unique values and does not allow duplicates.

```javascript
let numbers = new Set([10, 20, 20, 30]);

console.log(numbers);
```

---

## 44. Map

**Definition:**  
A `Map` is a collection of key-value pairs where each key is unique.

```javascript
let employee = new Map();

employee.set("name", "Vineeth");
employee.set("role", "SDET");
```

---

## 45. Palindrome

**Definition:**  
A palindrome is a value that remains the same when it is reversed.

Examples:

```text
121   → Palindrome
MADAM → Palindrome
1331  → Palindrome

123   → Not a Palindrome
```

---

## 46. Nested Loop

**Definition:**  
A nested loop is a loop placed inside another loop.

```javascript
for (let i = 0; i < arr1.length; i++) {

    for (let j = 0; j < arr2.length; j++) {

        // Logic

    }
}
```

It is commonly used when comparing elements between two arrays.

---

## 47. Callback Function

**Definition:**  
A callback function is a function passed as an argument to another function and executed by that function.

```javascript
scores.forEach((score) => {
    console.log(score);
});
```

Here:

```text
(score) => { ... }
```

is the callback function.

---

## 48. Dynamic Test Data

**Definition:**  
Dynamic test data means providing different input values to the same function or test instead of hardcoding the values inside the function.

```javascript
function login(username, password) {

    console.log(username);
    console.log(password);
}

login("Demo1", "Pass1");
login("Demo2", "Pass2");
login("Demo3", "Pass3");
```

This is particularly useful in test automation, where the same test logic may need to run with multiple sets of data.



---

## Source: JavaScript Functions, Callbacks, Promises and Async/Await

# JavaScript Functions, Callbacks, Promises, and Async/Await

## 1. Function Expression

### Definition

A **Function Expression** is a function that is assigned to a variable.

```javascript
let loginDetails = function login() {
    console.log("Login executed successfully");
};

loginDetails();
```

### Key Points

- Uses the `function` keyword.
- The function is assigned to a variable.
- The function can be called using the variable name.
- `login` is the function name.
- `loginDetails` is the variable that stores the function.

### Anonymous Function Expression

The function name is optional when a function is assigned to a variable.

```javascript
let loginDetails = function () {
    console.log("Login executed successfully");
};

loginDetails();
```

---

## 2. Arrow Function

### Definition

An **Arrow Function** is a shorter and modern syntax for writing functions.

```javascript
let loginDetails = () => {
    console.log("Login executed successfully");
};

loginDetails();
```

### Key Points

- Uses the `=>` syntax.
- Does not use the `function` keyword.
- Provides concise syntax.
- Commonly used with callbacks and Promises.
- Arrow functions do not have their own `this`.

### Single-Line Arrow Function

When there is only one statement, the braces can be omitted.

```javascript
let loginDetails = () => console.log("Login executed successfully");

loginDetails();
```

---

## 3. Function Expression vs Arrow Function

| Function Expression | Arrow Function |
|---|---|
| Uses `function` keyword | Uses `=>` syntax |
| Traditional syntax | Modern concise syntax |
| Can have its own `this` | Does not have its own `this` |
| Suitable for regular functions | Commonly used for callbacks |
| Can be named or anonymous | Usually anonymous when assigned to a variable |

### Important

Arrow functions are not simply a replacement for every function expression. The behavior of `this`, `arguments`, `prototype`, and constructors is different.

---

# 4. Synchronous Execution

### Definition

**Synchronous execution** means JavaScript executes statements one after another in sequence.

```javascript
console.log("Enter Username");
console.log("Enter Password");
console.log("Click Login Button");
```

### Output

```text
Enter Username
Enter Password
Click Login Button
```

The next statement executes after the current statement is completed.

---

# 5. Asynchronous Execution

### Definition

**Asynchronous execution** allows JavaScript to start an operation and continue executing other code without waiting for that operation to finish.

Example:

```javascript
console.log("Code for Enter Username");

setTimeout(() => {
    console.log("Code for Enter Password");
}, 5000);

console.log("Code for Click Login Button");
```

### Output

```text
Code for Enter Username
Code for Click Login Button
Code for Enter Password
```

The password code executes after 5 seconds.

### Important Correction

JavaScript does **not** execute all code asynchronously by default.

- Normal JavaScript statements execute synchronously.
- Operations such as `setTimeout()`, Promises, and many browser/Node.js APIs can work asynchronously.
- JavaScript uses the **event loop** to coordinate asynchronous operations.

---

# 6. setTimeout()

### Definition

`setTimeout()` schedules a function to execute after a specified delay.

```javascript
setTimeout(() => {
    console.log("Executed after 5 seconds");
}, 5000);
```

### Syntax

```javascript
setTimeout(callback, delay);
```

- `callback` → function to execute later.
- `delay` → time in milliseconds.
- `5000` milliseconds = 5 seconds.

### Important

`setTimeout()` does not pause the JavaScript program for the specified time. It schedules the callback to run later.

---

# 7. Callback Function

### Definition

A **callback function** is a function passed as an argument to another function and invoked by that function.

Example:

```javascript
function createAccount() {
    console.log("Account created");
}

function login(callback) {
    console.log("Login successful");
    callback();
}

login(createAccount);
```

### Output

```text
Login successful
Account created
```

Here:

- `createAccount` is passed as an argument.
- `callback` receives the function.
- `callback()` executes `createAccount()`.

---

# 8. Multiple Callback Functions

A function can accept more than one callback.

```javascript
function login(call1, call2) {

    console.log("Login successful");

    call1(); // createAccount()
    call2(); // createLead()
}

function createAccount() {
    console.log("Account created");
}

function createLead() {
    console.log("Lead created");
}

login(createAccount, createLead);
```

### Output

```text
Login successful
Account created
Lead created
```

### Execution Flow

```text
login()
   ↓
Login successful
   ↓
createAccount()
   ↓
Account created
   ↓
createLead()
   ↓
Lead created
```

### Important

When passing a function as a callback:

```javascript
login(createAccount);
```

Do **not** write:

```javascript
login(createAccount());
```

`createAccount()` executes the function immediately, whereas `createAccount` passes the function itself.

---

# 9. Promise

### Definition

A **Promise** is an object that represents the eventual completion or failure of an asynchronous operation.

A Promise can have three states:

1. **Pending** – operation is still in progress.
2. **Fulfilled** – operation completed successfully.
3. **Rejected** – operation failed.

---

## 10. Creating a Promise

```javascript
let enterPassword = new Promise((resolve, reject) => {

    setTimeout(() => {

        console.log("Code for Enter Password");

        resolve();

    }, 5000);

});
```

### Explanation

```javascript
new Promise((resolve, reject) => {
```

Creates a new Promise.

```javascript
resolve();
```

Indicates that the asynchronous operation completed successfully.

```javascript
reject();
```

Indicates that the asynchronous operation failed.

---

# 11. Handling a Promise with then()

The `.then()` method executes when the Promise is fulfilled.

```javascript
console.log("Code for Enter Username");

let enterPassword = new Promise((resolve) => {

    setTimeout(() => {

        console.log("Code for Enter Password");

        resolve();

    }, 5000);

});

enterPassword.then(() => {

    console.log("Code for Click Login Button");

});
```

### Output

```text
Code for Enter Username
Code for Enter Password
Code for Click Login Button
```

The login button code executes only after `resolve()` is called.

---

# 12. Promise with Resolve and Reject

```javascript
let login = new Promise((resolve, reject) => {

    let isLoginSuccessful = true;

    if (isLoginSuccessful) {
        resolve("Login successful");
    } else {
        reject("Login failed");
    }

});

login
    .then((message) => {
        console.log(message);
    })
    .catch((error) => {
        console.log(error);
    });
```

### Promise Methods

| Method | Purpose |
|---|---|
| `.then()` | Handles successful completion |
| `.catch()` | Handles failure |
| `.finally()` | Executes regardless of success or failure |

---

# 13. async Keyword

### Definition

The `async` keyword is used to declare an asynchronous function.

An `async` function always returns a Promise.

```javascript
async function login() {
    console.log("Login successful");
}

login();
```

Even though no Promise is explicitly created, `login()` returns a Promise.

---

# 14. await Keyword

### Definition

`await` is used to wait for a Promise to settle before continuing with the next statement inside the asynchronous function.

```javascript
function enterPassword() {

    return new Promise((resolve) => {

        setTimeout(() => {

            console.log("Password entered");

            resolve();

        }, 5000);

    });

}

async function login() {

    console.log("Username entered");

    await enterPassword();

    console.log("Login button clicked");

}

login();
```

### Execution Flow

```text
Username entered
       ↓
enterPassword()
       ↓
Wait for Promise
       ↓
Password entered
       ↓
Promise resolved
       ↓
Login button clicked
```

### Important Rule

`await` is normally used inside an `async` function.

```javascript
async function example() {
    await somePromise();
}
```

Modern JavaScript also supports top-level `await` in appropriate module environments.

---

# 15. Promise vs async/await

Both approaches can handle asynchronous operations.

### Using then()

```javascript
enterPassword.then(() => {
    console.log("Login button clicked");
});
```

### Using async/await

```javascript
async function login() {

    await enterPassword;

    console.log("Login button clicked");
}
```

### Comparison

| Promise `.then()` | `async/await` |
|---|---|
| Uses `.then()` and `.catch()` | Uses `await` and `try/catch` |
| Can become difficult to read with many chained operations | Usually easier to read |
| Promise-based | Built on top of Promises |
| Useful for chaining | Useful for sequential asynchronous flow |

---

# 16. Error Handling with async/await

Use `try...catch` to handle rejected Promises.

```javascript
function login() {

    return new Promise((resolve, reject) => {

        let isSuccessful = false;

        if (isSuccessful) {
            resolve("Login successful");
        } else {
            reject("Login failed");
        }

    });

}

async function executeLogin() {

    try {

        let message = await login();

        console.log(message);

    } catch (error) {

        console.log(error);

    }

}

executeLogin();
```

---

# 17. Sequential Execution in Automation

In automation, actions often need to happen in a specific order.

Example:

```text
Enter Username
      ↓
Enter Password
      ↓
Click Login
      ↓
Verify Home Page
```

With Playwright, many actions return Promises. Therefore, `await` is commonly used.

```javascript
await page.getByLabel("Username").fill("admin");
await page.getByLabel("Password").fill("admin123");
await page.getByRole("button", { name: "Login" }).click();
```

Each `await` waits for the corresponding asynchronous operation to complete before moving to the next statement.

---

# 18. Important Correction for Playwright

Do not say:

> "JavaScript is asynchronous by default."

A better explanation is:

> **JavaScript executes normal code synchronously, while asynchronous operations are handled through mechanisms such as Promises and the event loop. In Playwright, many browser actions return Promises, so we commonly use `await` to perform actions sequentially.**

---

# 19. Callback vs Promise vs async/await

| Concept | Purpose |
|---|---|
| Callback | Pass a function to be executed later |
| Promise | Represents the eventual result of an asynchronous operation |
| `.then()` | Handles a fulfilled Promise |
| `.catch()` | Handles a rejected Promise |
| `async` | Declares an asynchronous function |
| `await` | Waits for a Promise inside an async function |

### Simple Evolution

```text
Callback
   ↓
Promise
   ↓
async / await
```

This is a useful way to understand how asynchronous code can become easier to manage.

---

# 20. Complete Example

```javascript
// Function Expression
let loginDetails1 = function login() {
    console.log("Login executed successfully");
};

loginDetails1();


// Arrow Function
let loginDetails2 = () => {
    console.log("Login executed successfully");
};

loginDetails2();


// Callback Function
function createAccount() {
    console.log("Account created");
}

function createLead() {
    console.log("Lead created");
}

function login(call1, call2) {

    console.log("Login successful");

    call1();
    call2();
}

login(createAccount, createLead);


// Promise
function enterPassword() {

    return new Promise((resolve) => {

        setTimeout(() => {

            console.log("Password entered");

            resolve();

        }, 2000);

    });

}


// async/await
async function executeLogin() {

    console.log("Username entered");

    await enterPassword();

    console.log("Login button clicked");

}

executeLogin();
```

---

# Quick Interview Notes

### What is a Function Expression?

A function assigned to a variable is called a Function Expression.

### What is an Arrow Function?

An Arrow Function is a concise syntax for defining functions using `=>`.

### What is a Callback?

A function passed as an argument to another function is called a callback function.

### What is a Promise?

A Promise represents the eventual success or failure of an asynchronous operation.

### What are the states of a Promise?

- Pending
- Fulfilled
- Rejected

### What is `async`?

`async` declares a function that returns a Promise.

### What is `await`?

`await` pauses the execution of the async function until the Promise settles.

### Does `await` make JavaScript synchronous?

No. It only makes the asynchronous code inside the async function easier to write and read in a sequential style.

### Why is `await` commonly used in Playwright?

Because many Playwright APIs return Promises, and `await` allows the test to wait for those operations to complete before continuing.



---

## Source: TypeScript Types and Language Features

# TypeScript Notes

## 1. Type Inference

### Theory

Type inference is a feature of TypeScript where the compiler
automatically determines the type of a variable from the value assigned
to it.

There are two common ways to specify types:

-   **Implicit type inference:** TypeScript automatically identifies the
    type.
-   **Explicit type annotation:** The developer explicitly specifies the
    type.

### Implicit Type Inference

``` typescript
// TypeScript automatically infers the type as string.
let a = "Vineeth";

// Error because 'a' is inferred as string.
// a = 10;
```

### Explicit Type Annotation

``` typescript
// Explicitly specify the variable type as string.
let b: string = "Vinoth";
```

### JavaScript vs TypeScript

-   JavaScript is dynamically typed.
-   TypeScript is statically typed.
-   TypeScript checks types during development/compilation.
-   TypeScript helps identify many type-related errors before runtime.

------------------------------------------------------------------------

## 2. let, var and const

### Theory

`var`, `let`, and `const` are keywords used to declare variables.

-   `var` is function-scoped and can be redeclared and reassigned.
-   `let` is block-scoped and can be reassigned but cannot be redeclared
    in the same scope.
-   `const` is block-scoped and cannot be reassigned after
    initialization.

### let Example

``` typescript
// Declare a variable using let.
let a = "Vineeth";

// Reassigning a compatible value is allowed.
a = "Karthik";
```

In TypeScript, the inferred type is checked strictly.

``` typescript
// 'a' is inferred as string.
let a = "Vineeth";

// Error because a is a string.
// a = 20;
```

To allow both types:

``` typescript
// The variable can contain either a string or a number.
let a: string | number = "Vineeth";

// Reassign a number.
a = 20;
```

### var and const

``` typescript
// var can be reassigned.
var city = "Chennai";

// Reassign the variable.
city = "Bengaluru";

// const cannot be reassigned after initialization.
const country = "India";

// Error: Assignment to a constant variable.
// country = "USA";
```

------------------------------------------------------------------------

## 3. any and unknown

### Theory

Both `any` and `unknown` can represent values when the exact type is not
known.

### any

`any` disables most TypeScript type checking for that value. It provides
flexibility but reduces type safety.

``` typescript
// any allows any type of data.
let c: any = 7;

// TypeScript does not provide strict validation for the operation.
console.log(c.toUpperCase());
```

### unknown

`unknown` is safer than `any`. A value of type `unknown` cannot be
directly used as a specific type until TypeScript verifies its type.

``` typescript
// unknown can store a value whose type is not known.
let d: unknown = "Testleaf";

// Check the type before using the value.
if (typeof d === "string") {

    // TypeScript now knows that d is a string.
    console.log(d.toUpperCase());
}
```

### Practical Use

`unknown` is useful when handling external data such as API responses,
parsed input, or configuration values where the type is not guaranteed.

------------------------------------------------------------------------

## 4. Arrays and Tuples

### Theory

An array is a collection of values stored under one variable.

### Homogeneous Array

A homogeneous array contains values of the same type.

``` typescript
// All elements are numbers.
let numbers: number[] = [10, 20, 30];
```

### Heterogeneous Array

A heterogeneous array contains values of different types.

``` typescript
// The array contains numbers and a string.
let values = [10, 20, 30, "Vineeth"];
```

### Tuple

A tuple is a special TypeScript type that defines the number, type, and
order of elements.

``` typescript
// First value must be a number.
// Second and third values must be strings.
let data: [number, string, string] = [123, "Harrish", "https"];
```

### Array vs Tuple

-   Array: normally used for a collection of values.
-   Tuple: used when the position and type of each value are important.

------------------------------------------------------------------------

## 5. Classes and Objects

### Theory

A **class** is a blueprint or design used to create objects.

An **object** is an instance of a class. Multiple objects can be created
from one class.

The `new` keyword is used to create an object from a class.

### Example

``` typescript
// Create a class named Employee.
class Employee {

    // Employee name must be a string.
    empName: string;

    // Employee ID must be a number.
    empID: number;
}

// Create the first Employee object.
let emp1 = new Employee();

// Assign values to the first object.
emp1.empName = "Rahul";
emp1.empID = 1234;

// Create the second Employee object.
let emp2 = new Employee();

// Assign values to the second object.
emp2.empName = "Maha";
emp2.empID = 12345;

// Create the third Employee object.
let emp3 = new Employee();

// Assign values to the third object.
emp3.empName = "Maha";
emp3.empID = 12345;
```

### Key Terms

-   Class → Blueprint/design.
-   Object → Instance of a class.
-   Property → Data belonging to an object.
-   `new` → Creates an object from a class.

------------------------------------------------------------------------

## 6. Enum

### Theory

An enum is used to define a set of named constants.

Enums are useful when a variable should contain one value from a
predefined set of related values.

Common enum forms: - Numeric enum - String enum - Heterogeneous enum

### String Enum

``` typescript
// Each enum member contains a string value.
enum Environment {
    QA = "https://qa.com",
    PROD = "https://prod.com",
    UAT = "https://uat.com"
}
```

### Numeric Enum

``` typescript
// Enum members contain numeric values.
enum Status {
    NEW = 1,
    IN_PROGRESS = 2,
    COMPLETED = 3
}
```

### Heterogeneous Enum

A heterogeneous enum contains both string and numeric members.

``` typescript
// Create an enum for application environments.
enum Environments {

    // QA has a string value.
    QA = "https://qa.com",

    // PROD has a numeric value.
    PROD = 2,

    // UAT has a numeric value.
    UAT = 3
}

// Access the QA value using dot notation.
console.log(Environments.QA);
```

------------------------------------------------------------------------

## 7. Object Type

### Theory

TypeScript allows us to define the expected structure of an object.

We can specify: - Property names. - Property types. - Optional
properties.

The `?` symbol makes a property optional.

### Example

``` typescript
// Define the structure of the employee object.
let empDetails: {

    // Employee name must be a string.
    empName: string,

    // Employee ID must be a number.
    empID: number,

    // Employee department must be a string.
    empDepartment: string,

    // Employee availability is optional.
    empAvailability?: boolean

} = {

    // Assign the employee name.
    empName: "Rajesh@gmail.com",

    // Assign the employee ID.
    empID: 123,

    // Assign the employee department.
    empDepartment: "QA"
};

// Access the employee ID using dot notation.
console.log(empDetails.empID);

// Print the complete object.
console.log(empDetails);

// Update an existing property.
empDetails.empName = "karthik@gmail.com";

// Add the optional property.
empDetails.empAvailability = true;

// Delete the optional property.
delete empDetails.empAvailability;
```

### Object Operations

-   Updating → `empDetails.empName = "karthik@gmail.com";`
-   Adding → `empDetails.empAvailability = true;`
-   Deleting → `delete empDetails.empAvailability;`

------------------------------------------------------------------------

## 8. Union Type

### Theory

A union type allows a variable to contain one of multiple specified
types.

The union operator is `|`.

It means **OR**.

For example, `string | number` means the value can be either a string or
a number.

### Example

``` typescript
// A variable can contain either a string or a number.
let usernameField: string | number = "vineeth@gmail.com";

// A number is also allowed.
usernameField = 8925411170;
```

### Type Alias

A type alias gives a reusable name to a type definition.

``` typescript
// Create a reusable type containing string OR number.
type UsernameField = number | string;

// Use the type alias for an email ID.
let emailID: UsernameField = "vineeth@gmail.com";

// Use the same type alias for a number.
let mobile1: UsernameField = 892544411;

// A string is also valid for the same type alias.
let mobile2: UsernameField = "karthik@gmail.com";
```

### Key Point

`string | number` → string **OR** number.

------------------------------------------------------------------------

## 9. Intersection Type

### Theory

An intersection type combines multiple types into one type.

The intersection operator is `&`.

It means **AND**.

If two types are combined using `&`, the resulting type must satisfy the
requirements of both types.

### Example

``` typescript
// Define the username structure.
type Username = {

    // Username must be a string.
    username: string;
};

// Define the password structure.
type Password = {

    // Password must be a number.
    password: number;
};

// Combine Username and Password using intersection.
type Login = Username & Password;

// The object must contain both username and password.
let loginDetails: Login = {

    // Provide the username property.
    username: "vineeth@gmail.com",

    // Provide the password property.
    password: 1234
};
```

### Union vs Intersection

``` text
Union        |  OR  | One of the specified types
Intersection &  AND | Combined requirements of all types
```

------------------------------------------------------------------------

## 10. JavaScript and TypeScript

### Theory

TypeScript is a superset of JavaScript.

This means valid JavaScript code can generally be used in a TypeScript
file, while TypeScript adds features such as:

-   Static typing
-   Type annotations
-   Type aliases
-   Enums
-   Interfaces
-   Access modifiers
-   Compile-time type checking

TypeScript code is compiled/transpiled into JavaScript, which can then
run in JavaScript environments.

### Key Statement

**TypeScript is a superset of JavaScript.**



---

## Source: TypeScript Object-Oriented Programming

# TypeScript OOP -- Complete Notes

## 1. Object-Oriented Programming in TypeScript

Object-Oriented Programming (OOP) is a programming approach where
software is organized around **objects** that contain data and behavior.

TypeScript supports the major OOP concepts:

-   Classes and Objects
-   Encapsulation
-   Inheritance
-   Polymorphism
-   Abstraction
-   Interfaces

These concepts are especially useful in automation frameworks because
test code can be organized into reusable Page Objects, Base Classes,
utilities, and common actions.

------------------------------------------------------------------------

# 2. Class

## Theory

A **class** is a blueprint or template used to create objects.

A class can contain:

-   Properties -- represent data/state.
-   Methods -- represent actions/behavior.
-   Constructors -- initialize objects.
-   Access modifiers -- control visibility.
-   Getters and setters -- control access to data.

### Automation Example

A `LoginPage` class can contain:

-   Username locator
-   Password locator
-   Login button locator
-   `enterUsername()`
-   `enterPassword()`
-   `clickLoginButton()`

The class represents the behavior of a Login page.

------------------------------------------------------------------------

# 3. Object

## Theory

An **object** is an instance of a class.

The `new` keyword is normally used to create an object.

### Example

``` typescript
class LoginPage {
    clickLogin() {
        console.log("Login clicked");
    }
}

let loginPage = new LoginPage();
loginPage.clickLogin();
```

### Important Terms

  Term       Meaning
  ---------- ------------------------------
  Class      Blueprint
  Object     Instance of a class
  Property   Data/state
  Method     Action/behavior
  `new`      Creates an object
  `this`     Refers to the current object

------------------------------------------------------------------------

# 4. Function vs Method

## Theory

A **function** is a standalone reusable block of code.

A **method** is a function that belongs to a class or object.

### Function

A function can be called independently.

### Method

A method is normally accessed through a class object.

### Automation Context

A standalone utility function might perform a general calculation, while
a Page Object method might perform an action such as:

`loginPage.clickLoginButton()`

### Quick Comparison

  Function                 Method
  ------------------------ ----------------------------------
  Standalone               Belongs to a class/object
  Called independently     Usually called through an object
  General reusable logic   Object-specific behavior

------------------------------------------------------------------------

# 5. `this` Keyword

## Theory

`this` refers to the **current object**.

It is commonly used when a method needs to access a property belonging
to the same object.

For example, if a class has a property called `username` and a method
has a local parameter also called `username`, `this.username` clearly
refers to the class property.

### Why it is useful

It helps distinguish:

-   Local variables/parameters
-   Class properties

### Automation Example

A Page Object may store a locator as a property and use `this.locator`
inside its methods.

------------------------------------------------------------------------

# 6. Inheritance

## Theory

**Inheritance** allows one class to reuse members of another class.

-   Parent class -- provides common functionality.
-   Child class -- inherits and can add its own functionality.

TypeScript uses the `extends` keyword for class inheritance.

### Automation Example

A `LoginPage` can contain common login actions. A `CreateLead` page can
extend it and add lead-specific actions.

``` text
LoginPage
    ↓
CreateLead
```

### Benefits

-   Code reuse
-   Less duplication
-   Centralized common functionality
-   Easier maintenance
-   Supports framework-level base classes

### Inheritance Across Files

When classes are in different files:

1.  Export the parent class.
2.  Import it in the child file.
3.  Use `extends`.

------------------------------------------------------------------------

# 7. Multilevel Inheritance

## Theory

**Multilevel inheritance** occurs when inheritance continues through
multiple levels.

``` text
LoginPage
    ↓
CreateLead
    ↓
DeleteLead
```

`DeleteLead` inherits from `CreateLead`, and `CreateLead` inherits from
`LoginPage`.

Therefore, the `DeleteLead` object can access members inherited through
the chain.

### Automation Use Case

A framework may have:

``` text
BasePage
    ↓
LeadPage
    ↓
CreateLeadPage
```

Common browser/page actions can be kept in `BasePage`, while specialized
functionality is added at lower levels.

### Caution

Very deep inheritance hierarchies can make code harder to understand.
Composition and smaller reusable utilities can sometimes be preferable.

------------------------------------------------------------------------

# 8. Method Overloading

## Theory

**Method overloading** means allowing the same method name to support
different parameter combinations.

TypeScript implements overloads using:

1.  Multiple overload signatures.
2.  One implementation.

### Example

``` typescript
class Calculator {
    add(a: number, b: number): number;
    add(a: number, b: number, c: number): number;

    add(a: number, b: number, c?: number): number {
        return c !== undefined ? a + b + c : a + b;
    }
}
```

### Important Points

-   Method name remains the same.
-   Parameters/signatures differ.
-   TypeScript uses overload signatures for type checking.
-   There is only one runtime implementation.
-   Optional parameters are commonly used in the implementation.

### Automation Use Case

A utility may support different input combinations, such as an action
that accepts a locator alone or a locator plus an action description.

### Common Interview Trap

Do not say that TypeScript creates multiple runtime methods with the
same name. It does not. There is one implementation.

------------------------------------------------------------------------

# 9. Method Overriding

## Theory

**Method overriding** occurs when a child class provides a new
implementation for a method already defined in the parent class.

Inheritance is required.

### Example

``` typescript
class LaunchBrowser {
    launch() {
        console.log("Launching browser");
    }
}

class LaunchChrome extends LaunchBrowser {
    launch() {
        console.log("Launching Chrome");
    }
}
```

### Why Override?

A parent can define common behavior while child classes customize
behavior.

### Automation Example

A generic browser class can define `launch()`, while browser-specific
classes can provide Chrome, Edge, or Firefox behavior.

------------------------------------------------------------------------

# 10. `super` Keyword

## Theory

`super` is used inside a child class to access the parent class.

It can be used to:

-   Call a parent method.
-   Call a parent constructor.

### Example

``` typescript
class LaunchChrome extends LaunchBrowser {
    launch() {
        super.launch();
        console.log("Launching Chrome");
    }
}
```

### Execution Flow

``` text
Child launch()
      ↓
super.launch()
      ↓
Parent launch()
      ↓
Child-specific code
```

### Important Point

The parent method does not automatically execute when a child overrides
it. Use `super.methodName()` when the parent implementation is also
required.

------------------------------------------------------------------------

# 11. Interface

## Theory

An **interface** defines a contract.

It describes what a class should provide without supplying the normal
implementation of those class methods.

A class uses `implements` to follow an interface.

### Example

``` typescript
interface BrowserAction {
    clickAction(): void;
    fillValue(): string;
}
```

A class implementing this interface must provide the required members.

### Key Characteristics

-   Defines a contract.
-   Supports structural typing.
-   A class can implement an interface.
-   An interface cannot be instantiated directly.
-   Useful when unrelated classes need to follow the same contract.

### Automation Example

Different page/action classes may be required to support common actions
such as click and fill.

------------------------------------------------------------------------

# 12. `implements` Keyword

## Theory

`implements` tells TypeScript that a class must satisfy an interface.

Conceptually:

``` text
Interface
    ↓
Contract
    ↓
Class implements Interface
    ↓
Class provides implementation
```

### Important Point

`implements` does not mean that the class inherits implementation from
the interface. The class must provide the required implementation
itself.

------------------------------------------------------------------------

# 13. Abstract Class

## Theory

An **abstract class** is a base class that cannot be instantiated
directly.

It can contain both:

-   Abstract methods -- no implementation.
-   Concrete methods -- have implementation.

It can also contain properties and constructors.

### Example

``` typescript
abstract class Browser {
    abstract launch(): void;

    closeBrowser(): void {
        console.log("Browser closed");
    }
}
```

### Important Point

The abstract class defines some common behavior and leaves some behavior
for child classes to implement.

------------------------------------------------------------------------

# 14. Abstract Method

## Theory

An **abstract method** is declared without a method body and uses the
`abstract` keyword.

Example:

``` typescript
abstract launch(): void;
```

A concrete child class must provide the implementation.

### Why Use Abstract Methods?

They force child classes to provide behavior that is different for each
implementation.

### Automation Example

A base browser class may require every browser implementation to define
its own `launch()` method.

------------------------------------------------------------------------

# 15. Concrete Method

## Theory

A **concrete method** has an implementation.

An abstract class can contain concrete methods for behavior that is
common to all child classes.

### Example

``` typescript
closeBrowser(): void {
    console.log("Browser closed");
}
```

All child classes can reuse this implementation unless they choose to
override it.

------------------------------------------------------------------------

# 16. Implementing an Abstract Class

A child class uses `extends` and must implement all inherited abstract
methods before it can be instantiated.

Example:

``` typescript
class ChromeBrowser extends Browser {
    launch(): void {
        console.log("Launching Chrome");
    }
}
```

### Rule

If a concrete child class does not implement required abstract methods,
TypeScript reports a compile-time error.

------------------------------------------------------------------------

# 17. Interface vs Abstract Class

  -----------------------------------------------------------------------
  Interface                           Abstract Class
  ----------------------------------- -----------------------------------
  Defines a contract                  Defines a contract plus common
                                      implementation

  Class uses `implements`             Child uses `extends`

  Cannot be instantiated              Cannot be instantiated directly

  Mainly describes required structure Can contain abstract and concrete
                                      members

  Does not provide normal class       Can have properties and
  state/constructor behavior          constructors

  Useful for common                   Useful for related classes sharing
  capabilities/contracts              behavior
  -----------------------------------------------------------------------

### Beginner-Friendly Rule

**Interface → What should be provided**

**Abstract class → What should be provided + some common
implementation**

This is a simplified learning rule; TypeScript's type system provides
additional interface capabilities.

------------------------------------------------------------------------

# 18. Constructors

## Theory

A **constructor** is a special method used to initialize an object when
it is created.

It runs automatically when `new` is used.

### Important OOP Point

An abstract class can have a constructor.

An interface does not have a class constructor because an interface is
not a class and cannot be instantiated.

### Automation Use Case

A base Page Object constructor commonly receives a Playwright `Page`
object and stores it for use by page methods.

------------------------------------------------------------------------

# 19. Polymorphism

## Theory

**Polymorphism** means one common interface or parent type can represent
different implementations.

Two relevant forms in these topics are:

### Compile-Time / Type-Level Polymorphism

Method overloading allows one method name to represent different
accepted signatures.

### Runtime Polymorphism

Method overriding allows a child implementation to provide different
behavior for the same parent method.

### Simple View

``` text
Overloading  → Same name, different signatures
Overriding   → Same method, different implementation
```

------------------------------------------------------------------------

# 20. Encapsulation

## Theory

**Encapsulation** means keeping data and behavior together and
controlling how internal data is accessed.

TypeScript supports encapsulation using access modifiers such as:

-   `public`
-   `private`
-   `protected`
-   `readonly`

### Automation Example

A locator or internal implementation detail can be kept private while
exposing a public method such as `login()`.

### Benefit

The test should interact with the Page Object through meaningful methods
instead of directly manipulating every internal detail.

------------------------------------------------------------------------

# 21. Abstraction

## Theory

**Abstraction** means exposing the required behavior while hiding
unnecessary implementation details.

In TypeScript, abstraction can be achieved using:

-   Interfaces
-   Abstract classes
-   Encapsulation

### Automation Example

A test can call:

`loginPage.login(username, password)`

without needing to know every locator and low-level interaction used
internally.

------------------------------------------------------------------------

# 22. OOP Concepts in Automation

  OOP Concept      Example in Automation
  ---------------- --------------------------------------------------
  Class            `LoginPage`
  Object           `new LoginPage()`
  Property         Locator or Page reference
  Method           `clickLoginButton()`
  Inheritance      `CreateLead extends LoginPage`
  Overloading      Utility supporting multiple parameter signatures
  Overriding       Browser-specific `launch()`
  Interface        Common action contract
  Abstract class   Base Page/Base Browser
  Encapsulation    Private locators/internal state
  Abstraction      Expose business-level actions

------------------------------------------------------------------------

# 23. Best Practices

1.  Keep classes focused on one responsibility.
2.  Use meaningful method names such as `enterUsername()` and
    `clickLoginButton()`.
3.  Avoid unnecessarily deep inheritance.
4.  Put common behavior in a suitable base class.
5.  Use interfaces when the primary need is a contract.
6.  Use abstract classes when common implementation is also required.
7.  Keep implementation details hidden where possible.
8.  Prefer composition when inheritance creates unnecessary coupling.
9.  Use method overloading only when multiple signatures genuinely
    improve the API.
10. Keep Page Object methods focused on user actions and validations.

------------------------------------------------------------------------

# 24. Quick Revision

``` text
Class
→ Blueprint

Object
→ Instance of a class

Method
→ Action/behavior inside a class

Inheritance
→ Reuse parent functionality

Multilevel Inheritance
→ Inheritance through multiple levels

Overloading
→ Same method name, different signatures

Overriding
→ Child changes parent method implementation

Interface
→ Contract

Abstract Class
→ Contract + common implementation

Abstract Method
→ Method without implementation

Concrete Method
→ Method with implementation

super
→ Access parent class

extends
→ Class inheritance

implements
→ Interface implementation

new
→ Creates an object
```
