# This

What this refers to depends on how it is called/

## Method

* this -> object calling the method

```javascript
const jonas = {
  year: 1991,
  calcAge: function () {
    console.log(this);
  },
};
jonas.calcAge();
```

## Simple function call

* this -> undefined&#x20;

```javascript
const calcAge = function (birthyear) {
  console.log(this);
};
```

## Arrow function

* this -> parent function calling arrow function

```javascript
const calcAgeArrow = (birthyear) => {
  console.log(this);
};
```

## Event listener

* this -> DOM element that handler is attached to
