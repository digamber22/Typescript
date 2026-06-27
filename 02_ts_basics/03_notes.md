# Notes: Do you really know functions in typescript
**By Hitesh Choudhary**

## 1. The Core Problem with Functions in TypeScript
* **Implicit `any` in Parameters:** If you define a function and pass a parameter without explicitly assigning a type, TypeScript implicitly assigns it an `any` type. 
* **Why This is Bad:** Because the parameter is treated as `any`, you could mistakenly pass strings into a math function, or call inappropriate string methods on a number, defeating the entire purpose of TypeScript's strict checking.

## 2. Explicitly Typing Function Parameters
* **The Solution:** Always define the type of the arguments your function accepts directly in the parameter list.
* **Basic Function Example:**
  ```typescript
  function addTwo(num: number) {
      return num + 2;
  }
  
  // This is allowed:
  addTwo(5); 
  
  // This will throw an error because it expects a number:
  // addTwo("5"); 
  ```

* **Multiple Parameters Example:**
  ```typescript
  function signUpUser(name: string, email: string, isPaid: boolean) {
      // Function body
  }

  signUpUser("Hitesh", "hitesh@lco.dev", false);
  ```

## 3. Arrow Functions and Default Parameters
* **Typing Arrow Functions:** The syntax for adding types to an arrow function is identical to regular functions. You add the colon and type right after the parameter name.
* **Default Values:** You might want to assign default values so that a function can be called without providing every single argument.
* **Syntax for Defaults:** `parameter: type = defaultValue`
* **Example:**
  ```typescript
  let loginUser = (name: string, email: string, isPaid: boolean = false) => {
      // Function body
  }

  // Because isPaid has a default value, we can call it with just two arguments:
  loginUser("h", "h@h.com");
  ```
  *When compiled to JavaScript, TypeScript automatically generates the necessary conditional checks (e.g., checking if `isPaid` is `void 0` and falling back to `false`) to handle default values.*

## 4. The Next Issue: Function Return Types
* **The Vulnerability:** While we have secured what goes *into* the function (the parameters), we haven't secured what comes *out*. 
* **Example of the Problem:**
  ```typescript
  function addTwo(num: number) {
      // We expect this function to return a number, but TypeScript 
      // currently allows us to return a string without throwing an error!
      return "hello"; 
  }

  let myValue = addTwo(5);
  ```
* **Teaser for Part 2:** The next video will cover how to explicitly define and strictly type the **return values** of functions, preventing accidental returns of incorrect data types.