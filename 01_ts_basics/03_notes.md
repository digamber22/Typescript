# Notes: How to install typescript
**By Hitesh Choudhary**

## 1. Installation Strategies
* **Two Main Approaches:** There are two different ways to install and use TypeScript depending on what you're trying to achieve:
  1.  **Global System Install:** Ideal for learning core concepts, creating basic files, and getting a handle on the language without worrying about project-specific constraints.
  2.  **Project-Level Install (e.g., React, Angular):** Requires a specific `tsconfig.json` file to manage settings and preferences. In this scenario, it is installed as a "dev dependency" (`npm install typescript --save-dev`).

## 2. Prerequisites
* **Node.js:** You must have Node.js installed. Verify by typing `node -v` in your terminal. Any modern version is fine for following along.
* **NPM:** Node Package Manager (NPM) comes bundled with Node.js.
* **Terminal/Shell:** 
  * *Windows:* It is highly recommended to use **Git Bash** or PowerShell rather than the default command prompt to ensure access to Linux-friendly commands (like `cd`, `ls`). 
  * *Mac/Linux:* The default terminal works fine.

## 3. Global Installation Steps
1. Open your terminal (Run as Administrator on Windows, or prepare to use `sudo` on Mac/Linux).
2. Run the command: `npm install -g typescript`
   * *(The `-g` flag is what installs it globally across your entire machine.)*
3. Verify the installation by running: `tsc -v`
   * `tsc` stands for **TypeScript Compiler**. If this returns a version number, the installation was successful.

## 4. Writing and Compiling Your First TypeScript File
* **Setup:** Create a new folder for your code and open it in your editor (e.g., VS Code).
* **Creating a File:** Create a file named `intro.ts`. The `.ts` extension tells the editor that this is a TypeScript file.
* **Writing Code:** You can write standard JavaScript inside this file. For example:
  ```typescript
  let user = { name: "Hitesh", age: 10 };
  console.log(user.name);
  ```
* **Compiling:** Open the terminal in your project directory and run: `tsc intro.ts`
* **The Result:** The compiler takes your `.ts` file and generates a corresponding `intro.js` file. The output code inside the `.js` file is the vanilla JavaScript equivalent, ready to be run in a browser or Node environment.

## 5. TypeScript in Action: The "Squiggly Line" Warning
* If you try to log a property that doesn't exist, e.g., `console.log(user.email);`, VS Code will immediately give you a red squiggly line warning: `"Property 'email' does not exist on type..."`.
* **Important Note:** Even with the error present in the `.ts` file, if you run `tsc intro.ts`, the compiler will *still* generate the `intro.js` file with the flawed code. TypeScript warns you during development but doesn't completely block the creation of the JavaScript file by default.

## 6. Configuration (Preview)
* In a real project, you will use a `tsconfig.json` file.
* This file allows you to customize strictness, define module systems (like ESNext or CommonJS), target specific JavaScript versions (like ES2017), and restrict what gets compiled. We will dive deeper into this in future tutorials.

## 7. Myth Busted
* To reinforce the previous video, TypeScript *does not* mean writing less code. Often, you will write significantly more lines of TypeScript to ensure type safety, which then compiles down to a very concise block of JavaScript.