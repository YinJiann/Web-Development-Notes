# Data Structures

## Strings

#### Length of string

```
string.length
```

#### Slicing

```javascript
string.slice(startIndex, endIndex)
```



## Array

* Declared with "const" or "let"
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



#### Destructuring Arrays

* Extracting information about arrays, use \[ ]

```javascript
const arr = [2, 3, 4];
const [a, b, c] = arr;

//Leaving empty spaces
const [a, , c] = arr;

//default values if element doesn't exist in arr
const [a = 1, b = 1, c = 1] = arr;
```



## Spread Operator

* ...
* right side of assignment operator
* Applies for all iterables: Arrays, strings, maps, sets, objects

```javascript
const arr = [1, 2, 3];
const newArr = [...arr, 4, 5]; // output = [1, 2, 3, 4, 5]
```



## Rest Operator

* ...
* left side of assignment operator

```javascript
const [a, b, ...arr] = [1, 2, 3, 4, 5];
arr = [3 ,4 ,5]
```



## Objects

* Key-value pair
* Unordered
* Stored in heap.
* Copying objects using assignment operator (=) means creating another pointer to the same place in memory. BE CAREFUL!

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



#### Object Copying

* Object.assign() -> shallow copy, doesn't copy an object in an object
* Use external library for complete copy

```javascript
const example = {
  firstName: "John",
  lastName: "Doe",
};

const example2 = Object.assign({}, example);
```



#### Destructuring Objects

* Use { }, keys must exist in object
* Can be done in function parameter&#x20;

```javascript
const {key1, key2} = object;

//Renaming keys
const {key1: new_key1_name, key2: new_key2_name} = object;

//Renaming keys with default value
const {key1: new_key1_name = [], key2: new_key2_name = []} = object;
```



#### Iterating through an object

<pre class="language-javascript"><code class="lang-javascript"><strong>//To get all keys in an object
</strong><strong>for (const i of Object.keys(object_name)){
</strong>  //write code
}

//To get all values
for (const i of Object.values(object_name)){
  //write code
}

//To get key-value pair
for (const [key,value] of Object.entries(object_name)){
  //write code
}
</code></pre>



## Sets

* Array of unique values
* No order in set, no index

#### Set Declaration

```javascript
//Duplicates are removed
const set = new Set([1, 2, 3, 4, 5, 5]);
```

* Set size

```javascript
set.size;
```

* Adding to set

```javascript
set.add(element);
```

* Removing from set

```javascript
set.delete(element)
```

* Clear a set

```javascript
set.clear()
```



## Maps

* key-value pairs
* ordered
* Compared to objects (only strings), keys can be any values

#### Declaration

```javascript
const hashmap = new Map();

const question = new Map([
  ['question', 'What is the best programming language in the world?'],
  [1, 'C'],
]);
```

#### Adding pairs

```javascript
hashmap.set("Name", "KFC");
```

#### Removing pairs

```javascript
hashmap.delete(key);
```

#### Access data

```javascript
hashmap.get(key);
```

#### Check whether key pair exist

```javascript
hashmap.has(key);
```

#### Size

```javascript
hashmap.size;
```

#### Clear

```javascript
hashmap.clear();
```
