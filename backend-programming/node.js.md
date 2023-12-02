# Node.Js

## Node.Js

* JavaScript runtime environment for server-side development
* Not suitable for CPU-intensive server
* Many module/package support
* Single thread, non-blocking nature -> High performance and efficiency. However, async functions become important
* Most code are executed in event loop, but high computation tasks are offloaded to other threads (4 by default)

## Event Loop

1. Expired Timer Callbacks
2. I/O polling and callbacks
3. SetImmediate callbacks
4. Close callbacks

* process.nextTick: Higher priority
* microtasks (promises): Higher priority



## Node Terminal

#### Enter Node Terminal

* Read-Eval-Print-Loop
* Can write simple javaScript
* Hit Tab to see all node modules

```
node
```

#### Exit Node Terminal

* CTRL + D

```
.exit
```

#### To run JavaScript files without browser

```
node {.js file}
```



## Node Practices

#### To access other module

* Need to require the particular module

```javascript
//Example for filesystem module
const fs = require("fs");
```

#### Synchronous Code

```javascript
const textIn = fs.readFileSync("./txt/input.txt", "utf-8");
console.log(textIn);
```

#### Asynchronous Code

<pre class="language-javascript"><code class="lang-javascript"><strong>//Callback hell
</strong><strong>fs.readFile("./txt/start.txt", "utf-8", (err, data) => {
</strong>  fs.readFile(`./txt/${data}.txt`, "utf-8", (err2, data2) => {
    console.log(data2);
    fs.readFile("./txt/append.txt", "utf-8", (err3, data3) => {
        console.log(data3);
    })
});
</code></pre>



## Web Server

```javascript
const http = require("http");
```

#### Declaring Server

* Each time a request is made, callback function is executed

```javascript
const server = http.createServer((req, res) => {
    res.end("Hello from server");
});
```

#### Starting Server

* Access on browser by typing in address bar: {IP\_address:port\_number}

```javascript
//Listening on port 8000, local host IP address
server.listen(8000, "127.0.0.1", () => {
  console.log("Listening to requests on port 8000");
});
```

#### Exit Server

* CTRL + C



## Routing

* Different response depending on URL

#### Simple routing example

* res.writeHead()
  * Set status code
    * 200: OK
    * 404: Not Found
  * Set HTML response header variables
    * text/html
    * application/json
* \_\_dirname
  * Indicate where current JS file is
  * If you use "./.../", if the file is run on a different directory, it will not work
* url
  * Parse URL to get details such as path name and query
* Exporting functions

```javascript
const fs = require('fs');
const http = require('http');
const url = require('url');
const slugify = require('slugify');
const replaceTemplate = require('./modules/replaceTemplate');


//Loading data to avoid being loaded for every request to web server
const tempOverview = fs.readFileSync(
  `${__dirname}/templates/template-overview.html`,
  'utf-8'
);
const tempCard = fs.readFileSync(
  `${__dirname}/templates/template-card.html`,
  'utf-8'
);
const tempProduct = fs.readFileSync(
  `${__dirname}/templates/template-product.html`,
  'utf-8'
);

const data = fs.readFileSync(`${__dirname}/dev-data/data.json`, 'utf-8');
const dataObj = JSON.parse(data);

const slugs = dataObj.map(el => slugify(el.productName, { lower: true }));
console.log(slugs);


//Actual Server
const server = http.createServer((req, res) => {
  //Extracting details from URL
  const { query, pathname } = url.parse(req.url, true);

  // Overview page
  if (pathname === '/' || pathname === '/overview') {
    res.writeHead(200, {
      'Content-type': 'text/html'
    });

    //Replacing HTML template with data from JSON
    const cardsHtml = dataObj.map(el => replaceTemplate(tempCard, el)).join('');
    const output = tempOverview.replace('<div data-gb-custom-block data-tag="PRODUCT_CARDS"></div>', cardsHtml);
    res.end(output);

    // Product page
  } else if (pathname === '/product') {
    res.writeHead(200, {
      'Content-type': 'text/html'
    });
    const product = dataObj[query.id];
    const output = replaceTemplate(tempProduct, product);
    res.end(output);

    // API
  } else if (pathname === '/api') {
    res.writeHead(200, {
      'Content-type': 'application/json'
    });
    res.end(data);

    // Not found
  } else {
    res.writeHead(404, {
      'Content-type': 'text/html',
      'my-own-header': 'hello-world'
    });
    res.end('<h1>Page not found!</h1>');
  }
});
```



```javascript
//Exporting function
module.exports = (temp, product) => {
  let output = temp.replace(/<div data-gb-custom-block data-tag="PRODUCTNAME"></div>/g, product.productName);
  output = output.replace(/<div data-gb-custom-block data-tag="IMAGE"></div>/g, product.image);
  output = output.replace(/<div data-gb-custom-block data-tag="PRICE"></div>/g, product.price);
  output = output.replace(/<div data-gb-custom-block data-tag="FROM"></div>/g, product.from);
  output = output.replace(/<div data-gb-custom-block data-tag="NUTRIENTS"></div>/g, product.nutrients);
  output = output.replace(/<div data-gb-custom-block data-tag="QUANTITY"></div>/g, product.quantity);
  output = output.replace(/<div data-gb-custom-block data-tag="DESCRIPTION"></div>/g, product.description);
  output = output.replace(/<div data-gb-custom-block data-tag="ID"></div>/g, product.id);
  
  if(!product.organic) output = output.replace(/<div data-gb-custom-block data-tag="NOT_ORGANIC"></div>/g, 'not-organic');
  return output;
}
```



## Event Listener

* Observer Pattern
  * Event emitter
  * Event listener

```javascript
const EventEmitter = require("events");
const http = require("http");

class Sales extends EventEmitter {
  constructor() {
    super();
  }
}

const myEmitter = new Sales();

//Emitters, all will execute when sending request
myEmitter.on("newSale", () => {
  console.log("There was a new sale!");
});

myEmitter.on("newSale", () => {
  console.log("Costumer name: Jonas");
});

myEmitter.on("newSale", stock => {
  console.log(`There are now ${stock} items left in stock.`);
});

myEmitter.emit("newSale", 9);

//////////////////

const server = http.createServer();

//Listeners, both will execute when request received
server.on("request", (req, res) => {
  console.log("Request received!");
  console.log(req.url);
  res.end("Request received");
});

server.on("request", (req, res) => {
  console.log("Another request 😀");
});

server.listen(8000, "127.0.0.1", () => {
  console.log("Waiting for requests...");
});
```

## Streams

* Process data piece by piece without completing whole read/write operation, more memory efficient
* Event emitters

1. Readable stream

* pipe(): pipe read data into a writeable destination

1. Writeable stream
2. Duplex stream: read and write
3. Transform stream

```javascript
server.on("request", (req, res) => {
  // Solution 1, no stream, too slow for big file
   fs.readFile("test-file.txt", (err, data) => {
     if (err) console.log(err);
     res.end(data);
   });

  // Solution 2: Streams
  //Suffer from back pressure, too much data, send too slow
   const readable = fs.createReadStream("test-file.txt");
   //write when data received in stream
   readable.on("data", chunk => {
     res.write(chunk);
   });
   //closing stream when no more data
   readable.on("end", () => {
     res.end();
   });
   //Handling errors
   readable.on("error", err => {
     console.log(err);
     res.statusCode = 500;
     res.end("File not found!");
   });

  // Solution 3
  const readable = fs.createReadStream("test-file.txt");
  readable.pipe(res);
});
```



## Exporting modules

* Exporting a class

```javascript
class Calculator {
  add(a, b) {
    return a + b;
  }

  multiply(a, b) {
    return a * b;
  }

  divide(a, b) {
    return a / b;
  }
}

module.exports = Calculator;
```

* Exporting methods

```javascript
exports.add = (a, b) => a + b;
exports.multiply = (a, b) => a * b;
exports.divide = (a, b) => a / b;

```
