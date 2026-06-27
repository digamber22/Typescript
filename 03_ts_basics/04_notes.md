# Notes: Interface in typescript
**By Hitesh Choudhary**

## 1. What is an Interface?
* **The Concept:** An interface in TypeScript is very similar to a `type` alias. It is used to define the shape of an object—acting as a strict protocol or blueprint. 
* **High-Level View:** It forces the object to have specific properties and methods with exact return types, but it does **not** care about the actual underlying logic or *how* those methods are implemented. Think of it like an operating system interface: you know clicking a folder opens it, but you don't need to know the hardware-level logic happening behind the scenes.

## 2. Basic Syntax, Optional, and Readonly
* You declare it using the `interface` keyword. Just like type aliases, you can use `readonly` and optional (`?`) modifiers.
* **Code Example:**
  ```typescript
  interface User {
      readonly dbId: number;
      email: string;
      userId: number;
      googleId?: string; // Optional property
  }
  ```

## 3. Defining Methods in Interfaces
* There are two common ways to define that an interface must contain a specific function/method.
* **Method 1 (Arrow Function Syntax):**
  ```typescript
  interface User {
      // ...other properties
      startTrial: () => string; 
  }
  ```
* **Method 2 (Standard Function Syntax - Preferred by Hitesh):**
  ```typescript
  interface User {
      // ...other properties
      startTrial(): string;
  }
  ```

## 4. Method Parameters and Implementation
* You can define methods that require parameters. 
* **Important Note:** When you actually implement the interface in an object, the **parameter names do not have to match exactly**—only their data types must match.
* **Code Example:**
  ```typescript
  interface User {
      readonly dbId: number;
      email: string;
      userId: number;
      
      // Method expecting a string and returning a number
      getCoupon(couponName: string, value: number): number; 
  }

  // Implementing the User interface
  const hitesh: User = {
      dbId: 2211,
      email: "h@h.com",
      userId: 111,
      
      // The parameter names here ('name' and 'off') differ from the interface definition 
      // ('couponName' and 'value'), but TS allows this as long as the types match!
      getCoupon: (name: "h10", off: 10) => {
          return 10; // Returning the required number
      }
  };
  ```

## 5. Teaser for the Next Video
* Interfaces and Type Aliases are easily confused because they do almost the very same thing. The specific differences and advanced interface features (like "reopening" an interface or extending it) will be covered in the next video.