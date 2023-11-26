# OOP

## OOP Principles

* Abstraction
  * Hiding details that don't matter to users
* Encapsulation
  * Keeping properties and methods private to the class
  * Not accessible from outside the close
  * External sources interact through API
* Inheritance
  * Reuse logic
* Polymorphism



## Prototypes

* Contains methods that are accessible to all objects linked to it
* Methods and properties are delegated to linked objects



## Declaration

#### Constructor Function

1. New {} is created
2. "this" = {}
3. {} linked to prototype
4. function returns {}

<pre class="language-javascript"><code class="lang-javascript">const Person = function (firstName, birthYear) {
  // Instance properties
  this.firstName = firstName;
  this.birthYear = birthYear;

  // Avoid declaring function in objects!
  // this.calcAge = function () {
  //   console.log(2037 - this.birthYear);
  // };
};

//To call constructor
<strong>const jonas = new Person("Jonas", 1991);
</strong></code></pre>

We use prototype inheritance for method declaration

```javascript
ObjectName.prototype.methodName = function () {
  //write code
};
```

#### Object Literals

```javascript
const objectName = {
    firstName: "John",
    lastName: "Doe"
}
```

#### ES6 classes

* Similar to OOP in other programming languages
* Just use this man 💀

```javascript
class PersonCl {
  constructor(fullName, birthYear) {
    this.fullName = fullName;
    this.birthYear = birthYear;
  }

  // Instance methods
  calcAge() {
    console.log(2037 - this.birthYear);
  }

  //Setters and getters
  set fullName(name) {
    this._fullName = name;
  }

  get fullName() {
    return this._fullName;
  }

  // Static method, can only be called by class, not instance of class
  static hey() {
    console.log('Hey there 👋');
  }
}
```

#### Object.create

```javascript
const PersonProto = {
  calcAge() {
    console.log(2037 - this.birthYear);
  },

  init(firstName, birthYear) {
    this.firstName = firstName;
    this.birthYear = birthYear;
  },
};

const steven = Object.create(PersonProto);
```

## Inheritance

* I will only write how for ES6 classes

```javascript
class PersonCl {
  constructor(fullName, birthYear) {
    this.fullName = fullName;
    this.birthYear = birthYear;
  }

  // Instance methods
  calcAge() {
    console.log(2037 - this.birthYear);
  }
}

class StudentCl extends PersonCl {
  constructor(fullName, birthYear, course) {
    // Always needs to happen first!
    super(fullName, birthYear);
    this.course = course;
  }

  introduce() {
    console.log(`My name is ${this.fullName} and I study ${this.course}`);
  }

  //function override
  calcAge() {
    console.log(
      `I'm ${
        2037 - this.birthYear
      } years old, but as a student I feel more like ${
        2037 - this.birthYear + 10
      }`
    );
  }
}
```



## Encapsulation

* Prepend "#" to the variable name or method name

```javascript
class Account {
  // 1) Public fields (instances)
  locale = navigator.language;

  // 2) Private fields (instances)
  #movements = [];
  #pin;

  constructor(owner, currency, pin) {
    this.owner = owner;
    this.currency = currency;
    this.#pin = pin;
  }

  // 3) Public methods
  getMovements() {
    return this.#movements;
  }

  static helper() {
    console.log('Helper');
  }

  // 4) Private methods
  #approveLoan(val) {
    return true;
  }
}
```
