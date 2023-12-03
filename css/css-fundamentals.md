# CSS Fundamentals

## How to reference CSS?

1. In-line CSS

* Written as an attribute for the element

2. Internal CSS

* Written in \<head> of HTML

3. External CSS

* Written as a separate CSS file, linked in \<head>



## How to reference element?

```css
//All elements
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

//HTML elements
body {
  background-color: rgb(255, 247, 201);
}

//Class elements
.first {
  color: red;
}

//ID elements
#your-name {
  background-color: rgb(255, 220, 105);
}

//Child element (for targeting specific elements under another element)
#your-name h2 {
  color: olivedrab;
}
```

## CSS Attributes

#### Color

* background-color
* color

#### Position

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* border
* margin
* padding
* width (better to specify compared to height, height is auto adjusted)
* height
* box-sizing: border-box (QOL update)
  * Maintains width & height when changing other position attributes

#### Text

* font-family
* font-size
* text-align
