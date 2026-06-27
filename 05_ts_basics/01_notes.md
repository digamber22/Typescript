# Generics in TypeScript

## Introduction
Generics are a vital feature in TypeScript used for writing reusable, production-level code. They allow developers to build **components**—a broader term referring to functions, arrays, or chunks of code (not just React or Tailwind components)—that are capable of working over a variety of types rather than a single one. 

## The Problem without Generics
When creating an identity function (a function that simply returns the argument it is given), you might initially define specific types:

```typescript
function identity1(val: number | boolean): number | boolean {
    return val;
}
```
* **Limitation:** This approach isn't scalable if you need the function to support strings or other data types. You'd have to continuously add to the union type (`number | boolean | string | ...`).

To bypass this, developers sometimes resort to using the `any` keyword:

```typescript
function identity2(val: any): any {
    return val;
}
```
* **Limitation:** The `any` keyword is a bad escape hatch. It completely removes type information. With `any`, the compiler doesn't know the exact type being passed or returned. You could input a `number` but return a `string`, and TypeScript wouldn't throw an error. 

## The Solution: Generics
Generics solve this by using angular brackets `<Type>` to capture the type of the argument provided by the user. 

```typescript
function identity3<Type>(val: Type): Type {
    return val;
}
```
* **How it works:** It acts similarly to `any` by accepting all types, but **it locks the type once it is provided**. If you pass a `number` as an input, the type is locked as `number`, ensuring the return type is strictly a `number`.

### Example Usage:
```typescript
identity3(3);        // Locks 'Type' as number
identity3("hitesh"); // Locks 'Type' as string
identity3(true);     // Locks 'Type' as boolean
```

## The `<T>` Shortcut Convention
Instead of writing the full word `<Type>`, developers conventionally use a single capital letter, most commonly `<T>`, to denote the generic type.

```typescript
function identity4<T>(val: T): T {
    return val;
}
```
*Note: You can use any word or letter (e.g., `<H>`), as long as it's consistently referenced.*

## Custom Types with Generics
Generics are exceptionally powerful because they work with your custom interfaces and types, not just primitive types like numbers or strings.

```typescript
interface Bottle {
    brand: string;
    type: number;
}

// Using the custom interface as a generic type
identity4<Bottle>({ brand: "Milton", type: 1 });
```

## Built-in Generics: Arrays
TypeScript already utilizes generics under the hood, particularly with Arrays. You can define an array using generic syntax to enforce what type of data the array holds:

```typescript
const score: Array<number> = [];
const names: Array<string> = [];
```

## Conclusion
Generics allow you to build robust, highly reusable, and strictly typed components. You will encounter them frequently when working with modern frameworks like React or Angular!