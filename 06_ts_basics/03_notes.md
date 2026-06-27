# Discriminated Unions and Exhaustiveness Checking with `never` in TypeScript

## Introduction
This concludes the deep dive into **Type Narrowing** by exploring two advanced concepts: **Discriminated Unions** and **Exhaustiveness Checking** using the `never` type. These concepts act as safeguards for your codebase, especially as it grows and evolves.

## 1. Discriminated Unions
When you have multiple interfaces that might share a broad type, it becomes difficult for TypeScript to know which specific interface it's dealing with. A **Discriminated Union** is a pattern where you add a common, literal property (often named `kind`, `type`, or similar) to all related interfaces. This property acts as a "discriminator" to easily narrow down the type.

### Defining Interfaces with a Discriminator
Notice how each interface below has a `kind` property set to a specific literal string:

```typescript
interface Circle {
    kind: "circle";
    radius: number;
}

interface Square {
    kind: "square";
    side: number;
}

interface Rectangle {
    kind: "rectangle";
    length: number;
    width: number;
}

// A generic Shape type that can be any of the three
type Shape = Circle | Square | Rectangle;
```

### Narrowing with the Discriminator
Now, you can use the `kind` property to narrow the type with perfect autocomplete support:

```typescript
function getTrueShape(shape: Shape) {
    if (shape.kind === "circle") {
        // TypeScript knows 'shape' is definitely a Circle
        return Math.PI * shape.radius ** 2;
    } else if (shape.kind === "square") {
        // TypeScript knows 'shape' is definitely a Square
        return shape.side * shape.side;
    } 
    // Additional cases...
}
```

## 2. Exhaustiveness Checking with `never`
Codebases evolve. If you add a new interface (like `Rectangle`) to your `Shape` union but forget to update the functions that process `Shape`, you could introduce silent bugs.

**Exhaustiveness checking** prevents this by using TypeScript's `never` type in a `switch` statement's `default` case. It forces the compiler to yell at you if you haven't accounted for every possible type in a union.

### Example: Future-Proofing Code

```typescript
function getArea(shape: Shape) {
    switch (shape.kind) {
        case "circle":
            return Math.PI * shape.radius ** 2;
        case "square":
            return shape.side * shape.side;
        case "rectangle":
            return shape.length * shape.width;
            
        // The Exhaustiveness Check
        default:
            // We assign 'shape' to a variable explicitly typed as 'never'.
            // If all cases above are handled, 'shape' theoretically becomes 'never' here.
            const _defaultForShape: never = shape;
            return _defaultForShape;
    }
}
```

### Why does this work?
1. If your `switch` statement successfully handles all possible values of `shape.kind` (`circle`, `square`, `rectangle`), the code will theoretically never reach the `default` block. Therefore, TypeScript is happy assigning `shape` to `never`.
2. **The Magic:** If someone comes along later and adds a `Triangle` interface to the `Shape` type, TypeScript will immediately throw an error at the `default` block. It will complain: *"Type 'Triangle' is not assignable to type 'never'."* This strict error acts as an automatic reminder for the developer to add a `case "triangle"` to the switch block, keeping the code fully future-proof.