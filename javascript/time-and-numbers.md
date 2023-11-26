# Time and Numbers

In JavaScript, all numbers are stored as fractional values.

## To convert variables to number

```
// Some code
Number('23')

//Removes non number values
Number.parseInt("30px")
Number.parseFloat("2.5rem")
```



## Math library

* Math.min()
* Math.max()
* Math.PI
* Math.random() : values between 0 to 1
* Math.trunc(): Removes any value after decimal point
* Math.round()
* Math.floor()
* Math.ceil()



## BigInt

* To represent values to big to be represented normally
* Can only interact with BigInt

```
//Append an "n" at the end of the large integer
console.log(234324513241232135324124n)
```



## Date

```javascript
const now = new Date();
```

```javascript
//Year, month, day, hour, min, sec
//Month starts from index 0
const now = new Date(2037, 10, 19, 15, 23, 5);
```



## Timer

* SetTimeout
  * Code does not wait for SetTimeout to finish, it will continue executing subsequent code
  * Asynchronous Javascript

```javascript
setTimeout(function(param1, param2){
  //write code here
}, 5000, arg1, arg2);
```

* SetInterval
  * Continuously execute every timeout

```javascript
setInterval(function(param1, param2){
  //write code here
}, 5000, arg1, arg2);
```
