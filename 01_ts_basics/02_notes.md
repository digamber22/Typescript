# Notes: Typescript is not what you think
**By Hitesh Choudhary**

## 1. What TypeScript Is vs. What It Isn't
* **Not a Standalone Language:** Many people believe TypeScript is a completely new, independent programming language. This is not 100% true. It is heavily—in fact entirely—dependent on JavaScript.
* **It's a Development Tool:** It is more accurate to describe TypeScript as a development tool or a wrapper around JavaScript. Its primary purpose is to help you write cleaner, more maintainable code with fewer errors.
* **Production Code is Still JS:** The final code that actually runs in production environments (like browsers or Node.js) is 100% pure JavaScript. 

## 2. The Core Function: Static Checking
* **One Main Job:** The sole fundamental job of TypeScript is **static checking**.
* **What is Static Checking?:** Static checking means the code parser constantly analyzes your syntax while you type it in the IDE. It catches errors immediately (e.g., trying to access an undefined object property) instead of waiting for runtime execution to throw an error in your face.
* **Borrowed Concept:** This static checking functionality is borrowed from other strictly typed languages like Java and Golang.

## 3. The Myth of Writing "Less Code"
* **More Code in TS:** A common myth is that using TypeScript allows you to write less code. The reverse is actually true. You will write *more* code in TypeScript compared to raw JavaScript.
* **Compilation Ratios:** Sometimes 50 lines of TypeScript code will compile down to just 10 lines of vanilla JavaScript. However, the extra effort is worth it for the added type safety and maintainability.

## 4. The Development & Compilation Process
* **File Extensions:** 
  * You write TS code in a `.ts` file. 
  * If you are working with components (like in React) where HTML is baked in, you use `.tsx`.
* **Transpilation:** Your TypeScript code is "transpiled" (or compiled) into standard JavaScript. 
* **The "Squiggly Line" Reality:** Even if TypeScript analyzes your code and gives you a red squiggly line indicating a type error, **it does not stop you from compiling that code into JavaScript**. The JS code will still be produced and might even run. TypeScript merely warns you about the *potential* error; it doesn't hard-block the compilation process.

## 5. Summary
* TypeScript does not magically fix all JavaScript quirks automatically; you still need to know how to enforce type safety properly. 
* It's a layer on top of JS that adds new keywords (like Union and interfaces) to facilitate strict type checking, but at the end of the day, it's just a development tool that outputs regular JavaScript.