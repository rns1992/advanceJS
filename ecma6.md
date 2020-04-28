### Advanced JavaScript

- In computer science, scope is the region of a computer program where the binding or association of a name to an entity, such as a variable or function, is valid. JavaScript has the following two distinct types of scope:
  - Function scope
  - Block scope

-	Until ES6 there was only function scope, but later block scope was also introduced with keyword let and const.

#### FUNCTION SCOPE

- Function scope in JavaScript is created inside functions. When a function is declared, a new scope block is created inside the body of that function. Variables that are declared inside the new function scope cannot be accessed from the parent scope; however, the function scope has access to variables in the parent scope.
```
var example = 5;

function test() {

  var testVariable = 10;

  console.log( example ); // Expect output: 5

  console.log( testVariable ); // Expect output: 10

}

test();

console.log( testVariable ); // Expect reference error
```


### Function Scope Hoisting

- When a variable is created with function scope, it's declaration automatically gets hoisted to the top of the scope.
- Hoisting means that the interpreter moves the instantiation of an entity to the top of the scope it was declared in, regardless of where in the scope block it is defined. Functions and variables declared using var are hoisted in JavaScript; that is, a function or a variable can be used before it has been declared.

```
example = 5; // Assign value

console.log( example ); // Expect output: 5

var example; // Declare variable
```

- Since a hoisted variable that's been declared with var can  be used before it is declared, we have to be careful to not use that variable before it has been assigned a value. If a variable is accessed before it has been assigned a value, it will return the value as undefined, which can cause problems, especially if variables are used in the global scope.

- For variables
```
var name = "Baggins";

(function () {
	// Output: "Original name was : undefined"
	console.log("Original name was : " + name);

	var name = "Underhill";

	console.log("New name is " + name);
})();
```
- Function definition hoisting only occurs for function declarations, not function expressions. For example,

```
// Outputs: "Definition hoisted!"
definitionHoisted();

// TypeError: undefined is not a function
definitionNotHoisted();

function definitionHoisted() {
	console.log("Definition hoisted!");
}

var definitionNotHoisted() = function() {
	console.log("Definition not hoisted");
}
```


#### Block Scope

- A new block scope in JavaScript is created with curly braces ({}). A pair of curly braces can be placed anywhere in the code to define a new scope block. If statements, loops, functions, and any other curly brace pairs will have their own block scope. This includes floating curly brace pairs not associated with a keyword (if, for, etc). 
```
// Top level scope

function scopeExample() {

  // Scope block 1

  for ( let i = 0; i < 10; i++ ){ /* Scope block 2 */ }

  if ( true ) { /* Scope block 3 */ } else { /* Scope block 4 */ }

  // Braces without keywords create scope blocks

  { /* Scope block 5 */ }

  // Scope block 1

}

// Top level scope
```
- Variables declared with the keywords let and const have block scope. When a variable is declared with block scope, it does NOT have the same variable hoisting as variables that are created in function scope. Block scoped variables are not hoisted to the top of the scope and therefore cannot be accessed until they are declared. This means that variables that are created with block scope are subject to the Temporal Dead Zone (TDZ). The TDZ is the period between when a scope is entered and when a variable is declared.

```
{
	// Output: 5
	console.log(example);

	var example = 5;
	
	//Output:Uncaught ReferenceError: Cannot access 'test' before initialization
	console.log(test);

	let test;
}
```

- If a variable is accessed inside the Temporal Dead Zone, then a runtime error will be thrown.
- Basic JavaScript uses the keyword var for variable declaration. ECMAScript 6 introduced two new keywords to declare variables; they are let and const.

|  | Function Scope | Block Scope |
| - | - | - |
| Scope Creation | Block of scope for each function | Block of scope for curly braces {} |
| Variable Keyword | Variables defined with var | Variables defined with let and const |
| Hoisting and Instation | Variable hoisting | Temporal Dead Zone |


| - | Var | Let | Const |
| - | - | - | - |
| Scope Creation | Function Scope | Block scope | Block Scope |
| Reassignment | Can be reassigned | Can be reassigned | Can be reassigned |
| Hoisting | Hoisted | Hoisted | Hoisted |

#### Introducing Arrow Functions

- A way to create functions in ECMA Script 6. It is used in callback chains, promise chains, array methods, in any situation where unregistered functions would be useful.
- The key difference between arrow functions and normal functions in JavaScript is that arrow functions are anonymous. Arrow functions are not named and not bound to an identifier. This means that an arrow function is created dynamically and is not given a name like normal functions. Arrow functions can however be assigned to a variable to allow for reuse.

- Example.

```
const fn2 = ( a, b ) => { return a + b; };

( ) => { /* Do function stuff here */ }

arg1 => { /* Do function stuff here */ }

( arg1 = 10 ) => { /* Do function stuff here */ }

( arg1, arg2 ) => { 			 
	console.log( `This is arg1: ${arg1}` );			  
 	console.log( `This is arg2: ${arg2}` );			  
	/* Many more lines of code can go here */			
}

( num1, num2 ) => { return ( num1 + num2 ) }

( num1, num2 ) => num1 + num2

( numArray ) => numArray.filter( n => n > 5).map( n => n - 1 ).every( n => n < 10 )
```

#### Template Literals

- Template literals are a new form of string that was introduced in ECMAScript 6. They are enclosed by the backtick symbol (``) instead of the usual single or double quotes. 
- Template literals allow you to embed expressions in the string that are evaluated at runtime. Thus, we can easily create dynamic strings from variables and variable expressions. These expressions are denoted with the dollar sign and curly braces (${ expression }). The template literal syntax is shown in the following code:
```
const example = "pretty";

console.log( `Template literals are ${ example } useful!!!` );

// Expected output: Template literals are pretty useful!!!
```

- A more advanced form of template literals are tagged template literals. Tagged template literals can be parsed with a special function called tag functions, and can return a manipulated string or any other value.

```
// Define the tag function

function tagFunction( strings, numExp, fruitExp ) {

  const str0 = strings[0]; // "We have"

  const str1 = strings[1]; // " of "

  const quantity = numExp < 10 ? 'very few' : 'a lot';

  return str0 + quantity + str1 + fruitExp + str2;

}

const fruit = 'apple', num = 8;

// Note: lack of parenthesis or whitespace when calling tag function

const output = tagFunction`We have ${num} of ${fruit}. Exciting!`

console.log( output )

// Expected output: We have very few of apples. Exciting!!
```

- When object is passed in to a function then its properties are evaluated inside the functions expression.
```
function parseHouse( property ) {

 return `${property.owner} is selling the property at ${property.address} for ${property.price} USD`

}

const house = {

 address: "123 Main St, San Francisco CA, USA",

 floors: 2,

 price: 5000000,

 owner: "John Doe"

};

console.log( parseHouse( house ) );
```
