# Notes: Protected in Typescript
**By Hitesh Choudhary**

## 1. The Limitation of `private`
* **The Problem:** In previous videos, we learned that marking a property as `private` restricts its access entirely to the class where it was defined.
* **The Scenario:** When building real-world applications, you often use inheritance (one class extending another). If a child class inherits from a parent class, it **cannot** access the parent's `private` properties.
* **Example of the Limitation:**
  ```typescript
  class User {
      private _courseCount = 1;
      
      constructor(public email: string, public name: string) {}
  }

  // SubUser inherits from User
  class SubUser extends User {
      isFamily: boolean = true;

      changeCourseCount() {
          // ERROR: Property '_courseCount' is private and only accessible within class 'User'.
          // this._courseCount = 4; 
      }
  }
  ```

## 2. The `protected` Access Modifier
* **What is it?** The `protected` keyword is the middle ground between `public` (accessible everywhere) and `private` (accessible nowhere outside the parent class).
* **How it works:** A `protected` property or method cannot be accessed from outside the class instances (just like `private`), but it **can** be accessed by any class that inherits from that parent class.
* **The Fix using `protected`:**
  ```typescript
  class User {
      // Changed from private to protected
      protected _courseCount = 1; 
      
      constructor(public email: string, public name: string) {}
  }

  class SubUser extends User {
      isFamily: boolean = true;

      changeCourseCount() {
          // PERFECTLY VALID: Because _courseCount is protected, the inherited class has access!
          this._courseCount = 4; 
      }
  }

  const hitesh = new User("h@h.com", "hitesh");
  // hitesh._courseCount = 2; // ERROR: Still protected, cannot be accessed outside the class hierarchy!
  ```

## 3. Summary of Access Modifiers
* **`public` (Default):** Accessible anywhere—inside the class, outside the class, and in inherited classes.
* **`private`:** Accessible **only** within the exact class where it is defined. Not accessible in child classes.
* **`protected`:** Accessible within the class where it is defined **and** within any classes that inherit from it (child classes), but still completely hidden from outside instances. 

## 4. Why Use Inheritance and `protected`?
* This pattern is extremely common when you have a base class with core functionality (like `User`) and you want to create specialized classes (like `AdminUser`, `SubUser`, `PaidUser`) that share the core properties but also need to tweak or read internal states that shouldn't be exposed to the public API.