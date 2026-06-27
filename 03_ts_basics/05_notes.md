# Notes: Interface vs Type in typescript
**By Hitesh Choudhary**

## 1. The Core Confusion
* **The Similarity:** Interfaces and Type Aliases (`type`) look incredibly similar and, for most typical object-shaping use cases, they do exactly the same thing. 
* **The Choice:** According to the official TypeScript documentation, you can use either for most tasks. However, it's recommended to use `interface` until you specifically need features that only `type` can provide (like defining specific primitives, unions, or tuples).

## 2. Difference #1: "Re-opening" an Interface (Declaration Merging)
* **Interfaces:** One of the most powerful features of interfaces is that you can declare an interface with a specific name, and later in the code (or in another file), declare an interface with the *exact same name* to add more properties to it. The TypeScript compiler will automatically merge them.
* **Code Example (Interfaces):**
  ```typescript
  interface User {
      email: string;
      userId: number;
  }

  // Somewhere else in the code, or importing from a library:
  // We can "re-open" the User interface and inject new properties
  interface User {
      githubToken: string;
  }

  // Now, any object of type 'User' MUST have email, userId, AND githubToken
  const hitesh: User = {
      email: "h@h.com",
      userId: 2211,
      githubToken: "github123"
  };
  ```
* **Types:** You **cannot** do this with Type Aliases. Once a `type` is defined, it is locked. Trying to define a `type` with the same name twice will throw an error.

## 3. Difference #2: Extending / Inheritance
* **Interfaces:** Interfaces can easily inherit properties from other interfaces using the `extends` keyword, making them fantastic for object-oriented design.
* **Code Example (Interfaces):**
  ```typescript
  interface User {
      email: string;
      userId: number;
  }

  // Admin inherits everything from User, and adds a 'role' property
  interface Admin extends User {
      role: "admin" | "ta" | "learner";
  }

  const hiteshAdmin: Admin = {
      email: "h@h.com",
      userId: 2211,
      role: "admin"
  };
  ```
* **Types:** To achieve a similar result with `type`, you have to use Intersection Types (the `&` symbol), which we covered previously. It works, but the syntax is less clean and less aligned with traditional Object-Oriented Programming than `extends`.

## 4. Summary: When to Use Which?
* Use **`interface`** when you are defining the shape of an object, especially if you are building libraries or APIs where you or other developers might need to extend or inject new properties into the object shape later.
* Use **`type`** when you need to define Unions (e.g., `type ID = number | string`), Tuples, or when you are aliasing basic primitive values.