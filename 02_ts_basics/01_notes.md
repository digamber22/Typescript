# Notes: Number, boolean and type inference
**By Hitesh Choudhary**

## 1. Numbers in TypeScript
* **No Floats/Ints:** As explicitly stated in the TypeScript documentation, JavaScript (and by extension, TypeScript) does not have special runtime values for integers or floats. There is no `int` or `float` type.
* **The `number` Type:** Whether it's a whole number (`3344`) or a decimal (`3344.2`), it is strictly defined using the `number` type.
* **Syntax:** `let userId: number = 334466;`
* **Method Constraints:** When you annotate a variable as a `number`, TypeScript will only suggest methods relevant to numbers (e.g., `.toFixed()`, `.toExponential()`, `.toLocaleString()`).

## 2. Booleans in TypeScript
* **The `boolean` Type:** Used for `true` or `false` values.
* **Syntax:** `let isLoggedIn: boolean = false;`
* **Method Constraints:** Similar to numbers, typing a dot after a boolean variable will only reveal methods applicable to booleans (which are very few, mostly just `.valueOf()`).

## 3. Type Inference: The Core Concept
* **The Problem of Overuse:** Beginners often get overly excited about type annotations and try to explicitly type *everything*. 
  * Example of overuse: `let userId: number = 334466;`
* **What is Type Inference?** If you initialize a variable with a value immediately upon declaration, TypeScript is smart enough to *infer* its type automatically.
  * *Better code:* `let userId = 334466;`
* **Why Inference is Better Here:** Explicitly typing a variable that is immediately assigned a value is considered redundant and not a best practice. It is "too obvious."
* **Safety is Retained:** Even without the explicit `: number` annotation, if you initialize it as a number (`let userId = 3344`), TypeScript will still throw an error if you later try to assign a string to it (e.g., `userId = "hitesh"`). The type safety is still completely intact.

## 4. Summary
* Do not put colons and explicit types on every single variable in your file. 
* Rely on TypeScript's type inference when a value is assigned immediately. 
* Explicit types are useful for specific situations (which will be covered in future videos), but shouldn't be overused for simple, immediate assignments.
* Keep in mind that TypeScript annotations (like `: boolean` or `: number`) are completely stripped away when the file is compiled into plain JavaScript.

#
# TypeScript Fundamentals: Type Inference and Compilation

## 1. Type Inference vs. Over-Annotation

When starting with TypeScript, it is tempting to explicitly declare the type for every single variable. However, this often leads to redundant code.

**The Problem: Over-Annotation**
Explicitly typing a variable that is immediately assigned a value is considered an anti-pattern because the type is already obvious.
```typescript
// Redundant and not a best practice
let userId: number = 334466;
```

**The Solution: Type Inference**
If you initialize a variable with a value immediately upon declaration, TypeScript automatically infers its type. 
```typescript
// Better, cleaner code
let userId = 334466; 
```

**Why Inference is Powerful:**
* **Cleaner Code:** Your code looks much closer to standard JavaScript while remaining completely safe.
* **Strict Type Safety:** Even without the `: number` annotation, TypeScript remembers that `userId` was initialized as a number. If you try to reassign it to a string later (e.g., `userId = "hitesh"`), the TypeScript compiler will strictly throw an error.

---

## 2. Type Erasure and Compilation

Browsers and runtime environments (like Node.js) cannot execute TypeScript natively. They only understand plain JavaScript. Because of this, TypeScript acts purely as a **development-time** tool.

**The Compilation Process**
When you compile your `.ts` files into `.js` files (using a tool like `tsc`), the TypeScript compiler checks for errors and then **completely strips away all type annotations**.

*TypeScript (Development):*
```typescript
function calculateTotal(price: number, isTaxable: boolean): number {
    if (isTaxable) {
        return price * 1.2;
    }
    return price;
}
```

*JavaScript (Compiled Output):*
```javascript
function calculateTotal(price, isTaxable) {
    if (isTaxable) {
        return price * 1.2;
    }
    return price;
}
```

**Key Takeaways:**
* **No Runtime Checking:** Because types are erased during compilation, TypeScript cannot protect your application at runtime. 
* **External Data:** If your running application fetches data from an API and receives a string instead of an expected number, TypeScript will not catch this error. You must still write standard JavaScript validation for external data at runtime.