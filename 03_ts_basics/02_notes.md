# Notes: Union Types in TS
**By Hitesh Choudhary**

## 1. What are Union Types?
* **The Concept:** A Union Type allows a variable, parameter, or property to accept more than one type of data. It is the strict, highly recommended alternative to using the `any` keyword when you are unsure exactly what type of data will be provided (e.g., an ID could be a number or a string).
* **The Syntax:** You use the pipe symbol (`|`) to separate the allowed types.
* **Syntax Example:**
  ```typescript
  // 'score' can strictly only be a number OR a string
  let score: number | string = 33;
  score = 44; // Valid
  score = "55"; // Valid
  // score = true; // ERROR: boolean is not allowed
  ```

## 2. Union Types with Custom Aliases
* Union types are incredibly powerful when combined with custom type aliases. You can dictate that an object can be one of several different structural shapes.
* **Example:**
  ```typescript
  type User = {
      name: string;
      id: number;
  };

  type Admin = {
      username: string;
      id: number;
  };

  // 'hitesh' can be formatted as a User OR an Admin
  let hitesh: User | Admin = { name: "Hitesh", id: 334 };

  // Re-assigning it to match the Admin shape is perfectly valid
  hitesh = { username: "hc", id: 334 }; 
  ```

## 3. Union Narrowing in Functions
* **The Problem:** If a function parameter accepts a Union Type (e.g., `id: number | string`), TypeScript will restrict you from using methods that don't apply to *both* types. For instance, you can't use `.toLowerCase()` on the `id` because that method doesn't exist for numbers.
* **The Solution (Type Narrowing):** You must use conditional checks (like `typeof`) inside your function to narrow down the exact type before applying type-specific logic.
* **Example:**
  ```typescript
  function getDbId(id: number | string) {
      if (typeof id === "string") {
          // Inside this block, TS knows 'id' is 100% a string
          id.toLowerCase(); 
      } else {
          // Inside this block, TS knows 'id' is 100% a number
          id + 2;
      }
  }
  ```

## 4. Union Types in Arrays
* Arrays can also accept mixed data types using Unions, but the syntax can be tricky and is a common source of beginner mistakes.
* **The Mistake:**
  ```typescript
  // WRONG (for mixed arrays): This means the array must be ENTIRELY numbers OR ENTIRELY strings.
  let data: number[] | string[] = [1, 2, "3"]; // Throws error
  ```
* **The Correct Syntax:** You must wrap the union types in parentheses before adding the array brackets to signify that the array *elements* can be a mix of these types.
  ```typescript
  // CORRECT: The array can contain a mix of numbers, strings, and booleans
  let data: (number | string | boolean)[] = [1, 2, "3", true];
  ```

## 5. Literal Types with Unions
* You can use Union Types to strictly limit a variable to a specific set of exact literal values. This acts almost like an Enum.
* **Example:**
  ```typescript
  // 'seatAllotment' can ONLY be assigned one of these three exact strings
  let seatAllotment: "aisle" | "middle" | "window";
  
  seatAllotment = "aisle"; // Valid
  // seatAllotment = "crew"; // ERROR: "crew" is not an allowed literal value

  let pi:3.14 = 3.14
  pi = 3.1456    // ERROR:3.1456 is not an allowed literal value
  ```