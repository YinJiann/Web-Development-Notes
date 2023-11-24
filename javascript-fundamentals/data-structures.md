# Data Structures

## Array

* Declared with "const", but we can still edit the array
* Can hold different data types

```javascript
const friends = ['Hello', 'world', 4, true];
```

```javascript
const friends = new Array("hello", 'world');
```

* Length of array

```javascript
array.length;
```

* Add element to end of array, returns length of array

```javascript
array.push(element);
```

* Add element to start of array, returns length of array

```javascript
array.unshift(element);
```

* Remove last element of array, return removed element

```javascript
array.pop(element);
```

* Remove first element of array, return removed element

```javascript
array.shift(element);
```

* Find index of element, returns index of element

```javascript
array.indexOf(element);
```

* Find if element exist in array, returns Boolean

```javascript
array.includes(element);
```



## Objects

* Key-value pair
* Each key is also considered a property
* Used for unstructured data, or if you want to access specific details by key-value

#### Declaration

```javascript
const example = {
    firstName: "Yin",
    lastName: "Jian",
    age: 26,
};
```

#### Data Add

```javascript
example.new_key = "new_value"
```



#### Data access

* If you know the key beforehand

```javascript
object.key
```

* If you do not know the key beforehand

```
object[key]
```



#### Function Declaration in Objects

* For functions to access object properties, use "this" keyword

```javascript
const example = {
    //Properties
    
    //Function in an object, must be written as function expression
    function_name_1: function (param1) {
        return result;
    },
    
    function_name_2: function(){
        a = b + this.key;
        return result;
    }
};

console.log(example.function_name_1(arg1));
console.log(example.function_name_2());
```

