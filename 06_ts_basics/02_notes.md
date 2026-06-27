# `instanceof` and Type Predicates in TypeScript

## Introduction
This document continues the topic of **Type Narrowing** by exploring two powerful tools: the `instanceof` operator and **Type Predicates**. These techniques allow you to precisely narrow down types so that TypeScript can fully understand the specific data you are working with, unlocking the appropriate methods and properties.

## 1. The `instanceof` Operator
The `instanceof` operator is used to check if an object was constructed using a specific class or constructor function (anything created with the `new` keyword). While `typeof` is great for basic primitives (`string`, `number`), `instanceof` is the tool you need for complex objects, dates, or arrays.

### Example: Narrowing with `instanceof`
```typescript
function logValue(x: Date | string) {
    // We cannot use x.toUTCString() here because 'x' might be a string.
    
    // Narrowing down using instanceof
    if (x instanceof Date) {
        // TypeScript now knows 100% that 'x' is a Date object
        console.log(x.toUTCString());
    } else {
        // TypeScript knows 100% that 'x' is a string here
        console.log(x.toUpperCase());
    }
}
```
* **When to use:** Use `instanceof` whenever you are checking variables that could be instances of classes (e.g., `Date`, custom classes, or `Array`).

## 2. Type Predicates (`is` Keyword)
Sometimes, custom validation functions return a simple `boolean` (`true` or `false`). However, simply returning a boolean doesn't help TypeScript's type checker know *what* type the variable was successfully validated as. 

To solve this, we use **Type Predicates**. A type predicate is a special return type syntax (`parameterName is Type`) that tells the TypeScript compiler: *"If this function returns true, treat this variable as this specific type from now on."*

### Scenario Setup
Let's define two types that have different methods:
```typescript
type Fish = {
    swim: () => void;
}

type Bird = {
    fly: () => void;
}
```

### The Problem Without Type Predicates
We write a validation function to check if a pet is a `Fish`:
```typescript
// Returning a simple boolean
function isFish(pet: Fish | Bird): boolean {
    return (pet as Fish).swim !== undefined;
}

function getFood(pet: Fish | Bird) {
    if (isFish(pet)) {
        // ERROR/ISSUE: TypeScript STILL thinks 'pet' is 'Fish | Bird' 
        // It doesn't know that isFish() returning true means 'pet' is a Fish.
        return "fish food";
    } else {
        return "bird food";
    }
}
```

### The Solution: Type Predicates
By changing the return type of `isFish` from `boolean` to `pet is Fish`, we bridge the logical gap for the TypeScript compiler.

```typescript
// Using a Type Predicate
function isFish(pet: Fish | Bird): pet is Fish {
    return (pet as Fish).swim !== undefined;
}

function getFood(pet: Fish | Bird) {
    if (isFish(pet)) {
        // SUCCESS: TypeScript now knows 'pet' is 100% a Fish here!
        return "fish food";
    } else {
        // SUCCESS: TypeScript now knows 'pet' is 100% a Bird here!
        return "bird food";
    }
}
```

### Breakdown of `pet is Fish`:
1. `pet`: This must be the name of the parameter passed into the function.
2. `is`: The special TypeScript keyword used for predicates.
3. `Fish`: The specific type we are locking the parameter to if the function evaluates to `true`.

## Conclusion
* Use **`instanceof`** to narrow down types instantiated with the `new` keyword.
* Use **Type Predicates (`is`)** in custom validation functions so the TypeScript compiler can understand exactly what type a variable has been narrowed down to after a `true` evaluation.