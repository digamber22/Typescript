# Notes: Bad behaviour of objects in typescript
**By Hitesh Choudhary**

## 1. Typical Object Usage in TypeScript
* Simply defining a standalone object is essentially identical to raw JavaScript. The true power and primary use case of objects in TypeScript come into play when you are passing objects *into* functions or returning objects *from* functions.

## 2. Passing Objects into Functions
* You can explicitly define the shape of the object a function should accept directly in the parameter list.
* **Code Example:**
  ```typescript
  // The function expects an object with a specific string 'name' and boolean 'isPaid'
  function createUser({name, isPaid}: {name: string, isPaid: boolean}) {
      // function body
  }

  // Calling it correctly
  createUser({name: "Hitesh", isPaid: false});
  ```

## 3. Returning Objects from Functions
* The syntax for defining a function that *returns* a strictly typed object can look a bit weird and confusing for beginners because of the nested brackets.
* **Code Example:**
  ```typescript
  // The object definition after the colon dictates what MUST be returned.
  function createCourse(): {name: string, price: number} {
      // You must return an object matching the exact structure defined above
      return {
          name: "ReactJS",
          price: 399
      };
  }
  ```

## 4. The "Bad Behavior" (Object Literal vs. Variable Assignment)
* TypeScript has a known, odd behavior regarding strict property checking that catches many developers off guard. 

### The Strict Check (Inline Object)
If you pass an object literal directly into a function call, TypeScript strictly checks the properties. If you pass an extra property that wasn't defined in the function signature, it throws an error.
* **Code Example (Throws Error):**
  ```typescript
  // ERROR: Object literal may only specify known properties. 'email' does not exist.
  createUser({name: "Hitesh", isPaid: false, email: "h@h.com"}); 
  ```

### The Loophole / Bad Behavior (Variable Assignment)
If you define the exact same object and assign it to a variable *first*, and then pass that variable into the function, TypeScript's strict checking ignores the extra properties and **does not throw an error**.
* **Code Example (No Error!):**
  ```typescript
  let newUser = {
      name: "Hitesh", 
      isPaid: false, 
      email: "h@h.com" // This extra property will be ignored by the checker!
  };

  // This is perfectly valid and throws NO ERRORS, despite the extra 'email' property.
  createUser(newUser); 
  ```
* **Why this matters:** In real-world applications (like a MERN stack backend), you often build objects progressively from different sources before passing them to a database function. This loophole means bad data can easily slip through.
* **The Solution:** This issue is typically resolved using "Interfaces" and "Type Aliases," which enforce stricter rules and allow for optional properties. These concepts will be covered in the next videos.