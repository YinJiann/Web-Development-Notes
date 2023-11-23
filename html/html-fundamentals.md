# HTML Fundamentals

## Basic Structure

* html: Wraps the whole HTML file
* head
  * CSS file link
  * favicon
  * Title of page
*   body

    * Content of website



    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />

        <link href="style.css" rel="stylesheet" />

        <title>Learning HTML & CSS</title>
      </head>
      <body>
        <h1>JavaScript is fun, but so is HTML & CSS!</h1>
        <p class="first">
          You can learn JavaScript without HTML and CSS, but for DOM manipulation
          it's useful to have some basic ideas of HTML & CSS. You can learn more
          about it
          <a href="https://www.udemy.com/user/jonasschmedtmann/">on Udemy</a>.
        </p>

        <h2>Another heading</h2>
        <p class="second">
          Just another paragraph
        </p>

        <img
          id="course-image"
          src="https://img-a.udemycdn.com/course/480x270/437398_46c3_9.jpg"
        />

        <form id="your-name">
          <h2>Your name here</h2>
          <p class="first">Please fill in this form :)</p>

          <input type="text" placeholder="Your name" />
          <button>OK!</button>
        </form>
      </body>
    </html>

    ```

## Elements

#### Boxes

* div

#### Headings

* h1
* h2
* h3
* h4
* h5
* h6

#### Content

* p

#### Line Breaks

* br
* hr

#### Media

* img
* video
* a: hyperlink
* audio

#### Misc

* form
* table
* input



## Attributes

* Can be added to elements to provide more information, especially for styling

#### Examples (Applicable for all elements)

* Classes
  * Can be repeated
* id
  * Have to be unique

#### Examples (Not Applicable for all elements)

* href
* src
* type
* placeholder
