# Notes: Private Public in Typescript
**By Hitesh Choudhary**

## 1. Classes in TypeScript
* **The Basics:** Just like in object-oriented JavaScript, you can create classes in TypeScript. However, TypeScript allows you to strictly type the properties of the class before initializing them in the constructor.
* **Basic Syntax Example:**
  ```typescript
  class User {
      email: string;
      name: string;
      city: string = ""; // Default value initialized

      constructor(email: string, name: string) {
          this.email = email;
          this.name = name;
      }
  }

  const hitesh = new User("h@h.com", "hitesh");
  hitesh.city = "Jaipur"; 
  ```

## 2. Access Modifiers: Public and Private
* **The `public` Keyword:** By default, every property and method in a TypeScript class is `public`. This means it can be accessed and modified from outside the class (e.g., `hitesh.city = "Delhi"`). You can explicitly write `public` before the property name, but it is not required.
* **The `private` Keyword:** If you want to restrict access to a property so it can only be used *inside* the class itself, you use the `private` keyword. 
* **Example:**
  ```typescript
  class User {
      public email: string;
      public name: string;
      private readonly city: string = "Jaipur"; 

      constructor(email: string, name: string) {
          this.email = email;
          this.name = name;
      }
  }

  const hitesh = new User("h@h.com", "hitesh");
  // hitesh.city = "Delhi"; // ERROR: Property 'city' is private and only accessible within class 'User'.
  ```

## 3. TypeScript `private` vs JavaScript `#`
* **JS Private Fields:** In modern JavaScript, private fields are denoted using the hash symbol (`#`). 
* **TypeScript Counterpart:** While you can use the `#` syntax in TypeScript (if your target compiler settings support it), the `private` keyword is the more traditional, readable, and widely used TypeScript approach. Both achieve the same goal of encapsulating data.

## 4. The Professional Shorthand Syntax
* **Writing Less Code:** In the basic example, we declare properties at the top, then pass them in the constructor, and finally assign them with `this.prop = prop`. This is repetitive.
* **The Shortcut:** TypeScript offers a shorthand. If you add an access modifier (`public`, `private`, or `protected`) directly to the constructor parameters, TypeScript automatically declares the property and assigns the value for you behind the scenes.
* **Refactored Code Example (Best Practice):**
  ```typescript
  class User {
      // By adding public/private in the constructor, we don't need to declare them above or write 'this.email = email'
      constructor(
          public email: string, 
          public name: string, 
          private userId: string
      ) {}
  }

  const hitesh = new User("h@h.com", "hitesh", "1234");
  // hitesh.userId // ERROR: Cannot access private property
  ```
  *This shorthand is heavily used in professional codebases and frameworks like Angular to keep class definitions clean and concise.*