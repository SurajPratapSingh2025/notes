## Table of Contents

[JavaScript Concept](#javascript-concept)

[JavaScript Core](#javascript-core)

  1. [Lexical Structure](#lexical-structure)
  2. [Types, Values, and Variables](#types-values-and-variables)
  3. [Expressions and Operators](#expressions-and-operators)
  4. [Statements](#statements)
  5. [Objects](#objects)
  6. [Arrays](#arrays)
  7. [Functions](#functions)

[Reference Information](#reference-information)

<br />

## JavaScript Concept

* JavaScript was created in 1995 by [Brendan Eich](https://twitter.com/BrendanEich) while working at Netscape

* ECMAScript is the standardized name for JavaScript

<br />

## JavaScript Core

<a name="lexical-structure"></a>
### Lexical Structure

  * JavaScript programs should be written using the Unicode character set (ES5 requires implementations to support Unicode 3 and later)

  * JavaScript is case-sensitive, so "keywords, variables, function names, and identifiers" must maintain consistent casing

  * **Literal**: A data value that appears directly in program code

    Examples:
    ```javascript
    12                  // The number 12
    1.2                 // The number 1.2
    "hello world"       // A string
    {x:1, y:2}          // Object initializer
    [1, 2, 3, 4, 5]     // Array initializer
    ```

  * **Identifier**: A name used to identify "variables, functions, or labels in loops". Must start with "a letter, underscore, or dollar sign", followed by "letters, digits, underscores, or dollar signs"

  * **Reserved words**: Cannot be used as identifiers

    Examples:
    ```javascript
    break, class, var, or int
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="types-values-and-variables"></a>
### Types, Values, and Variables

  * JavaScript types are divided into two categories: primitive types and object types

  * **Primitive types**: numbers, strings, booleans, null, undefined

  * **Object types**: Anything that's not a primitive type is an object type

  * JavaScript variables are untyped, use lexical scoping, and are declared with `var`

  * All numbers in JavaScript are represented as floating-point values (not integers). **Be aware of potential precision errors in calculations**

  * When a numeric operation results in a value larger than the maximum representable number, the result is the special infinity value `Infinity`

  * Dividing zero by zero results in `NaN` (not-a-number)

  * **String literals**: Enclose string characters in matching single or double quotes

    Examples:
    ```javascript
    ""            // Empty string
    'testing'
    "3.14"
    ```

  * **Escape sequences in string literals**: Used to represent characters that can't be directly represented, using `\`

    Example:
    ```javascript
    'You\'re right, it can\'t be a quote'
    ```

  * **String concatenation**: The `+` operator joins strings together

    Example:
    ```javascript
    msg = 'Hello, ' + 'World';     // => 'Hello, World'
    ```

  * **null**: Represents the absence of a value

  * **undefined**: Occurs in these situations: uninitialized variables, accessing non-existent object properties or array elements, functions with no return value, function parameters with no corresponding arguments

  * **Global object**: When the JavaScript interpreter starts or when a browser loads a new page, it creates a global object with these initial properties:

    * undefined, Infinity, NaN

    * isNaN(), parseInt(), eval()

    * Constructor functions like Date(), RegExp(), String(), Object()

    * Global objects like Math and JSON

  * **The `this` keyword**: Not a constant - its value changes depending on where it appears in the code

    > Unlike variables, the `this` keyword doesn't have scope

    - At the **top-level** (code not inside any function): `this` refers to the global object

    - Function invocation: `this` refers to the global object (or `undefined` in strict mode)

    - Method invocation: `this` refers to the object the method belongs to

    Example:
    ```javascript
    var obj = {
      m: function() {
        var self = this;
        console.log(this === obj);       // => true
        
        func();
        
        function func() {
          console.log(this === obj);     // => false, `this` is global object or undefined
          console.log(self === obj);     // => true, `self` is outer `this`
        }
      }
    };
    obj.m();
    ```

  * **Wrapper objects**: When you refer to a property of a string, number, or boolean, JavaScript converts it to a temporary object. This object inherits properties from the corresponding prototype. After the property reference, the temporary object is discarded. **null and undefined** don't have wrapper objects. **These object properties are read-only and you can't define new properties**

  * **Primitive types**: Compared by value, values are immutable. Two values are equal if they contain the same value

    Example:
    ```javascript
    var s = 'hello';     // Create a lowercase string
    s.toUpperCase();     // Returns 'HELLO' but doesn't modify s
    s                    // => 'hello': original string unchanged
    ```

  * **Object types**: Compared by reference, values are mutable. Two objects with identical properties are not equal unless they refer to the same object

    Example:
    ```javascript
    var a = [];          // Variable a references an empty array
    var b = a;           // Now b references the same array
    b[0] = 1;            // Modify the array through b
    a[0]                 // => 1: The change is visible through a
    a === b              // => true: a and b reference the same object
    ```

  * **Explicit type conversion**: Use conversion functions

    Examples:
    ```javascript
    Number('3')       // => 3
    String(false)     // => 'false'
    Boolean([])       // => true
    Object(3)        // => new Number(3)
    ```

  * **Variable declaration**: Use `var`. You can declare multiple variables with one `var` keyword and initialize them. Undeclared variables have the value `undefined`

    Example:
    ```javascript
    var i, sum;
    var x = 0, y = 1, z = 2;
    ```

    > Automatically global: If you assign a value to a variable that hasn't been declared, it automatically becomes a global variable, even if the assignment is inside a function.

    > Global variables are not created automatically in "Strict Mode".

  * **Variable scope**: Variables declared at the top-level are global. Variables declared in a function body are local. Function parameters are also local variables.

  * **Variable precedence**: Local variables take precedence over global variables with the same name

    Example:
    ```javascript
    var scope = 'global';        // Declare global variable
    
    function checkScope() {
      var scope = 'local';       // Declare local variable with same name
      return scope;              // Return local variable's value
    }
    
    checkScope();                // => 'local'
    ```

  * **Function scope**: Variables are visible within the function they're defined in and any nested functions

    > Each function creates a new scope.

  * **Global variables**:
    - A variable declared outside a function becomes global.
    - A global variable has global scope: All scripts and functions can access it.
    > When you declare a global variable, you're actually defining a property of the global object
    > In HTML, the global scope is the window object. All global variables belong to the window object.

  * **Local variables**:
    - Variables declared within a JavaScript function become local to the function.
    - Local variables have local scope: They can only be accessed within the function.

  * **Variable lifetime**:
    - Starts when declared.
    - Local variables are deleted when the function completes.
    - In browsers, global variables are deleted when you close the window/tab.

  * **Hoisting**: `var` declarations and `function` declarations are "hoisted" to the top of their scope
    - Declarations are processed before any code executes.
    - JavaScript only hoists declarations, not initializations.
    - For function declarations, both the name and function body are hoisted.

    Examples:
    ```javascript
    // Function declaration hoisting
    foo();
    function foo() {}  // This function is hoisted
    
    // Actual execution:
    function foo() {}
    foo();
    
    // Variable declaration hoisting
    foo();
    var foo = function() {};
    
    // Actual execution:
    var foo;
    foo();     // TypeError: undefined is not a function
    foo = function() {};
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="expressions-and-operators"></a>
### Expressions and Operators

  * **Expression**: Something the interpreter can evaluate to produce a value

  * **Operators**: Most operators are represented by punctuation. They have precedence and associativity.

  * **Operands**: The elements that operators evaluate

    Examples:
    ```javascript
    1 + 2;          // => 3; + is operator, 1 and 2 are operands
    11 < 3;         // => true
    delete o.x;     // Delete property x of object o
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="statements"></a>
### Statements

  * **Conditional statements**: `if`, `else if`, `switch`

    Examples:
    ```javascript
    // if statement
    if (username === null) {
      username = 'Justin Ho';
    } else {
      console.log(username);
    }
    
    // else if statement
    if (x === 1) {
      // Execute block 1
    } else if (x === 2) {
      // Execute block 2
    } else if (x === 3) {
      // Execute block 3
    } else {
      // Execute block 4 if no conditions match
    }
    
    // switch statement
    /* Case matching uses === identity operator
     * ECMAScript allows any expression after case
     * If no case matches and no default, skip entire switch body
     */
    switch (x) {
      case 'number':     // If x equals 'number'
        // Execute block 1
        break;
      case 'string':
        // Execute block 2
        break;
      default:           // If no matches
        // Execute block 3
        break;           // Stop execution
    }
    ```

  * **Loop statements**: `while`, `do/while`, `for`, `for/in`

    Examples:
    ```javascript
    // while statement
    var count = 0;
    while (count < 10) {
      console.log(count);
      count++;
    }
    
    // do/while statement
    var array = [1, 2, 3];
    var len = array.length, i = 0;
    do {
      console.log(array[i]);
    } while (++i < len);
    
    // for statement
    for (var count = 0; count < 10; count++) {
      console.log(count);
    }
    
    // for/in statement
    /* Only enumerable properties are listed
     */
    for (var p in o) {         // Assign property names of o to p
      console.log(o[p]);       // Print each property value
    }
    ```

  * **Labeled statements**: Add a label to a statement for reference elsewhere. Label names can be any legal identifier (not reserved words). Label names are in a different namespace from variables and functions.

    Example:
    ```javascript
    mainloop: while (token != null) {
      // Code omitted...
      continue mainloop;     // Jump to next iteration of named loop
      // More code omitted...
    }
    ```

  * **Jump statements**: `break`, `continue`, `return`, `try/catch/finally`

    Examples:
    ```javascript
    // break statement
    for (var i = 0; i < a.length; i++) {
      if (a[i] == target) {
        break;     // Immediately terminate innermost loop
      }
    }
    
    // continue statement
    for (i = 0; i < data.length; i++) {
      if (!data[i]) {
        continue;     // Start next iteration
      }
      total += data[i];
    }
    
    // return statement
    function square(x) {
      return x*x;     // Return value to caller
    }
    
    // try/catch/finally statement
    /* When exception is thrown, interpreter stops normal execution
     * and jumps to nearest exception handler (catch block)
     * try: Defines code block to test for errors
     * catch: Executes if try block throws exception
     * finally: Executes regardless of try block outcome
     * At least one of catch/finally must accompany try
     */
    try {
      // Code to try
    } catch (exception) {     // exception has block scope
      // Handle exceptions
    } finally {
      // Executes when try block ends:
      // 1) Normally reaches end
      // 2) Due to break/continue/return
      // 3) Exception caught by catch
      // 4) Uncaught exception propagating
    }
    ```

  * 'use strict': Indicates that following code is strict code. If a function body is defined in strict code, that function is also strict.

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="objects"></a>
### Objects

  * Objects are collections of properties

  * Each property has associated property attributes:
    * writable: Can the value be changed?
    * enumerable: Can the property be returned by for/in?
    * configurable: Can the property be deleted or its attributes modified?

  * Each object has associated object attributes:
    * prototype: Reference to inherited object
    * class: String identifying object type
    * extensible: Can new properties be added?

  * Create objects using: object literals, `new` keyword, or `Object.create()`
    - The `new` keyword must be followed by a function call (constructor)
    > Besides built-in constructors (Object, Date, RegExp), you can define your own

    Examples:
    ```javascript
    // Object literal
    var empty = {};
    var point = {x:0, y:0};
    var point2 = {x: point.x, y:point.y+1};
    var book = {
      "main title": "JavaScript",
      'sub-title': "The Definitive Guide",
      "for": "all audiences",
      author: {
        firstname: "David",
        surname: "Flanagan"
      }
    };
    
    // new keyword
    var o = new Object();         // Empty object, same as {}
    var a = new Array();          // Empty array, same as []
    var d = new Date();           // Date object for current time
    var r = new RegExp("js");     // RegExp object for pattern matching
    
    // Object.create()
    var o1 = Object.create({x:1, y:2});     // o1 inherits x and y
    var o2 = Object.create(null);           // o2 inherits nothing
    ```

  * Every object has a prototype object from which it inherits properties

  * **Prototype chain**: The inheritance relationship between objects

  * Objects created with object literals have the same prototype object: `Object.prototype`

  * Objects created with `new` and constructor functions have the constructor's `prototype` property as their prototype
    > Objects created with `new Object()` inherit from `Object.prototype` (same as `{}`)
    > Objects created with `new Date()` have `Date.prototype` as prototype

  * `Object.create()` can create objects with specified prototypes or no prototype

  * Access properties using `.` or `[]` operators

    Examples:
    ```javascript
    // Get
    var author = book.author;
    var name = author.surname;
    var title = book['main title']
    
    // Set
    book.edition = 6;
    book['main title'] = 'ECMAScript';
    book['Hello' + 'World'] = 'helloworld';
    ```

  * If an inherited property x exists, adding an own property x shadows (overrides) the inherited property

  * Property assignment checks the prototype chain to determine if allowed. If allowed, it creates/sets the property on the original object, never modifying prototype chain objects

  * Inheritance happens when querying properties, not when setting them. You can't modify prototype properties through inheritance

  * Delete properties with `delete` operator. Only works on own properties, and won't delete non-configurable properties

    Examples:
    ```javascript
    delete book.author;
    delete book['main title'];
    ```

  * Check property attributes with `Object.getOwnPropertyDescriptor()`

    Example:
    ```javascript
    var o = {x:1, y:2, z:3};
    console.log(Object.getOwnPropertyDescriptor(o, 'y'));
    /* Returns:
     * {
     *   configurable: true,
     *   enumerable: true,
     *   value: 2,
     *   writable: true
     * }
     */
    ```

  * Set property attributes with `Object.defineProperty()`

    Example:
    ```javascript
    var o = {};
    Object.defineProperty(o, 'x', {
      value: 1,
      writable: true,
      enumerable: false,
      configurable: true
    });
    o.x;     // => 1
    ```

  * Set multiple properties with `Object.defineProperties()`

  * Enumerate object properties:
    - Own properties: `Object.getOwnPropertyNames(object)` (includes non-enumerable)
    - Inherited properties: `for-in` loop (enumerable properties only)

  * Get/set object attributes:
    - Prototype:
      - Get: `Object.getPrototypeOf(object)`
      - Set: `Object.setPrototypeOf(object, prototype)`
    - Class:
      - Get: `Object.prototype.toString.call(object).slice(8, -1)` (only indirect way)
      - Set: Not possible
    - Extensible:
      > All built-in and user-defined objects are extensible by default
      - Get: `Object.isExtensible(object)`
      - Set: `Object.preventExtensions(object)` (makes object non-extensible)

  * **Object serialization**: Convert objects to strings and back

    Example:
    ```javascript
    var o = {x:1, y:{z:[false, null, '']}};     // Define object
    var s = JSON.stringify(o);                  // Serialize to string
    var p = JSON.parse(s);                      // Deserialize back to object
    console.log(p.y.z[0]);                      // => false
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="arrays"></a>
### Arrays

  * Array elements can be any type, and different elements can have different types

  * Create arrays with `[]` or `new Array()`. **Array literals allow trailing commas**

    Examples:
    ```javascript
    var empty = [];                    // Empty array
    var primes = [2, 3, 5, 7, 11];     // Array with 5 numbers
    var misc = [1.1, true, 'a',];      // 3 elements + trailing comma
    
    var base = 1024;
    var table = [base, base+1, base+2, base+3];
    
    var count = [1,,3];     // count[1] => undefined
    var undefs = [,,];      // Sparse array
    
    var a = new Array();                          // Same as []
    var a = new Array(10);                        // Specify length
    var a = new Array(5, 4, 3, 2, 1, 'test');     // 6-element array
    ```

  * Read/write array elements with `[]`

    Example:
    ```javascript
    var a = ['world'];          // Single-element array
    var value = a[0];           // Read element 0
    a[1] = 3.14;                // Write element 1
    
    var i = 2;
    a[i+1] = 'hello';           // Write element 3
    ```

  * `forEach()`: Iterates through all elements. First argument is a function called with three arguments. Cannot use `break` to terminate.

    - First argument: array element value
    - Second argument: array index
    - Third argument: array itself

    Example:
    ```javascript
    var data = [1, 2, 3, 4, 5];
    data.forEach(function(value, index, array) {
      array[index] = value + 1;
    });
    console.log(data);     // => [2, 3, 4, 5, 6]
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="functions"></a>
### Functions

  * **Function**: A block of JavaScript code defined once but can be invoked multiple times

  * When assigned to an object property, it's called a method

  * Function declaration with `function`

    Example:
    ```javascript
    function distance(x1, y1, x2, y2) {          // distance is function name, () contains parameters
      var dx = x2 - x1;
      var dy = y2 - y1;
      return Math.sqrt(dx*dx + dy*dy);           // Return value with return
    }
    ```

  * Function declarations actually declare a variable and assign the function object to it. Function expressions don't declare variables.

  * Function expressions can omit the function name

    Examples:
    ```javascript
    var x = 10;
    var square = function(x) {return x*x;};
    console.log(square(x));                                 // => 100
    
    data.sort(function(a,b) {return a-b;});                // Function expressions as arguments
    
    var tensquared = (function(x) {return x*x}(10));       // Immediately invoked function expression
    ```

  * Invoke functions four ways: "as functions", "as methods", "as constructors", and "indirectly"
    - Invocation context:
      - Function invocation: In ES3 and non-strict ES5, context is global object. In strict mode, it's `undefined`
      - Method invocation: The object the method belongs to is the context (referenced with `this`)
      - Constructor invocation: Creates new object which becomes context (referenced with `this`)
      - Indirect invocation: First argument of call()/apply() specifies context

    Examples:
    ```javascript
    // Function invocation
    printprops(10, 5);
    
    // Method invocation
    o.printprops(10, 5);
    
    // Constructor invocation
    var o = new Object();
    var o = new Object;
    
    // Indirect invocation
    f.call(o);           // Invoke f() as method of o
    f.apply(o);
    f.call(o, 1, 2);     // First arg is context, rest are function arguments
    ```

  * Function invocation doesn't check argument types or count

  * Fewer arguments than parameters: Extra parameters set to undefined

  * More arguments than parameters: Access extras via `arguments`

  * `arguments` is array-like object

    Example:
    ```javascript
    function f(x, y, z) {
      console.log(arguments[0]);         // arguments[0] is same as x
      console.log(arguments[1]);         // arguments[1] is same as y
      console.log(arguments[2]);         // arguments[2] is same as z
      console.log(arguments.length);     // => 3 (if called with 3 args)
    }
    ```

  * Functions are not just syntax - they're values

    Example:
    ```javascript
    function square(x) {return x*x;}             // Define function
    var s = square;                              // s and square reference same function
    square(4);                                   // => 16
    s(4);                                        // => 16
    
    var a = [function(x) {return x*x;}, 20];     // Array literal
    a[0](a[1]);                                  // => 400
    ```

  * Functions are specialized objects and can have properties

    Example:
    ```javascript
    uniqueInteger.counter = 0;            // Initialize counter property
    function uniqueInteger() {
      return uniqueInteger.counter++;     // Return and increment counter
    }
    ```

  * Parameter passing: Call by sharing - copies reference to new reference. Modifications affect original, assignments create new references.

    Example:
    ```javascript
    var arr1 = [1,2,3];
    var arr2 = arr1;       // arr1 and arr2 point to same reference
    arr2 = [4,5,6];        // Create new Array, assign to arr2
    console.log(arr1);     // => [1, 2, 3]
    ```

  * Each function has a prototype property referencing a prototype object. When creating objects with `new`, this prototype is used for inheritance.

  * `call()`, `apply()`: For indirect invocation, allowing methods to be called on objects that don't originally have them, specifying execution context.

    - `call(thisArg, arg1, arg2)`: First arg is context, rest are function arguments
    - `apply(thisArg, [argsArray])`: First arg is context, second is array of arguments

    Example:
    ```javascript
    var obj1 = {
      getName: function() {
        return this.name;
      }
    };
    var obj2 = {                              // obj2 has no getName()
      name: 'Justin'
    };
    console.log(obj1.getName.call(obj2));     // => 'Justin', obj2 indirectly calls obj1's method
    ```

  * `bind()`: Binds a function to an object

    Example:
    ```javascript
    function f(y) { return this.x + y; }     // Function to bind
    var o = { x: 1 };                        // Object to bind to
    var g = f.bind(o);                       // Calling g(x) invokes o.f(x)
    g(2);                                    // => 3
    ```

  * **Callback**: A function passed as an argument to another function to be executed later

    Example:
    ```javascript
    var func = function() {
      console.log('Hello World');
    };
    window.addEventListener('load', func, false);     // => 'Hello World' when load event triggers
    ```

  * **Closure**: A function that has access to the parent scope, even after the parent function has closed.
    - Enables "private" variables.
    - Closures capture the bindings of local variables (and parameters) from their outer function's scope.

    Example:
    ```javascript
    var scope = 'global scope';
    function checkScope() {
      var scope = 'local scope';
      function func() {
        return console.log(scope);
      }
      return func;
    }
    checkScope()();    // => 'local scope', func() is a closure
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

## Reference Information

JavaScript: The Definitive Guide, 6E Traditional Chinese (Author: David Flanagan)

Speaking JavaScript, Traditional Chinese (Author: Dr. Axel Rauschmayer)

JavaScript — call-by-sharing (Author: Avinash Kondeti)
  - https://medium.com/wwstay-engineering/javascript-call-by-sharing-2d3ca42c4d02#.ms38pikzt

Introduction to JavaScript Parameter Passing (Author: Tommy Lin)
  - http://www.slideshare.net/YiTaiLin/java-script-63031051

<br />
