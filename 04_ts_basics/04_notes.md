# Notes: Why interface is important in TS
**By Hitesh Choudhary**

## 1. Interfaces as Protocols for Classes
* **The Concept:** So far, we've seen interfaces used to define the shape of simple objects. However, their most powerful use case in object-oriented programming is acting as a strict **protocol** or **blueprint** for classes.
* **The `implements` Keyword:** When a class uses the `implements` keyword alongside an interface, TypeScript forces that class to include all the properties and methods defined in that interface.
* **Real-World Analogy:** Think of a smartphone camera. If an app (like Instagram or Snapchat) wants to access the camera, the mobile operating system provides a standard "interface" (protocol). The app *must* follow this protocol to successfully utilize the camera features.

## 2. Basic Implementation Example
* **Defining the Interface:**
  ```typescript
  interface TakePhoto {
      cameraMode: string;
      filter: string;
      burst: number;
  }
  ```
* **Implementing it in a Class:**
  ```typescript
  class Instagram implements TakePhoto {
      constructor(
          public cameraMode: string,
          public filter: string,
          public burst: number
      ) {}
  }
  ```
  *If the `Instagram` class forgets to include the `burst` property, TypeScript will throw an error because the class is failing to implement the complete `TakePhoto` protocol.*

## 3. Adding Extra Properties (More is Allowed, Less is Not)
* When a class implements an interface, it must contain **at least** the properties and methods defined in the interface. 
* However, the class is perfectly allowed to declare **additional** properties and methods of its own that aren't dictated by the interface.
* **Example:**
  ```typescript
  class YouTube implements TakePhoto {
      constructor(
          public cameraMode: string,
          public filter: string,
          public burst: number,
          public short: string // This extra property is completely valid!
      ) {}
  }
  ```

## 4. Implementing Multiple Interfaces
* A single class can implement multiple interfaces at the same time. This is incredibly useful for building complex, feature-rich classes out of smaller, modular protocols.
* **The Syntax:** Separate the interface names with a comma.
* **Example:**
  ```typescript
  interface TakePhoto {
      cameraMode: string;
      filter: string;
      burst: number;
  }

  interface Story {
      createStory(): void;
  }

  // The class must now fulfill the requirements of BOTH interfaces
  class Snapchat implements TakePhoto, Story {
      constructor(
          public cameraMode: string,
          public filter: string,
          public burst: number
      ) {}

      // Must include the method dictated by the 'Story' interface
      createStory(): void {
          console.log("Story was created successfully");
      }
  }
  ```
#
  # Notes: Abstract Classes in TypeScript

## 1. What is an Abstract Class?
An **abstract class** is a specialized blueprint for other classes. Unlike regular classes, you **cannot** create an instance (object) of an abstract class directly using `new`. They are intended to be inherited by subclasses.

*   **`abstract` Keyword:** The class must be defined using the `abstract` keyword.
*   **No Direct Instantiation:** Trying to run `new AbstractClassName()` will cause the TypeScript compiler to throw an error.

## 2. Key Features
*   **Abstract Methods:** You can define methods marked with `abstract` that have **no implementation (body)**. Any class that inherits (extends) the abstract class **must** provide its own implementation for these methods.
*   **Concrete Methods:** Unlike interfaces, abstract classes can contain fully functional methods with logic. Subclasses will inherit these methods automatically.
*   **Constructors & Properties:** You can define properties and constructors, which subclasses will inherit.

## 3. Implementation Example
In this example, `TakePhoto` defines a protocol that subclasses must follow, while also providing shared logic.

```typescript
abstract class TakePhoto {
    constructor(public cameraMode: string, public filter: string) {}

    // Abstract method: MUST be implemented by any subclass
    abstract getSepia(): void;

    // Concrete method: inherited by all subclasses
    getReelTime(): number {
        // Logic shared by all subclasses
        return 8; 
    }
}

class Instagram extends TakePhoto {
    constructor(
        public cameraMode: string, 
        public filter: string, 
        public burst: number
    ) {
        super(cameraMode, filter);
    }

    // Implementing the required abstract method
    getSepia(): void {
        console.log("Sepia filter is applied");
    }
}

const hc = new Instagram("test", "Test", 3);
hc.getSepia(); // From implementation
console.log(hc.getReelTime()); // Inherited from TakePhoto
```

## 4. Comparison: Abstract Class vs. Interface

| Feature | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Implementation** | Can have both abstract and concrete methods. | Only defines signatures (no logic). |
| **State** | Can hold properties/fields and constructors. | Cannot hold state or constructors. |
| **Purpose** | Used to share code among *related* classes. | Used to define a contract for *any* class. |

## 5. When to Use Which?
*   Use an **abstract class** when you want to define a base class that shares common behavior and state among a hierarchy of related objects.
*   Use an **interface** when you want to define a strict "contract" or protocol that completely unrelated classes can implement.