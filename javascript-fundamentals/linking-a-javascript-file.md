# Linking a JavaScript File

**Printing to console**

```
// Some code
console.log("...")
```



**Inline JavaScript**

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <title>JavaScript Fundamentals – Part 1</title>
  <style>
    body {
      height: 100vh;
      display: flex;
      align-items: center;
      background: linear-gradient(to top left, #28b487, #7dd56f);
    }

    h1 {
      font-family: sans-serif;
      font-size: 50px;
      line-height: 1.3;
      width: 100%;
      padding: 30px;
      text-align: center;
      color: white;
    }
  </style>
  <script>
      #insert javascript here
  </script>
</head>
```



**External JavaScript file**

* Link inside body of HTML

```html
<body>
  <h1>JavaScript Fundamentals – Part 1</h1>
  <script src="index.js"></script>
</body>
```



#### When to include script.js

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* Either add at the end of the body
* Or defer in the head
