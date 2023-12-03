# Express.Js

* Node.js framework to write easier and more efficient server side code
* Easy to follow MVC architecture
* Configurations are written in app.js&#x20;

#### Install express

```
npm install express@4
```

#### Importing express

```javascript
const express = require('express');
const app = express();

app.listen(8000, () =>{
    console.log(App listening on port 8000);
})
```



## Routing in Express

#### Type of requests (CRUD)

* Get: Read data
* Post: Create new data
* Put: Update the whole resource
* Patch: Update a new part of an existing resource
* Delete: Delete data

#### Status code

* 200: OK
* 201: When data successfully created
* 204: When data successfully deleted
* 400: Bad user request
* 404: Error
* 500: Internal server error

#### Response methods

* .status: set status code
* .send: return string
* .json: return object

#### GET example (all data)

<pre class="language-javascript"><code class="lang-javascript">const tours = JSON.parse(
  fs.readFileSync(`${__dirname}/dev-data/data/tours-simple.json`)
);
<strong>
</strong><strong>app.get('/api/v1/tours', (req, res) => {
</strong>  res.status(200).json({
    status: 'success',
    data: {
      tours,
    },
  });
});
</code></pre>

#### Get Example (one data)

* semicolon before variable to define as parameter
* ? after variable to make it optional parameter

```javascript
app.get('/api/v1/tours/:id/:x?', (req, res) => {
  console.log(req.params);
  
  const id = Number(req.params.id);
  const tour = tours.find((el) => el.id === id);
  
  if (!tour) {
    return res.status(404).json({
      status: 'Failed',
      message: 'Invalid ID',
    });
  }

  
  res.status(200).json({
    status: 'success',
    data: {
      tour: tour,
    },
  });
});
```

#### POST example

```javascript
app.post('/api/v1/tours', (req, res) => {
  console.log(req.body);
  const newID = tours[tours.length - 1].id + 1;
  const newTour = Object.assign({ id: newID }, req.body);
  tours.push(newTour);
  fs.writeFile(
    `{__dirname}/dev-data/data/tours-simple.json`,
    JSON.stringify(tours),
    (err) => {
      res.status(201).json({
        status: 'success',
        data: {
          tour: newTour,
        },
      });
    }
  );
});
```

#### PATCH example

* logic not implemented

```javascript
app.patch('/api/v1/tours/:id', (req, res) => {
  const id = Number(req.params.id);
  const tour = tours.find((el) => el.id === id);

  if (!tour) {
    return res.status(404).json({
      status: 'Failed',
      message: 'Invalid ID',
    });
  }

  res.status(200).json({
    status: 'success',
    data: {
      tour: 'Updated tour here',
    },
  });
});
```

#### PUT example

#### Delete example

#### More efficient routing

* combining HTTP methods that use the same endpoints
* .route()

```javascript
// app.get('/api/v1/tours', getAllTours);
// app.get('/api/v1/tours/:id', getOneTour);
// app.post('/api/v1/tours', createTour);
// app.patch('/api/v1/tours/:id', updateTour);
// app.delete('/api/v1/tours/:id', deleteTour);

app.route('/api/v1/tours').get(getAllTours).post(createTour);
app
  .route('/api/v1/tours/:id')
  .get(getOneTour)
  .patch(updateTour)
  .delete(deleteTour);
```

#### Separating routing functions

* Define a new router for each functionality
* Remember to change the path namet

```javascript
const tourRouter = express.Router();

tourRouter.route('/').get(getAllTours).post(createTour);
tourRouter.route('/:id').get(getOneTour).patch(updateTour).delete(deleteTour);

const userRouter = express.Router();

userRouter.route("/'").get(getAllUsers).post(createUser);
userRouter.route('/:id').get(getOneUser).patch(updateUser).delete(deleteUser);

app.use('/api/v1/tours', tourRouter);
app.use('/api/v1/users', userRouter);
```



## Middleware

* Manipulate request object
* All middleware are within the middleware stack
* Middleware are affected by order in code
* .use()

#### Body Parser

```javascript
app.use(express.json());
```

#### Custom Middleware Template

* next in parameter
* next() at the end of middleware body

```javascript
app.use((req, res, next) => {
    console.log("Hello from the middleware");
    next();
});

//Time recording
app.use((req, res, next) => {
  req.requestTime = new Date().toISOString();
  console.log(req.requestTime);
  next();
});
```

#### morgan

* 3rd party middleware package
* Logger in terminal for API calls

```javascript
npm i morgan
```

#### Param Middleware

* Middleware that only works when parameter is available, else ignored
* Use case: Checking valid parameters

```javascript
router.param('id', (req, res, next, val) => {
  console.log(`ID is ${val}`);
  next();
});
```

#### Middleware Chaining

* checkBody is a middleware function declared in controller
* HTTP response will go into middleware before handler

```javascript
router
  .route('/')
  .get(tourController.getAllTours)
  .post(tourController.checkBody, tourController.createTour);
```



## File System Configuration

* server.js
  * Starting server
* app.js
  * Middleware
  * Link to routers
* Routes Folder
  * Link to route handlers
*   Controller Folder

    * Handlers for routes
    * Specific middleware



## Environment Variables

* Development: default mode
* Production
* Other variables
  * Different databases

```javascript
console.log(app.get('env'));
console.log(process.env);
```

#### To set environment in terminal

```
NODE_ENV={environment} nodemon server.js
```

#### config.env

* file containing all environment variables

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

* use dotenv npm package for project to read config.env

```
npm i dotenv
```

```javascript
const dotenv = require('dotenv');
dotenv.config({ path: './config.env' });
```

#### To access environment variables

```javascript
if (process.env.NODE_ENV === 'development') {
  app.use(morgan('dev'));
}
```
