# Notes: Getters and Setters in typescript
**By Hitesh Choudhary**

## 1. What are Getters and Setters?
* **The Concept:** Getters and Setters in TypeScript function almost exactly as they do in standard JavaScript. They are methods that allow you to control access to a class's properties, especially private properties. 
* **Why Use Them:** You typically use them to expose a `private` property to the outside world, but with additional logic or restrictions applied (e.g., validating data before setting it, or formatting data before getting it). You don't have to have both; you can have a getter without a setter if you want a property to be read-only from the outside.

## 2. Implementing a Getter (`get`)
* You use the `get` keyword to define a getter.
* **Important:** A getter must always return a value, so it's best practice to annotate the return type explicitly.
* **Code Example:**
  ```typescript
  class User {
      private _courseCount = 1;

      // ...constructor and other properties...

      // A simple getter to expose the private property
      get courseCount(): number {
          return this._courseCount;
      }

      // A getter that adds logic/formatting to a property
      get getAppleEmail(): string {
          return `apple_${this.email}`; 
      }
  }
  ```

## 3. Implementing a Setter (`set`)
* You use the `set` keyword to define a setter. A setter takes an argument (the new value you want to assign).
* **The "Gotcha" (Interview Question):** In TypeScript, **a setter cannot have a return type annotation—not even `void`.** If you try to write `set courseCount(num): void`, TypeScript will throw an error. It is designed this way strictly by the TS compiler.
* **Code Example:**
  ```typescript
  class User {
      private _courseCount = 1;

      // The Setter (Notice there is NO return type annotation like ': void')
      set courseCount(courseNum) {
          if (courseNum <= 1) {
              throw new Error("Course count should be more than 1");
          }
          this._courseCount = courseNum;
      }
  }
  ```

## 4. Private Methods
* Just like properties can be `private` or `public`, methods can also have access modifiers.
* If you mark a method as `private`, it can only be called by other methods *inside* the class. You cannot call it from a created instance of the class (e.g., `hitesh.deleteToken()` will fail).
* **Code Example:**
  ```typescript
  class User {
      // ...properties...

      private deleteToken() {
          console.log("Token deleted");
      }
  }

  const hitesh = new User("h@h.com", "hitesh");
  // hitesh.deleteToken(); // ERROR: Property 'deleteToken' is private.
  ```