# Basics

**Variable Declaration**

1. "let": Variables that will change during runtime

```javascript
let first_name = "Jonas";
first_name = 'Hello';
```

2. "var": Variables that will change during runtime

* Old way to declare variables
* Completely avoid if possible

```javascript
var job = "programmer";
job = "teacher"
```

3. "const": Variables that cannot change during runtime

* Cannot be declared undefined
* Use by default, unless prior knowledge that it will change

```javascript
const birth = 1991;
//Invalid assignment below
birth = 1990
```



**Primitive Data Types**

* Dynamic typing: Variable is not assigned a data type. Value determines the data type.

1. Number
   * Used for both decimals and integers
2. String
   * Single or Double quotes
3. Boolean
   1. true
   2. false: 0, "", undefined, NaN, null
4. null
5. Undefined



**Comment**

* Single line comment

```
// Some code
```

* For multi-line comment

```
/* hello
  world
  */
```



**Operators**

* Math
  * \+
  * \-
  * /&#x20;
  * \*
  * \*\*
  * %
* Comparison
  * \>
  * <
  * \=== : equals strictly, comparison must be same data types
  * \== : equals loosely, when comparison involve different data types
  * !==: strict
  * !=: loose
* Logical
  * &&
  * ||
  * !
*   Assignment

    * \=
    * \+=
    * \++



**String Concatenation**

* Use +
* Use \`\`: Template strings or multi line strings

```javascript
const firstName = "YJ";
const age = 49;
console.log(`I'm ${firstName}, my age is ${age}`);
```

```javascript
console.log(`String
with
lines`)
```



**Type conversion and coercion**

Conversion: Explicitly done

```javascript
const inputYear = "1991";
//Convert to number data type
console.log(Number(inputYear) + 19);

//Convert to string data type
console.log(String(23))
```

Coercion: Implicitly done

```javascript
const age = 23
console.log("I am " + age + " years old.");
```



**Control Flow**

* if, else if, else statements
* switch statements
* For loops

```javascript
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

* for each loops
* while loops



**Strict mode**

* Prevents use of reserved keywords
* Identify potential errors in code

```javascript
//Use this at the top of the code
'use strict';
```



