# Generic Classes and Constraints in TypeScript

## Introduction
This lesson dives deeper into Generics, focusing on **Generic Constraints** using the `extends` keyword, and **Generic Classes**. Understanding these concepts helps you write scalable, organized code, particularly for large, production-level projects. 

## Generic Constraints (`extends`)
Sometimes, a standard Generic (`<T>`) is too broad. You might want to use Generics to maintain flexibility but still enforce that the input meets specific criteria. This is where the `extends` keyword comes in.

### The Problem with Unconstrained Generics:
If you have a generic function that takes two arguments, it will accept anything:

```typescript
function anotherFunction<T, U>(valOne: T, valTwo: U): object {
    return {
        valOne,
        valTwo
    }
}

// Allowed, but maybe you only want numbers for the second argument?
anotherFunction(3, "4"); 
```

### Applying Constraints:
You can use `extends` to restrict the generic type.

```typescript
function constrainedFunction<T, U extends number>(valOne: T, valTwo: U): object {
    return {
        valOne,
        valTwo
    }
}

// Error: Argument of type 'string' is not assignable to parameter of type 'number'
// constrainedFunction(3, "4"); 

// Allowed
constrainedFunction(3, 4.6); 
```

### Real-World Use Case (Interfaces):
Constraints are incredibly useful when working with custom interfaces (like a database configuration) where you want to ensure the passed generic object contains at least the required properties.

```typescript
interface Database {
    connection: string;
    username: string;
    password: string;
}

// The generic type T MUST be an object that includes the properties defined in the Database interface.
function dbConnector<T extends Database>(valOne: T) {
    // Operations here...
}
```

## Generic Classes
Generics aren't just for functions; they are highly effective when applied to **Classes**. A generic class acts as a template that can work with various data types without needing to rewrite the logic for each type. 

### Scenario: E-Commerce Platform
Imagine you are building a platform that sells both **Quizzes** and **Courses**. They have different properties, but both can be added to a shopping cart. 

```typescript
interface Quiz {
    name: string;
    type: string;
}

interface Course {
    name: string;
    author: string;
    subject: string;
}
```

Instead of writing a specific Cart class for `Quiz` and a separate one for `Course`, you can write one **Generic Class** to handle both (or any future sellable items like `Bundles`).

```typescript
// The <T> indicates this is a Generic Class
class Sellable<T> {
    
    // A cart array that holds items of type T
    public cart: T[] = [];

    // A method to add items of type T to the cart
    addToCart(product: T) {
        this.cart.push(product);
    }
}

// Example Usage:
// const courseCart = new Sellable<Course>();
// const quizCart = new Sellable<Quiz>();
```

### Key Takeaways for Generic Classes:
* **Future-Proofing:** If your project expands to sell new types of items, this generic class will still work perfectly without modifications.
* **Shared Logic:** Generic classes are ideal for extracting shared logic (like adding to a cart or managing state) into a single, reusable component. 
* **Not a Silver Bullet:** While powerful, generic classes don't solve everything. You might still need specific classes for highly specialized operations, but generic classes beautifully handle common, overlapping functionalities.