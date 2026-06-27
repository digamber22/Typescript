# Notes: Your first intro to typescript docs
**By Hitesh Choudhary**

## 1. The Importance of Documentation
* **Core Skill:** The ultimate way to master TypeScript is to learn how to read its official documentation (`typescriptlang.org`).
* **Docs Navigation:** Go to Docs -> Basics -> "Everyday Types" to see the foundational specifications of the language.

## 2. Understanding Types in TypeScript
* **It's All About Types:** The core of TypeScript revolves around mastering available types and knowing how to utilize them.
* **Common Types:** Includes primitive types (`number`, `string`, `boolean`), as well as `null`, `undefined`, `void`, `object`, `arrays`, and `tuples`.
* **Special Types:** TypeScript also features special types like `unknown` and `never`.
* **The Danger of `any`:** Avoid using the `any` keyword. Using `any` intentionally turns off TypeScript's strict checking, making your code vulnerable and behaving just like raw JavaScript. It usually indicates a lack of certainty about what data type should be used.

## 3. Why TypeScript is Useful (Use Case Scenarios)
* **Input Validation:** In regular JS, if a function accepts two numbers, you often have to write explicit, defensive code inside the function to verify the inputs are actually numbers. TypeScript handles this type-checking automatically, saving you from writing extra validation lines.
* **Predictable Outputs:** If a function is supposed to return a string, TypeScript enforces this. When working in teams, this guarantees that other developers won't accidentally break the app by returning a number or another unexpected type from that function.

## 4. Basic Syntax for Variable Declaration
* **The Syntax:** `let variableName: type = value;`
* **Lowercase Types:** All core types in TypeScript are written in lowercase (e.g., `string`, not `String`; `number`, not `Number`).
* **Example:** `let greetings: string = "Hello Hitesh";`
* **Type Safety:** Once `greetings` is defined as a `string`, TypeScript will throw an error if you try to assign a number (e.g., `greetings = 6`) or boolean to it later.

## 5. Editor Features & Error Prevention
* **Type-Specific Methods:** When you type a dot (`.`) after a variable, TypeScript only suggests methods valid for that specific data type. For example, it won't let you call `.toUpperCase()` on a `number`.
* **Typo Correction:** If you misspell a built-in method (e.g., typing `.toLowercase()` instead of the correct `.toLowerCase()`), TypeScript catches the typo and suggests the correct capitalization.

## 6. Fixing the "Cannot redeclare block-scoped variable" Error
* When writing basic TypeScript files in the same directory without proper configuration, you might see a squiggly line error complaining about redeclaring variables.
* **Temporary Fix:** You can add `export {}` to the file. This tells TypeScript to treat the file as an isolated module, temporarily getting rid of the error (this concept will be explored deeply in future videos).
#
# TypeScript Error: "Cannot redeclare block-scoped variable"

## The Root Cause: Global Scope vs. Module Scope
This is a very common error when first learning TypeScript. It happens because of how TypeScript distinguishes between **Scripts** and **Modules**:

1. **A Script:** If a file has no `import` or `export` statements, TypeScript assumes it is a traditional script. Scripts share a **single, global scope**.
2. **A Module:** If a file contains at least one `import` or `export`, TypeScript treats it as a module. Modules have their own **isolated, local scope**.

When you create multiple basic TypeScript files in the same folder without a configuration file (`tsconfig.json`), TypeScript treats all of them as "Scripts" living in the exact same global space.

## The Scenario

Imagine you create two files to practice different concepts:

**`variables.ts`**
```typescript
let myName = "Alice"; 
```

**`functions.ts`**
```typescript
// ERROR: Cannot redeclare block-scoped variable 'myName'.
let myName = "Bob"; 
```

Because both files are treated as being in the same global scope, TypeScript thinks you are trying to declare the block-scoped variable (`let` or `const`) `myName` twice.

## The Temporary Fix: `export {}`

You can fix this by adding `export {}` to the bottom (or top) of your file:

**`functions.ts` (Fixed)**
```typescript
let myName = "Bob"; 

// This tells TS: "Treat this file as its own isolated module!"
export {}; 
```

**Why it works:** You aren't actually exporting any variables, but the mere presence of the `export` keyword flips a switch inside the TypeScript compiler. It stops treating the file as a global script and gives it its own private, isolated scope. The `myName` variable no longer clashes with other files.

## The "Real" Fix (For Real Projects)
While `export {}` is a great temporary hack when sketching out ideas, you won't do this in real applications. 

In a real project, you generate a `tsconfig.json` file. Modern setups include a setting like `"moduleDetection": "force"`, which automatically treats every file as its own module, even if you forget to add an `export` or `import`.