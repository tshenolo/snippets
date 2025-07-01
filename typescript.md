# TypeScript Cheatsheet

TypeScript is a superset of JavaScript that adds static types. This cheatsheet covers core TypeScript concepts, types, interfaces, classes, functions, generics, and more.

## Basic Setup and Compilation

*   **Installation**:
    ```bash
    npm install -g typescript
    # or
    # yarn global add typescript
    ```
*   **Compilation**:
    ```bash
    tsc filename.ts # Compiles filename.ts to filename.js
    tsc --init      # Creates a tsconfig.json file for project-wide settings
    tsc             # Compiles all .ts files in the project based on tsconfig.json
    tsc -w          # Watch mode: recompile on file changes
    ```
*   **`tsconfig.json` (Common Options)**:
    ```json
    {
      "compilerOptions": {
        "target": "es6",          // Target JavaScript version (e.g., "es5", "es6", "es2020")
        "module": "commonjs",     // Module system (e.g., "commonjs", "es6", "amd")
        "outDir": "./dist",       // Output directory for compiled JS files
        "rootDir": "./src",       // Root directory of source .ts files
        "strict": true,           // Enable all strict type-checking options
        "esModuleInterop": true,  // Enables compatibility with CommonJS modules
        "skipLibCheck": true,     // Skip type checking of declaration files
        "forceConsistentCasingInFileNames": true,
        // "sourceMap": true,      // Generate source maps for debugging
        // "declaration": true,    // Generate .d.ts declaration files
        // "noImplicitAny": true,  // Raise error on expressions and declarations with an implied 'any' type.
        // "strictNullChecks": true // Null and undefined cannot be assigned to other types.
      },
      "include": ["src/**/*"],    // Glob patterns for files to include
      "exclude": ["node_modules", "dist"] // Glob patterns for files to exclude
    }
    ```

## Basic Types

*   **`boolean`**:
    ```typescript
    let isActive: boolean = true;
    ```
*   **`number`**: All numbers are floating-point.
    ```typescript
    let decimal: number = 6;
    let hex: number = 0xf00d;
    let binary: number = 0b1010;
    let octal: number = 0o744;
    ```
*   **`string`**: Textual data, can use single quotes, double quotes, or template literals.
    ```typescript
    let color: string = "blue";
    color = 'red';
    let fullName: string = `Bob Bobbington`;
    let sentence: string = `Hello, my name is ${fullName}.`;
    ```
*   **`array`**: Two ways to declare:
    ```typescript
    let list1: number[] = [1, 2, 3];
    let list2: Array<number> = [1, 2, 3]; // Generic array type
    let names: string[] = ["Alice", "Bob"];
    ```
*   **`tuple`**: Array with a fixed number of elements whose types are known, but need not be the same.
    ```typescript
    let x: [string, number];
    x = ["hello", 10]; // OK
    // x = [10, "hello"]; // Error
    console.log(x[0].substring(1)); // "ello"
    // console.log(x[1].substring(1)); // Error, 'number' does not have 'substring'
    ```
*   **`enum`**: A way of giving more friendly names to sets of numeric values.
    ```typescript
    enum Color {Red, Green, Blue} // Starts at 0 by default
    let c: Color = Color.Green; // 1

    enum HttpStatus {OK = 200, NotFound = 404, ServerError = 500}
    let statusVal: HttpStatus = HttpStatus.OK; // 200
    let statusName: string = HttpStatus[200]; // "OK"
    ```
*   **`any`**: Opt-out of type checking. Avoid using if possible, as it defeats the purpose of TypeScript.
    ```typescript
    let notSure: any = 4;
    notSure = "maybe a string instead";
    notSure = false; // okay, definitely a boolean
    ```
*   **`void`**: Absence of having any type at all. Typically used as the return type of functions that do not return a value.
    ```typescript
    function warnUser(): void {
        console.log("This is my warning message");
    }
    let unusable: void = undefined; // Can only assign undefined or null (if strictNullChecks is false)
    ```
*   **`null` and `undefined`**: Subtypes of all other types by default. With `strictNullChecks: true`, `null` and `undefined` can only be assigned to `any` and their respective types (or `void`).
    ```typescript
    let u: undefined = undefined;
    let n: null = null;
    // With strictNullChecks:
    // let name: string = null; // Error
    // let age: number = undefined; // Error
    ```
*   **`never`**: Represents the type of values that never occur. For functions that always throw an error or never return.
    ```typescript
    function error(message: string): never {
        throw new Error(message);
    }
    function infiniteLoop(): never {
        while (true) {}
    }
    ```
*   **`object`**: Represents a non-primitive type, i.e., anything that is not `number`, `string`, `boolean`, `bigint`, `symbol`, `null`, or `undefined`.
    ```typescript
    let obj: object = { key: "value" };
    // obj = "string"; // Error
    // obj = 123; // Error
    ```
*   **`unknown`**: Type-safe counterpart of `any`. You must perform some form of checking before operating on `unknown` values.
    ```typescript
    let value: unknown;
    value = true;
    value = 42;
    // let num: number = value; // Error: Type 'unknown' is not assignable to type 'number'.
    if (typeof value === 'number') {
        let num: number = value; // OK
        console.log(num + 10);
    }
    ```

## Type Assertions (Casting)

Tells the compiler to treat a value as a specific type. Does not perform any special checking or restructuring of data.
```typescript
let someValue: any = "this is a string";
let strLength1: number = (someValue as string).length;
let strLength2: number = (<string>someValue).length; // JSX syntax conflicts with this style

// Be careful: if the assertion is wrong, runtime errors can occur.
// let wrongValue: any = 5;
// let strLengthWrong: number = (wrongValue as string).length; // Runtime error, 5 has no length
```

## Interfaces

Define the "shape" or contract of an object.
```typescript
interface Person {
    firstName: string;
    lastName: string;
    age?: number; // Optional property
    readonly ssn?: string; // Readonly property
    greet?(): void; // Optional method
}

function printPerson(person: Person): void {
    console.log(`Name: ${person.firstName} ${person.lastName}`);
    if (person.age) {
        console.log(`Age: ${person.age}`);
    }
    if (person.greet) {
        person.greet();
    }
}

let user: Person = { firstName: "John", lastName: "Doe", age: 30 };
// user.ssn = "123"; // Error if ssn is readonly and already set or not set at declaration
printPerson(user);

// Interface for function types
interface SearchFunc {
    (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function(src, sub) {
    return src.search(sub) > -1;
}

// Indexable Types (for arrays or objects used like dictionaries)
interface StringArray {
    [index: number]: string;
}
let myArray: StringArray = ["Bob", "Fred"];
let first = myArray[0];

interface NumberDictionary {
    [index: string]: number;
    length: number; // OK, length is a number
    // name: string;  // Error, the type of 'name' is not a subtype of the numeric index type
}
```

## Classes

Blueprints for creating objects.
```typescript
class Animal {
    // Properties (member variables)
    public name: string; // public is default
    private species: string; // private: accessible only within this class
    protected sound: string; // protected: accessible within this class and subclasses

    // Constructor
    constructor(name: string, species: string, sound: string = "makes a sound") {
        this.name = name;
        this.species = species;
        this.sound = sound;
    }

    // Methods
    public move(distanceInMeters: number = 0): void {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }

    public makeSound(): void {
        console.log(`${this.name} ${this.sound}.`);
    }

    private getSpecies(): string {
        return this.species;
    }
}

class Dog extends Animal { // Inheritance
    constructor(name: string) {
        super(name, "Canis familiaris", "barks"); // Call parent constructor
    }

    // Override method
    public makeSound(): void {
        console.log(`${this.name} ${this.sound} loudly!`);
    }

    public wagTail(): void {
        console.log(`${this.name} wags its tail.`);
        // console.log(this.species); // Error: species is private to Animal
        console.log(this.sound);   // OK: sound is protected
    }
}

let tom: Animal = new Animal("Tom the Cat", "Felis catus");
tom.move(10);
tom.makeSound();

let buddy: Dog = new Dog("Buddy");
buddy.move(5);
buddy.makeSound(); // Buddy barks loudly!
buddy.wagTail();

// Parameter properties (shorthand for declaring and initializing properties in constructor)
class Octopus {
    readonly numberOfLegs: number = 8;
    constructor(readonly name: string) { // 'readonly name: string' is a parameter property
    }
}
let o = new Octopus("Ollie");
console.log(o.name); // Ollie

// Abstract classes (cannot be instantiated directly, must be subclassed)
abstract class Department {
    constructor(public name: string) {}
    printName(): void { console.log("Department name: " + this.name); }
    abstract printMeeting(): void; // Must be implemented in derived class
}
class AccountingDepartment extends Department {
    constructor() { super("Accounting and Auditing"); }
    printMeeting(): void { console.log("The Accounting Department meets each Monday at 10am."); }
}
// let department: Department = new Department("Common"); // Error: Cannot create an instance of an abstract class.
let accounting: Department = new AccountingDepartment();
accounting.printName();
accounting.printMeeting();
```

## Functions (with Types)

```typescript
// Named function
function add(x: number, y: number): number {
    return x + y;
}

// Anonymous function (function expression)
let multiply = function(x: number, y: number): number { return x * y; };

// Arrow function
const subtract = (x: number, y: number): number => x - y;

// Optional parameters (must come after required parameters or have default values)
function buildName(firstName: string, lastName?: string): string {
    if (lastName) return firstName + " " + lastName;
    else return firstName;
}
let result1 = buildName("Bob"); // Bob
let result2 = buildName("Bob", "Adams"); // Bob Adams

// Default parameters
function greet(name: string, greeting: string = "Hello"): string {
    return `${greeting}, ${name}!`;
}
console.log(greet("Alice")); // Hello, Alice!
console.log(greet("Bob", "Hi")); // Hi, Bob!

// Rest parameters (collect multiple arguments into an array)
function buildFullName(firstName: string, ...restOfName: string[]): string {
    return firstName + " " + restOfName.join(" ");
}
let employeeName = buildFullName("Joseph", "Samuel", "Lucas", "MacKinzie"); // Joseph Samuel Lucas MacKinzie

// Function overloading (multiple function signatures for the same function name)
function processInput(input: string): string;
function processInput(input: number): number;
function processInput(input: string | number): string | number {
    if (typeof input === "string") {
        return input.toUpperCase();
    } else {
        return input * 2;
    }
}
console.log(processInput("test")); // TEST
console.log(processInput(10));   // 20
// console.log(processInput(true)); // Error
```

## Generics

Create reusable components that can work over a variety of types rather than a single one.
```typescript
// Generic function
function identity<T>(arg: T): T {
    return arg;
}
let output1 = identity<string>("myString"); // Explicitly set T to string
let output2 = identity(100); // Type inference: T is number

// Generic interface
interface GenericIdentityFn<T> {
    (arg: T): T;
}
let myIdentity: GenericIdentityFn<number> = identity;

// Generic class
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;

    constructor(zero: T, addFn: (x: T, y: T) => T) {
        this.zeroValue = zero;
        this.add = addFn;
    }
}
let myGenericNumber = new GenericNumber<number>(0, (x, y) => x + y);
console.log(myGenericNumber.add(5, 10)); // 15
let myGenericString = new GenericNumber<string>("", (x, y) => x + y);
console.log(myGenericString.add("hello", " world")); // hello world

// Generic Constraints (limit the types that can be used with a generic)
interface Lengthwise {
    length: number;
}
function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length); // Now we know it has a .length property
    return arg;
}
// loggingIdentity(3); // Error, number does not have 'length' property
loggingIdentity({length: 10, value: 3}); // OK
loggingIdentity("test string"); // OK
loggingIdentity([1,2,3]); // OK
```

## Type Inference

TypeScript infers types when possible if you don't explicitly provide them.
```typescript
let message = "Hello, TypeScript!"; // message is inferred as type 'string'
// message = 10; // Error: Type 'number' is not assignable to type 'string'.

function sum(a: number, b: number) { // Return type is inferred as 'number'
    return a + b;
}
```

## Union Types

A value can be one of several types.
```typescript
function printId(id: number | string): void {
    console.log("Your ID is: " + id);
    if (typeof id === "string") {
        console.log(id.toUpperCase()); // OK, id is string here
    } else {
        console.log(id + 10); // OK, id is number here
    }
}
printId(101);
printId("202abc");
// printId({ myID: 22342 }); // Error
```

## Intersection Types

Combine multiple types into one.
```typescript
interface ErrorHandling {
    success: boolean;
    error?: { message: string };
}
interface ArtworksData {
    artworks: { title: string }[];
}
type ArtworksResponse = ArtworksData & ErrorHandling; // Intersection

let response: ArtworksResponse = {
    success: true,
    artworks: [{ title: "Mona Lisa" }],
    // error: { message: "An error occurred" } // Optional
};
```

## Type Aliases

Create a new name for a type.
```typescript
type Point = { x: number; y: number; };
type ID = string | number;
type StringOrNumberArray = (string | number)[];

let p1: Point = { x: 10, y: 20 };
let userId: ID = "user123";
userId = 456;
```

## Literal Types

Specify exact values a string, number, or boolean must have.
```typescript
let httpMethod: "GET" | "POST" | "PUT" | "DELETE";
httpMethod = "GET"; // OK
// httpMethod = "PATCH"; // Error

type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;
let roll: DiceRoll = 3; // OK
```

## Type Guards and Narrowing

Using `typeof`, `instanceof`, `in` operator, or user-defined type guards to narrow down types within a conditional block.
```typescript
function isFish(pet: Fish | Bird): pet is Fish { // User-defined type guard
    return (pet as Fish).swim !== undefined;
}
interface Fish { swim(): void; }
interface Bird { fly(): void; }

function move(pet: Fish | Bird) {
    if (isFish(pet)) {
        pet.swim(); // pet is Fish here
    } else {
        pet.fly(); // pet is Bird here
    }
}
```

## Modules (ES6 style)

Organize code into separate files.
```typescript
// ---- utility.ts ----
// export function logMessage(message: string): void {
//     console.log(message);
// }
// export const APP_NAME: string = "My Awesome App";

// ---- main.ts ----
// import { logMessage, APP_NAME } from './utility';
// logMessage(`Welcome to ${APP_NAME}`);

// Default exports
// ---- math.ts ----
// export default function add(x: number, y: number): number { return x + y; }
// ---- app.ts ----
// import sumNumbers from './math'; // Can name default import anything
// console.log(sumNumbers(5,3));
```

## Declaration Files (`.d.ts`)

Used to describe the shape of existing JavaScript code (e.g., third-party libraries) for TypeScript.
Many popular libraries have their type declarations available via `@types/package-name` on NPM.
```bash
npm install --save-dev @types/lodash
```
If types are not available, you can write your own `.d.ts` files.
```typescript
// Example: my-js-lib.d.ts
// declare module "my-js-lib" {
//   export function doSomething(value: string): boolean;
//   export const version: string;
// }

// Then in your .ts file:
// import { doSomething, version } from "my-js-lib";
```

This provides a solid, actionable cheatsheet for TypeScript. I'll proceed with `java.md`.The `typescript.md` cheatsheet has been successfully updated with detailed explanations and code examples for its type system, interfaces, classes, functions, generics, modules, and other core features.

Next, I will enhance `java.md`, focusing on its OOP principles, core syntax, common data structures from the Collections Framework, and an introduction to Streams.
