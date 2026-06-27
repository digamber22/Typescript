# Notes: Why to learn Typescript
**By Hitesh Choudhary**

## 1. Prerequisites and Mindset
* **Learn JavaScript First:** There is a rush in the market to jump straight into TypeScript, but the creator highly recommends having a solid foundation in JavaScript before starting TypeScript.

## 2. What Exactly is TypeScript?
* **The "Superset" Concept:** TypeScript is a superset of JavaScript. This means that everything you can write in JavaScript is already valid and available in TypeScript.
* **No New Syntax Features:** A common misconception is that TypeScript adds entirely new programming features. It **does not** give you new loops, new modules, or new arrow functions. It simply allows you to write your JavaScript in a much more precise manner.

## 3. How TypeScript Works Under the Hood
* **Development Experience:** TypeScript's main benefit happens *while* you write code. It catches potential runtime errors and displays them immediately in your editor (like VS Code) before you even run the program.
* **Compilation to JS:** Browsers don't understand TypeScript. All TS code is ultimately compiled down into standard JavaScript.
* *Note on Compilation:* Even if your code editor yells at you with squiggly lines for a type error, the compiler will still allow you to compile it into JS (though it will likely still throw errors when you try to run it).

## 4. When You Shouldn't Use TypeScript
* **Tiny Projects:** If your project is incredibly small (e.g., just two files with 5-10 lines of code each), enforcing TypeScript rules is completely unnecessary.
* **The `any` Keyword:** If you implement TypeScript just for the "fanciness" of having `.ts` files, but you bypass all the rules by slapping the `any` keyword everywhere, you are not using TypeScript correctly.

## 5. The Core Philosophy: Type Safety
* The single most important takeaway from the video is that TypeScript is entirely about **Type Safety**.
* **Fixing JS Quirks:** JavaScript has notoriously quirky behaviors because it lacks strict type safety. TypeScript stops you from executing these mismatched type errors. Examples of raw JavaScript quirks that TS prevents:
    * Adding a number `2` to a string `"2"` gives you `"22"`.
    * Adding `2` to `null` gives `2`.
    * Adding `2` to `undefined` gives `NaN` (Not a Number).