# DOM Manipulation

## What is DOM?

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* Document Object Model: To access and change HTML and CSS elements

##

## Element Selection

#### Class

* If more than 1 of a class, only the first will be selected

```javascript
document.querySelector(".message")
```

* To select all. Returns an array of class elements

```
document.querySelectorAll(".message")
```

#### ID

```javascript
document.querySelector("#message")
```

* Alternate way to obtain by ID, no need for "#"

```javascript
const score1 = document.getElementById("score--1");
```

#### Text Content

<pre class="language-javascript"><code class="lang-javascript"><strong>document.querySelector(element).textContent
</strong></code></pre>

#### Input Value

<pre class="language-javascript"><code class="lang-javascript"><strong>document.querySelector(element).value
</strong></code></pre>

#### Style

* "style" keyword
* Followed by specific CSS attribute

```javascript
document.querySelector(element).style.attribute = value;
```

##

## On-click Events

* Arg1: Specify what event it is
  * click
* Arg2: function to execute during event

```javascript
document.querySelector(element).addEventListener(event, function () {
  //event code
});

```

#### Add classes

* .classList.add("class1", "class2")

```javascript
btnsOpenModal[i].addEventListener("click", function () {
  modal.classList.add("hidden");
});
```

#### Remove classes

* .classList.remove("class1", "class2")

```javascript
btnsOpenModal[i].addEventListener("click", function () {
  modal.classList.remove("hidden");
});
```

#### Toggle classes

* .classList.toggle("class1")

```javascript
btnsOpenModal[i].addEventListener("click", function () {
  modal.classList.toggle("class1");
});
```



## Keypress Event

* keypress: hold down
* keydown: when pressed
* keyup: when released

#### Specific key event

* Pass an argument for the function to get information of event

```javascript
document.addEventListener("keydown", function (event) {
  //If escape key is pressed
  if (event.key === "Escape") {
    closeModal();
  }
});
```



## Element creation and insertion

```javascript
// Creating and inserting elements
const message = document.createElement('div');
message.classList.add('cookie-message');
message.textContent = 'We use cookied for improved functionality and analytics.';
message.innerHTML =
  'We use cookied for improved functionality and analytics. <button class="btn btn--close-cookie">Got it!</button>';

header.prepend(message);
header.append(message);
header.append(message.cloneNode(true));

header.before(message);
header.after(message);
```



## Element Deletion

```javascript
// Delete elements
document
  .querySelector('.btn--close-cookie')
  .addEventListener('click', function () {
     message.remove();
  });
```



## Changing HTML and CSS attributes

```javascript
// Non-standard
console.log(logo.getAttribute('designer'));
logo.setAttribute('company', 'Bankist');

console.log(logo.getAttribute('src'));

const link = document.querySelector('.nav__link--btn');
//returns absolute path
console.log(link.href);
//returns path written in HTML doc
console.log(link.getAttribute('href'));
```



## Smooth scrolling after hitting button

```javascript
btnScrollTo.addEventListener('click', function (e) {
  //section1 is destination
  document.querySelector("#section1").scrollIntoView({ behavior: 'smooth' });
}
```



## Event propagation

#### Bubbling and capturing

* Capture: When an event occurs, event is generated at top of DOM tree and passed down to target node
* Bubbling: Event is executed, then passed to top of DOM tree
* If parent HTML element handles the same event, event will also be triggered during bubbling phase
* To stop propagation, event.stopPropagation()
* Use case: Rather than assigning same function to multiple child nodes, implement in the parent node, disable event execution on the parent node if pressed directly, and let bubbling handle the rest.



## DOM Traversing

* Finding child, parent DOM during runtime

```javascript
// DOM Traversing
const h1 = document.querySelector('h1');

// Going downwards: child
console.log(h1.querySelectorAll('.highlight'));
console.log(h1.childNodes);
console.log(h1.children);

// Going upwards: parents
console.log(h1.parentNode);
console.log(h1.parentElement);

//Closest parent with defined element
h1.closest('h1').style.background = 'var(--gradient-primary)';

// Going sideways: siblings
console.log(h1.previousElementSibling);
console.log(h1.nextElementSibling);

console.log(h1.previousSibling);
console.log(h1.nextSibling);
```

