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
