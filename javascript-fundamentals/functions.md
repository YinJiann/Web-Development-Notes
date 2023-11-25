# Functions

**Function Declaration**

* No type declaration for parameters
* No type declaration for return type
* Function can be called before declaration

```javascript
function function_name(param1, param2) {
    //write code
    return variable;
}
```



**Function Expression**

* Functions without a function name can be assigned to a const variable instead
* Function cannot be called before expression

```javascript
const function_name = function (param1, param2) {
    return variable;
}
```



**Arrow Function**

* Has no "this" keyword
* Use case: when calling a function in a function, so that it can use parent's scope (this)

```javascript
const function_name = (param1, param2) => {
    //write code
    return variable;
}
```



**Function Call**

```javascript
function_name(argument1, argument2);
```



#### Default parameters

```javascript
function_name(argument1 = 1, argument2 = 2);
```



#### Higher order functions (IMPORTANT)

* Functions that receives another function as argument or returns a new function
* Use case for callback functions: abstraction

```javascript
const greet = () => console.log("hi");

//addEventListener = higher-order function
//greet = callback function. Value is passed in, function is not called
btn.addEventListener.("click", greet);
```

```javascript
// Functions Returning Functions
const greet = function (greeting) {
  return function (name) {
    console.log(`${greeting} ${name}`);
  };
};

const greeterHey = greet('Hey');
greeterHey('Jonas');
greeterHey('Steven');

greet('Hello')('Jonas');
```



#### Call method

* Pass context for "this" keyword when doing normal function call

```javascript
const lufthansa = {
  airline: 'Lufthansa',
  iataCode: 'LH',
  bookings: [],
  // book: function() {}
  book(flightNum, name) {
    console.log(
      `${name} booked a seat on ${this.airline} flight ${this.iataCode}${flightNum}`
    );
    this.bookings.push({ flight: `${this.iataCode}${flightNum}`, name });
  },
};

const eurowings = {
  airline: 'Eurowings',
  iataCode: 'EW',
  bookings: [],
};

const book = lufthansa.book;

// Does NOT work as this is a normal function call, not method call
// book(23, 'Sarah Williams');

// Call method
book.call(eurowings, 23, 'Sarah Williams');
```



#### Bind Method

* Set context for "this" keyword
* Alternative to call method

```javascript
//"this" context is always eurowings
const bookEW = book.bind(eurowings);

bookEW(23, 'Steven Williams');

//Can bind multiple context
const bookEW23 = book.bind(eurowings, 23);
bookEW23('Jonas Schmedtmann');
```



#### Closures

* Function keeps track of variables in where it was created

```javascript
// Closures
const secureBooking = function () {
  let passengerCount = 0;

  return function () {
    passengerCount++;
    console.log(`${passengerCount} passengers`);
  };
};

const booker = secureBooking();

//passengerCount = 1
booker();
////passengerCount = 2
booker();
////passengerCount = 3
booker();

console.dir(booker);
```
