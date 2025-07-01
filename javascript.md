# JavaScript (ES6+) Cheatsheet

This cheatsheet covers common JavaScript (ECMAScript 6 and later) syntax, data types, operators, control flow, functions, arrays, objects, DOM manipulation, and modern ES6+ features. Examples are primarily for browser environments but many apply to Node.js as well.

## Basic Syntax & Variables

*   **Comments**:
    ```javascript
    // This is a single-line comment

    /*
    This is a
    multi-line comment.
    */
    ```
*   **Variables (ES6+)**:
    *   `let`: Block-scoped variable, can be reassigned.
        ```javascript
        let message = "Hello";
        message = "Hi";
        console.log(message); // Hi
        if (true) {
            let blockVar = "I am block scoped";
            console.log(blockVar);
        }
        // console.log(blockVar); // ReferenceError: blockVar is not defined
        ```
    *   `const`: Block-scoped variable, must be initialized, cannot be reassigned (but mutable if it's an object/array).
        ```javascript
        const PI = 3.14159;
        // PI = 3.14; // TypeError: Assignment to constant variable.

        const person = { name: "Alice" };
        person.name = "Bob"; // This is allowed, modifying the object's property
        console.log(person.name); // Bob
        // person = { name: "Charlie" }; // TypeError
        ```
    *   `var` (Older, function-scoped or globally-scoped, generally avoid in modern JS):
        ```javascript
        var count = 100;
        function testVar() {
            var localVar = "local";
            console.log(count); // 100 (can access outer scope)
        }
        // console.log(localVar); // ReferenceError
        ```
*   **Console Output**:
    ```javascript
    console.log("Simple log message");
    console.warn("This is a warning");
    console.error("This is an error");
    let user = { id: 1, name: "Test" };
    console.table(user); // Displays object/array as a table
    ```

## Data Types

*   **Primitive Types**:
    *   `String`: Sequence of characters.
        ```javascript
        let greeting = "Hello, World!";
        let name = 'Alice';
        let multiline = `This is a
        multi-line string.`; // Template literal (ES6)
        ```
    *   `Number`: Integers and floating-point numbers.
        ```javascript
        let integer = 10;
        let floatNum = 3.14;
        let notANumber = NaN; // Special numeric value
        let infinity = Infinity;
        ```
    *   `Boolean`: `true` or `false`.
        ```javascript
        let isActive = true;
        let isLoggedIn = false;
        ```
    *   `Null`: Represents the intentional absence of any object value.
        ```javascript
        let noValue = null;
        ```
    *   `Undefined`: A variable that has been declared but not assigned a value.
        ```javascript
        let notAssigned;
        console.log(notAssigned); // undefined
        ```
    *   `Symbol` (ES6): Unique and immutable primitive value, often used as object property keys.
        ```javascript
        const sym1 = Symbol('description');
        const sym2 = Symbol('description');
        console.log(sym1 === sym2); // false
        ```
    *   `BigInt` (ES2020): For arbitrarily large integers.
        ```javascript
        const bigNumber = 1234567890123456789012345678901234567890n;
        const anotherBigInt = BigInt(123);
        ```
*   **Object Type**: Collections of key-value pairs (properties and methods).
    ```javascript
    let car = {
        make: "Toyota",
        model: "Camry",
        year: 2021,
        start: function() {
            console.log("Engine started!");
        }
    };
    console.log(car.make); // Toyota
    car.start(); // Engine started!
    ```
    Arrays and Functions are also special types of objects.

## Operators

*   **Arithmetic**: `+`, `-`, `*`, `/`, `%` (modulo), `**` (exponentiation - ES7).
*   **Assignment**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `**=`.
*   **Comparison**:
    *   `==` (Loose equality, type coercion) - **Avoid using, prefer `===`**
    *   `===` (Strict equality, no type coercion)
    *   `!=` (Loose inequality) - **Avoid using, prefer `!==`**
    *   `!==` (Strict inequality)
    *   `>`, `<`, `>=`, `<=`.
*   **Logical**:
    *   `&&` (Logical AND)
    *   `||` (Logical OR)
    *   `!` (Logical NOT)
*   **Ternary Operator**: `condition ? exprIfTrue : exprIfFalse`
    ```javascript
    let age = 20;
    let type = (age >= 18) ? "adult" : "minor"; // "adult"
    ```
*   **Typeof Operator**: Returns a string indicating the type of the unevaluated operand.
    ```javascript
    console.log(typeof "hello"); // "string"
    console.log(typeof 123);     // "number"
    console.log(typeof true);    // "boolean"
    console.log(typeof {});      // "object"
    console.log(typeof null);    // "object" (historical quirk)
    console.log(typeof undefined); // "undefined"
    console.log(typeof function(){}); // "function"
    ```
*   **Spread Operator (`...`) (ES6)**: Expands iterables (arrays, strings) or object expressions.
    ```javascript
    const arr1 = [1, 2, 3];
    const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]
    const obj1 = { a: 1, b: 2 };
    const obj2 = { ...obj1, c: 3 }; // { a: 1, b: 2, c: 3 }
    function sum(x, y, z) { return x + y + z; }
    const numbers = [1, 2, 3];
    console.log(sum(...numbers)); // 6
    ```
*   **Rest Parameter (`...`) (ES6)**: Collects all remaining arguments into an array.
    ```javascript
    function logArgs(firstArg, ...restArgs) {
        console.log("First:", firstArg); // First: one
        console.log("Rest:", restArgs);  // Rest: ["two", "three"]
    }
    logArgs("one", "two", "three");
    ```
*   **Nullish Coalescing Operator (`??`) (ES2020)**: Returns right-hand operand if left-hand is `null` or `undefined`.
    ```javascript
    let userProvidedName = null;
    let displayName = userProvidedName ?? "Guest"; // "Guest"
    let count = 0;
    let displayCount = count ?? 10; // 0 (because 0 is not null or undefined)
    ```

## Control Flow

*   **If/Else If/Else**:
    ```javascript
    let score = 85;
    if (score >= 90) {
        console.log("Grade A");
    } else if (score >= 80) {
        console.log("Grade B");
    } else {
        console.log("Grade C or lower");
    }
    ```
*   **Switch Statement**:
    ```javascript
    let day = "Monday";
    switch (day) {
        case "Monday":
            console.log("Start of the work week.");
            break;
        case "Friday":
            console.log("TGIF!");
            break;
        default:
            console.log("Another day.");
    }
    ```
*   **For Loop**:
    ```javascript
    for (let i = 0; i < 5; i++) {
        console.log(i); // 0, 1, 2, 3, 4
    }
    ```
*   **While Loop**:
    ```javascript
    let i = 0;
    while (i < 3) {
        console.log(i);
        i++;
    }
    ```
*   **Do...While Loop**:
    ```javascript
    let k = 0;
    do {
        console.log(k);
        k++;
    } while (k < 3);
    ```
*   **For...of Loop (ES6)**: Iterates over iterable objects (Arrays, Strings, Maps, Sets).
    ```javascript
    const colors = ["red", "green", "blue"];
    for (const color of colors) {
        console.log(color);
    }
    const message = "Hi";
    for (const char of message) {
        console.log(char); // H, i
    }
    ```
*   **For...in Loop**: Iterates over the enumerable properties of an object (keys).
    ```javascript
    const student = { name: "Eve", grade: "A", age: 22 };
    for (const key in student) {
        console.log(`${key}: ${student[key]}`);
    }
    ```
*   **Break and Continue**:
    *   `break`: Exits the loop.
    *   `continue`: Skips the current iteration and proceeds to the next.

## Functions

*   **Function Declaration**:
    ```javascript
    function greet(name) {
        return `Hello, ${name}!`;
    }
    console.log(greet("Alice")); // Hello, Alice!
    ```
*   **Function Expression**:
    ```javascript
    const sayGoodbye = function(name) {
        return `Goodbye, ${name}!`;
    };
    console.log(sayGoodbye("Bob")); // Goodbye, Bob!
    ```
*   **Arrow Functions (ES6)**: Concise syntax for functions.
    ```javascript
    // Single parameter, single expression (implicit return)
    const square = x => x * x;
    console.log(square(5)); // 25

    // Multiple parameters
    const add = (a, b) => a + b;
    console.log(add(3, 4)); // 7

    // With function body (explicit return needed if not single expression)
    const complexCalc = (a, b) => {
        const temp = a + b;
        return temp * 2;
    };
    console.log(complexCalc(2,3)); // 10

    // No parameters
    const getRandom = () => Math.random();

    // Arrow functions do not have their own 'this' binding.
    // They inherit 'this' from the surrounding (lexical) scope.
    ```
*   **Default Parameters (ES6)**:
    ```javascript
    function welcome(name = "Guest") {
        console.log(`Welcome, ${name}!`);
    }
    welcome(); // Welcome, Guest!
    welcome("Charlie"); // Welcome, Charlie!
    ```
*   **Immediately Invoked Function Expression (IIFE)**:
    ```javascript
    (function() {
        console.log("This function runs immediately!");
        // Creates a private scope
    })();
    ```

## Arrays

*   **Creating Arrays**:
    ```javascript
    let emptyArr = [];
    let fruits = ["apple", "banana", "cherry"];
    let mixed = [1, "text", true, {objKey: "objVal"}];
    ```
*   **Accessing Elements**:
    ```javascript
    console.log(fruits[0]); // "apple"
    fruits[1] = "blueberry"; // Modify element
    ```
*   **Common Array Methods**:
    *   `length`: Property, not a method.
        ```javascript
        console.log(fruits.length); // 3
        ```
    *   `push()`: Adds element(s) to the end, returns new length.
        ```javascript
        fruits.push("orange"); // ["apple", "blueberry", "cherry", "orange"]
        ```
    *   `pop()`: Removes the last element, returns that element.
        ```javascript
        let lastFruit = fruits.pop(); // "orange"
        ```
    *   `shift()`: Removes the first element, returns that element.
        ```javascript
        let firstFruit = fruits.shift(); // "apple"
        ```
    *   `unshift()`: Adds element(s) to the beginning, returns new length.
        ```javascript
        fruits.unshift("mango"); // ["mango", "blueberry", "cherry"]
        ```
    *   `indexOf()`: Returns the first index of an element, or -1 if not found.
        ```javascript
        console.log(fruits.indexOf("cherry")); // 2
        ```
    *   `includes()` (ES7): Returns `true` if an array contains a certain value, `false` otherwise.
        ```javascript
        console.log(fruits.includes("blueberry")); // true
        ```
    *   `slice(start, end)`: Returns a shallow copy of a portion of an array (end index not included). Does not modify original.
        ```javascript
        let subArray = fruits.slice(1, 3); // ["blueberry", "cherry"]
        ```
    *   `splice(startIndex, deleteCount, ...itemsToAdd)`: Changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
        ```javascript
        let numbers = [10, 20, 30, 40, 50];
        numbers.splice(2, 1, 35); // Removes 1 element at index 2, adds 35. Result: [10, 20, 35, 40, 50]
        numbers.splice(1, 0, 15); // Adds 15 at index 1. Result: [10, 15, 20, 35, 40, 50]
        ```
    *   `forEach(callbackFn(element, index, array))`: Executes a provided function once for each array element.
        ```javascript
        fruits.forEach((fruit, index) => console.log(`${index}: ${fruit}`));
        ```
    *   `map(callbackFn(element, index, array))`: Creates a new array populated with the results of calling a provided function on every element.
        ```javascript
        let nums = [1, 2, 3];
        let doubled = nums.map(num => num * 2); // [2, 4, 6]
        ```
    *   `filter(callbackFn(element, index, array))`: Creates a new array with all elements that pass the test implemented by the provided function.
        ```javascript
        let ages = [15, 22, 18, 30];
        let adults = ages.filter(age => age >= 18); // [22, 18, 30]
        ```
    *   `reduce(callbackFn(accumulator, currentValue, currentIndex, array), initialValue)`: Executes a reducer function on each element, resulting in a single output value.
        ```javascript
        let values = [1, 2, 3, 4];
        let sum = values.reduce((acc, current) => acc + current, 0); // 10
        ```
    *   `find(callbackFn(element, index, array))`: Returns the first element that satisfies the provided testing function. Otherwise `undefined`.
        ```javascript
        let people = [{name: "A", age: 20}, {name: "B", age: 25}];
        let personB = people.find(p => p.name === "B"); // {name: "B", age: 25}
        ```
    *   `findIndex(callbackFn(element, index, array))`: Returns the index of the first element that satisfies the testing function. Otherwise -1.
    *   `some(callbackFn)`: Tests whether at least one element passes the test. Returns boolean.
    *   `every(callbackFn)`: Tests whether all elements pass the test. Returns boolean.
    *   `Array.isArray()`: Checks if a value is an array.
        ```javascript
        console.log(Array.isArray(fruits)); // true
        ```

## Objects

*   **Creating Objects**:
    *   Object Literal:
        ```javascript
        let car = { make: "Honda", model: "Civic", year: 2020 };
        ```
    *   Constructor Function (older way):
        ```javascript
        function Vehicle(make, model) {
            this.make = make;
            this.model = model;
        }
        let myVehicle = new Vehicle("Ford", "Focus");
        ```
    *   ES6 Classes (syntactic sugar over constructor functions):
        ```javascript
        class Animal {
            constructor(name) {
                this.name = name;
            }
            speak() {
                console.log(`${this.name} makes a sound.`);
            }
        }
        let dog = new Animal("Dog");
        dog.speak();
        ```
*   **Accessing Properties**:
    *   Dot notation: `car.make`
    *   Bracket notation (useful for dynamic keys or keys with special characters): `car["model"]`
        ```javascript
        let propName = "year";
        console.log(car[propName]); // 2020
        ```
*   **Adding/Modifying Properties**:
    ```javascript
    car.color = "blue";
    car.year = 2022;
    ```
*   **Deleting Properties**:
    ```javascript
    delete car.year;
    ```
*   **Object Methods**:
    *   `Object.keys(obj)`: Returns an array of an object's own enumerable property names.
    *   `Object.values(obj)`: Returns an array of an object's own enumerable property values.
    *   `Object.entries(obj)`: Returns an array of an object's own enumerable string-keyed property [key, value] pairs.
    *   `Object.assign(target, ...sources)`: Copies all enumerable own properties from one or more source objects to a target object.
    *   `Object.hasOwnProperty(prop)`: Checks if an object has a specified property as its own property.
*   **Destructuring Assignment (ES6)**: Unpack values from arrays or properties from objects into distinct variables.
    ```javascript
    const userProfile = {
        username: "jdoe",
        email: "jdoe@example.com",
        city: "New York"
    };
    const { username, email } = userProfile;
    console.log(username); // "jdoe"

    const rgb = [255, 0, 128];
    const [red, green, blueVal] = rgb;
    console.log(red); // 255
    ```

## DOM Manipulation (Browser Environment)

The Document Object Model (DOM) represents the HTML structure of a web page.

*   **Selecting Elements**:
    *   `document.getElementById('elementId')`
    *   `document.getElementsByClassName('className')` (returns HTMLCollection)
    *   `document.getElementsByTagName('tagName')` (returns HTMLCollection)
    *   `document.querySelector('cssSelector')` (returns the first matching element)
    *   `document.querySelectorAll('cssSelector')` (returns a NodeList of all matching elements)
    ```javascript
    const mainTitle = document.getElementById('main-title');
    const buttons = document.querySelectorAll('.btn');
    ```
*   **Modifying Element Content**:
    *   `element.textContent`: Get or set the text content.
    *   `element.innerHTML`: Get or set the HTML content (use with caution due to XSS risks if content is user-provided).
    ```javascript
    if (mainTitle) {
        mainTitle.textContent = "New Page Title";
    }
    ```
*   **Modifying Element Attributes**:
    *   `element.getAttribute('attributeName')`
    *   `element.setAttribute('attributeName', 'value')`
    *   `element.removeAttribute('attributeName')`
    *   Direct property access for common attributes: `element.id`, `element.src`, `element.href`.
    ```javascript
    const myImage = document.querySelector('img');
    if (myImage) {
        myImage.setAttribute('src', 'new_image.jpg');
        myImage.alt = "A new descriptive image"; // Direct property
    }
    ```
*   **Modifying Element Styles**:
    *   `element.style.property = 'value'` (e.g., `element.style.color = 'red'`)
    *   `element.classList.add('className')`
    *   `element.classList.remove('className')`
    *   `element.classList.toggle('className')`
    *   `element.classList.contains('className')`
    ```javascript
    const infoBox = document.querySelector('.info');
    if (infoBox) {
        infoBox.style.backgroundColor = 'lightyellow';
        infoBox.classList.add('highlight');
    }
    ```
*   **Creating and Adding Elements**:
    ```javascript
    const newParagraph = document.createElement('p');
    newParagraph.textContent = "This is a new paragraph.";
    const container = document.getElementById('content-area');
    if (container) {
        container.appendChild(newParagraph); // Adds as the last child
        // container.prepend(newParagraph); // Adds as the first child
    }
    ```
*   **Removing Elements**:
    ```javascript
    const oldElement = document.getElementById('to-remove');
    if (oldElement) {
        oldElement.remove(); // Modern way
        // oldElement.parentNode.removeChild(oldElement); // Older way
    }
    ```
*   **Event Handling**:
    ```javascript
    const myButton = document.getElementById('myBtn');
    if (myButton) {
        myButton.addEventListener('click', function(event) {
            console.log('Button clicked!');
            console.log(event.target); // The button element
            // event.preventDefault(); // If it's a form submit or link
        });

        // Using an arrow function
        // myButton.addEventListener('mouseover', () => {
        //    console.log('Mouse is over the button!');
        // });
    }
    ```

## ES6+ Features (Recap and More)

*   **`let` and `const`**: Block-scoped variables.
*   **Arrow Functions**: Concise function syntax, lexical `this`.
*   **Template Literals**: Multi-line strings and string interpolation with `${expression}`.
*   **Destructuring Assignment**: For arrays and objects.
*   **Default Parameters**: For function arguments.
*   **Rest Parameter (`...args`)**: Collects remaining function arguments.
*   **Spread Operator (`...iterable`)**: Expands iterables.
*   **Classes**: Syntactic sugar for constructor functions and prototypes.
    ```javascript
    class Rectangle {
        constructor(height, width) {
            this.height = height;
            this.width = width;
        }
        get area() { // Getter
            return this.calcArea();
        }
        calcArea() {
            return this.height * this.width;
        }
        static defaultRectangle() { // Static method
            return new Rectangle(10, 10);
        }
    }
    const rect = new Rectangle(10, 20);
    console.log(rect.area); // 200 (accessing getter)
    const defaultRect = Rectangle.defaultRectangle();
    console.log(defaultRect.area); // 100
    ```
*   **Modules (Import/Export)**: Organize code into reusable pieces.
    ```javascript
    // lib.js
    // export const PI = 3.14;
    // export function calculateCircumference(radius) { return 2 * PI * radius; }
    // export default function greetUser(name) { return `Hello, ${name}`; }

    // main.js
    // import greetUser, { PI, calculateCircumference } from './lib.js';
    // console.log(PI);
    // console.log(calculateCircumference(5));
    // console.log(greetUser("Dev"));
    ```
    *Note: Module usage in browsers often requires `<script type="module" src="main.js"></script>` or a bundler like Webpack/Parcel.*
*   **Promises**: For asynchronous operations (alternative to callbacks).
    ```javascript
    const fetchData = () => {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                const success = Math.random() > 0.3; // Simulate success/failure
                if (success) {
                    resolve({ data: "Sample data from server" });
                } else {
                    reject(new Error("Failed to fetch data."));
                }
            }, 1000);
        });
    };

    fetchData()
        .then(response => {
            console.log("Success:", response.data);
        })
        .catch(error => {
            console.error("Error:", error.message);
        })
        .finally(() => {
            console.log("Fetch attempt finished.");
        });
    ```
*   **Async/Await (ES2017)**: Syntactic sugar over Promises, makes async code look more synchronous.
    ```javascript
    async function getData() {
        try {
            console.log("Fetching data...");
            const response = await fetchData(); // Pauses here until promise settles
            console.log("Async Success:", response.data);
            return response.data;
        } catch (error) {
            console.error("Async Error:", error.message);
            throw error; // Re-throw if needed
        } finally {
            console.log("Async fetch attempt finished.");
        }
    }
    getData().then(data => console.log("Data received by caller:", data)).catch(err => {});
    ```
*   **Map and Set (ES6)**:
    *   `Map`: Ordered collection of key-value pairs where keys can be any type.
    *   `Set`: Collection of unique values.

This provides a comprehensive JavaScript cheatsheet with ES6+ features. I'll proceed with `typescript.md`.The `javascript.md` cheatsheet has been successfully enhanced with detailed syntax examples, code snippets for data types, operators, control flow, functions (including arrow functions), arrays, objects, DOM manipulation, and key ES6+ features like Promises and Async/Await.

Next, I will enhance `typescript.md`, focusing on its type system, interfaces, classes, generics, and how it builds upon JavaScript.
