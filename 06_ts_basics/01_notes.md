# Type Narrowing in TypeScript

## Introduction
In TypeScript, you often deal with variables that can hold multiple types (e.g., `number | string`). **Type narrowing** is the process of writing code that forces TypeScript to narrow down that broad type to a specific, single type so you can safely perform operations on it. It’s less of a "problem-and-solution" concept and more of a series of cautionary practices to ensure your code behaves correctly.

## The Problem with `typeof`
JavaScript’s `typeof` operator has some quirks that you need to be aware of when narrowing types:
* `typeof 1` returns `"number"`
* `typeof "hello"` returns `"string"`
* `typeof ""` (empty string) returns `"string"`
* **The Catch:** `typeof [1, 2, 3]` returns `"object"`, and `typeof null` *also* returns `"object"`. 

This behavior is standard JavaScript, but it requires developers to be extra cautious when validating arrays or `null` values.

## Type Guards (Using `typeof`)
The easiest way to narrow down a type is by using the `typeof` operator. In TypeScript documentation, using `typeof` in conditionals is often referred to with the fancy term **"Type Guard"**.

### Example 1: Basic Narrowing
```typescript
function detectTypes(val: number | string) {
    // TypeScript errors if you try to use a string/number method before checking the type:
    // return val.toLowerCase(); // Error! 'val' could be a number.

    if (typeof val === "string") {
        // Here, TypeScript knows 'val' is definitely a string
        return val.toLowerCase();
    }
    if (typeof val === "number") {
        // Here, TypeScript knows 'val' is definitely a number
        return val + 3;
    }
}
```

## Narrowing with `null`
When writing business logic, it's common for an argument (like an ID) to either be a valid string or `null` (if not provided). You must manually narrow down the type to exclude the `null` case before operating on the variable.

### Example 2: Handling `null`
```typescript
function provideId(id: string | null) {
    // Narrowing to check if 'id' is falsy (like null)
    if (!id) {
        console.log("Please provide ID");
        return;
    }
    
    // Because of the early return above, TypeScript knows 'id' is guaranteed to be a string here.
    return id.toLowerCase();
}
```

## Cautionary Case: Truthiness and Empty Strings
Sometimes, checking for truthiness (`if (strs)`) doesn't cover all business cases, particularly in JavaScript where an empty string (`""`) is considered falsy.

### Example 3: The Flawed `printAll` Example
Take a look at this cautionary example straight from the TypeScript documentation:

```typescript
function printAll(strs: string | string[] | null) {
    // Check 1: Is strs truthy? (Eliminates 'null', but ALSO eliminates an empty string "")
    if (strs) {
        // Check 2: Is it an array? (In JS, arrays have typeof "object")
        if (typeof strs === "object") {
            for (const s of strs) {
                console.log(s);
            }
        } else if (typeof strs === "string") {
            console.log(strs);
        }
    }
}
```
* **The Issue:** While this code successfully handles arrays, valid strings, and `null` without crashing, it completely ignores empty strings (`""`). Because `""` is falsy, the code inside `if (strs)` never runs. In real-world business logic, you might need to handle empty strings explicitly rather than just dropping them alongside `null`.

## Conclusion
Type narrowing is all about writing defensive code (Type Guards). Be particularly mindful of JavaScript's inherent quirks, like arrays and `null` evaluating to `"object"`, and empty strings evaluating to falsy values.