# Notes: Type Aliases in Typescript
**By Hitesh Choudhary**

## 1. The Problem with Inline Object Typing
* In previous videos, we typed object parameters directly inside the function signature (e.g., `function createUser(user: {name: string, email: string, isActive: boolean})`). 
* **The Issue:** If you have an object with 15 properties, and you need to use this same structure across 8 different functions (like `createUser`, `getUserDetails`, `modifyUser`), writing out that inline type every time becomes incredibly lengthy, redundant, and hard to maintain.

## 2. Introduction to Type Aliases
* **What is it?** A type alias allows you to define a custom type (like a blueprint for an object) once, name it, and reuse it throughout your codebase anywhere a type is expected.
* **The Keyword:** You use the `type` keyword to create an alias.
* **Syntax Example:**
  ```typescript
  // Creating a Type Alias
  type User = {
      name: string;
      email: string;
      isActive: boolean;
  };
  ```

## 3. Using Type Aliases in Functions
* Once defined, you can use your custom type alias exactly like you would use built-in types like `string` or `boolean`.

### As a Parameter Type
* You can enforce that a function argument matches your custom type.
  ```typescript
  function createUser(user: User) {
      // The compiler ensures 'user' contains name, email, and isActive
  }

  // Calling the function
  createUser({ name: "", email: "", isActive: true });
  ```

### As a Return Type
* You can also enforce that a function returns an object matching your custom type.
  ```typescript
  function createUser(user: User): User {
      // Must return an object that satisfies the User type
      return { name: "", email: "", isActive: true };
  }
  ```

## 4. Renaming Built-in Types (A Quirky Feature)
* **Technical Capability:** You can technically use type aliases to rename built-in types. 
  * Example: `type MyString = string;`
* **Real-World Use:** While technically allowed, it is rarely useful. The only practical use case might be if an entire team strictly prefers a certain naming convention (e.g., renaming `boolean` to `bool` using `type bool = boolean;`). 

## 5. Documentation Connection
* This concept aligns directly with the "Type Aliases" section in the official TypeScript documentation. 
* A common documentation example creates a `Point` type (`type Point = { x: number, y: number }`) to simplify functions handling coordinate geometry.
* **Best Practice Tip:** In a real-world app, you will typically define all your `type` aliases in one file, export them, and import them into whatever files and functions need them, keeping your function definitions clean and readable.