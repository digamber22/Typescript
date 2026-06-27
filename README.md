# Typescript

## 1. What Exactly is TypeScript?
* **The "Superset" Concept:** TypeScript is a superset of JavaScript. This means that everything you can write in JavaScript is already valid and available in TypeScript.
* **No New Syntax Features:** A common misconception is that TypeScript adds entirely new programming features. It **does not** give you new loops, new modules, or new arrow functions. It simply allows you to write your JavaScript in a much more precise manner.


## 2. Basic Syntax for Variable Declaration
* **The Syntax:** `let variableName: type = value;`
* **Lowercase Types:** All core types in TypeScript are written in lowercase (e.g., `string`, not `String`; `number`, not `Number`).
* **Example:** `let greetings: string = "Hello Hitesh";`
* **Type Safety:** Once `greetings` is defined as a `string`, TypeScript will throw an error if you try to assign a number (e.g., `greetings = 6`) or boolean to it later.

## 3. Fixing the "Cannot redeclare block-scoped variable" Error
* When writing basic TypeScript files in the same directory without proper configuration, you might see a squiggly line error complaining about redeclaring variables.
* **Temporary Fix:** You can add `export {}` to the file. This tells TypeScript to treat the file as an isolated module, temporarily getting rid of the error (this concept will be explored deeply in future videos).