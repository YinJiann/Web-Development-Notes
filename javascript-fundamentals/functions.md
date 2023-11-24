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
* Has no access to argument execution context?

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
