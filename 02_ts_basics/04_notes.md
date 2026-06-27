# Notes: A better way to write function in typescript
**By Hitesh Choudhary**

## 1. Explicit Return Types
* **The Problem:** In JavaScript, a function can return anything. If you expect a function to return a number but it accidentally returns a string, it can crash your application—especially in large codebases with multiple developers.
* **The Solution:** You should explicitly define the return type of your functions immediately after the parameter list.
* **Syntax Example:**
  ```typescript
  function addTwo(num: number): number {
      // TypeScript will now throw an error if we try to return "hello"
      return num + 2; 
  }
  ```

## 2. Returning Different Types (Introduction to Unions)
* Sometimes a function needs to return different types based on conditional logic (e.g., returning a boolean or a string). 
* **Example of the issue:**
  ```typescript
  function getValue(myVal: number) {
      if (myVal > 5) {
          return true;
      }
      return "200 OK";
  }
  ```
* *Note: The strict way to handle this using TypeScript is through Union Types, which will be covered in depth in a future video.*

## 3. Arrow Functions Return Types
* Typing the return value of an arrow function follows the exact same logic. You place the colon and the return type right before the arrow (`=>`).
* **Example:**
  ```typescript
  const getHello = (s: string): string => {
      return "";
  }
  ```

## 4. Contextual Typing in Array Methods (like `.map`)
* TypeScript is smart enough to infer types dynamically when working with arrays. If you have an array of strings, TypeScript automatically knows the mapped items are strings. If you change the array to numbers, the type automatically switches.
* **Best Practice:** While TypeScript can infer the *input* of the map callback, it is highly recommended to explicitly annotate the *return* type of the callback function to enforce strictness.
* **Example:**
  ```typescript
  const heroes = ["thor", "spiderman", "ironman"];
  // const heroes = [1, 2, 3]; // Context automatically switches to numbers

  heroes.map((hero): string => {
      return `hero is ${hero}`;
      // return 2; // This would throw an error because we enforced a string return
  });
  ```

## 5. The `void` Type
* If a function is solely designed to perform an action (like logging to the console) and does **not return anything**, you should strictly type its return value as `void`.
* **Example:**
  ```typescript
  function consoleError(errmsg: string): void {
      console.log(errmsg);
      // return 1; // Not allowed because the function is strictly void
  }
  ```

## 6. The `never` Type
* The `never` type is explicitly meant for functions that **never return a value** under any circumstances. 
* According to the official documentation, `never` is used when a function throws an exception or intentionally terminates the execution of the program.
* **Difference from `void`:** `void` means the function runs to completion but outputs nothing. `never` means the function *never finishes executing normally* (it crashes or throws an error).
* **Example:**
  ```typescript
  function handleError(errmsg: string): never {
      throw new Error(errmsg);
  }
  ```