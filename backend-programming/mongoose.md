# Mongoose

## What is Mongoose?

* Abstraction from mongoDB driver
* More efficient query, schema, middleware

#### Installation

```
npm i mongoose@5
```

#### Connection

```javascript
const mongoose = require("mongoose")

const DB = process.env.DATABASE.replace("<PASSWORD>", process.env.DATABASE_PASSWORD);

mongoose.connect(DB, {
  useNewUrlParser: true,
  useCreateIndex: true,
  UseFindAndModify: false,
}).then(() =>{
  console.log("Database successfully connected. ");
})
```



## Schema

* Blueprint for document
* Schema properties as needed
* Anything not in a schema is ignored when retrieved

#### Declaration

```javascript
const tourSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'Tour must have a name'],
    unique: true,
  },
  duration: {
    type: Number,
    required: [true, 'Tour must have a duration'],
  },
  maxGroupSize: {
    type: Number,
    required: [true, 'Tour must have a group size'],
  },
  difficulty: {
    type: String,
    required: [true, 'Tour must have a difficulty'],
  },
  ratingsAverage: {
    type: Number,
    default: 4.5,
  },
  ratingsQuantity: {
    type: Number,
    default: 0,
  },
  price: {
    type: Number,
    required: [true, 'Tour must have a price'],
  },
  discount: {
    type: Number,
  },
  summary: {
    type: String,
    trim: true,
    required: [true, 'Tour must have a summary'],
  },
  description: {
    type: String,
    trim: true,
    required: [true, 'Tour must have a description'],
  },
  imageCover: {
    type: String,
    required: [true, 'Tour must have a cover image'],
  },
  images: [String],
  createdAt: {
    type: Date,
    default: Date.now(),
    select:false // never appears in API response
  },
  startDates: [Date],
});
```

#### Virtual Properties

* Not saved in database schema, but is calculated whenever API is invoked
  * ToJSON
  * ToObject

```javascript
//Attach to end of schema
{
    toJSON: { virtuals: true },
    toObject: { virtuals: true }
}
```

```javascript
tourSchema.virtual('durationWeeks').get(function() {
  return this.duration / 7;
});
```

## Model

* Instance of a schema

```javascript
const Tour = mongoose.model("Tour", tourSchema)
```



## CRUD

#### Create

* use async-await
* Remember to handle errors

```javascript
exports.createTour = async (req, res) => {
  try {
    const newTour = await Tour.create(req.body);

    res.status(201).json({
      status: 'success',
      data: {
        tour: newTour,
      },
    });
  } catch (err) {
    res.status(400).json({
      status: 'Failed',
      message: err,
    });
  }
};
```

#### Read

```javascript
exports.getAllTours = async (req, res) => {
  try {
    const tours = await Tour.find();
    console.log(tours);
    res.status(200).json({
      status: 'success',
      data: {
        tours,
      },
    });
  } catch (err) {
    res.status(404).json({
      status: 'Failed',
      message: err,
    });
  }
};
```

```javascript
exports.getOneTour = async (req, res) => {
  try {
    const tour = await Tour.findById(req.params.id);

    res.status(200).json({
      status: 'success',
      data: {
        tour,
      },
    });
  } catch (err) {
    res.status(404).json({
      status: 'Failed',
      message: err,
    });
  }
};
```

#### Update

```javascript
exports.updateTour = async (req, res) => {
  try {
    const tour = await Tour.findByIdAndUpdate(req.params.id, req.body, {
      new: true,
      runvalidator: true,
    });
    res.status(200).json({
      status: 'success',
      data: {
        tour: tour,
      },
    });
  } catch (err) {
    res.status(404).json({
      status: 'Failed',
      message: err,
    });
  }
};
```

#### Delete

* No need to send anything back for delete operation

```javascript
exports.deleteTour = async (req, res) => {
  try {
    await Tour.findByIdAndDelete(req.params.id);
    res.status(204).json({
      status: 'success',
      data: null,
    });
  } catch (err) {
    res.status(404).json({
      status: 'Failed',
      message: err,
    });
  }
};

```



## Importing data from existing JSON

```javascript
const fs = require('fs');
const dotenv = require('dotenv');
const mongoose = require('mongoose');
const Tour = require('./../../Models/tourModel');

dotenv.config({ path: `${__dirname}/../../config.env` });

const DB = process.env.DATABASE.replace(
  '<PASSWORD>',
  process.env.DATABASE_PASSWORD
);

mongoose
  .connect(DB, {
    useNewUrlParser: true,
    useCreateIndex: true,
    UseFindAndModify: false,
  })
  .then(() => {
    console.log('Database successfully connected. ');
  });

//Read JSON file
const tours = JSON.parse(
  fs.readFileSync(`${__dirname}/tours-simple.json`, 'utf-8')
);

//Import data into database
const importData = async () => {
  try {
    await Tour.create(tours);
    console.log('Tours loaded');
  } catch (err) {
    console.log(err);
  }
};

//Delete data from database
const deleteData = async () => {
  try {
    await Tour.deleteMany();
    console.log('Tours deleted');
  } catch (err) {
    console.log(err);
  }
};

if (process.argv[2] === '--import') {
  importData();
  process.exit();
}
if (process.argv[2] === '--delete') {
  deleteData();
  process.exit();
}

console.log(process.argv);

```



## API Improvement: Filtering by queries

#### To see queries

* E.g. 127.0.0.1:8000/api/v1/tours/?duration\[gte]=5\&difficulty=easy
* duration >= 5
* difficulty = easy

```
console.log(req.query)
```

#### Excluding fields

* Sorting
  * Ascending or descending
  * Sort by multiple parameters
  * E.g. /?sort=name,data
* Limit fields
  * determine how much data is returned in the API call (less bandwidth)
  * E.g. />fields=name,data
* Pagination and limit
  * Number of page
  * How many to show per page
  * E.g. /?page=2\&limit=100

```javascript
class APIFeatures {
  constructor(query, queryString) {
    this.query = query;
    this.queryString = queryString;
  }

  filter() {
    const queryObj = { ...this.queryString };
    const excludedFields = ['page', 'sort', 'limit', 'fields'];
    excludedFields.forEach(el => delete queryObj[el]);

    // 1B) Advanced filtering
    let queryStr = JSON.stringify(queryObj);
    queryStr = queryStr.replace(/\b(gte|gt|lte|lt)\b/g, match => `$${match}`);

    this.query = this.query.find(JSON.parse(queryStr));

    return this;
  }

  sort() {
    if (this.queryString.sort) {
      const sortBy = this.queryString.sort.split(',').join(' ');
      this.query = this.query.sort(sortBy);
    } else {
      this.query = this.query.sort('-createdAt');
    }

    return this;
  }

  limitFields() {
    if (this.queryString.fields) {
      const fields = this.queryString.fields.split(',').join(' ');
      this.query = this.query.select(fields);
    } else {
      this.query = this.query.select('-__v');
    }

    return this;
  }

  paginate() {
    const page = this.queryString.page * 1 || 1;
    const limit = this.queryString.limit * 1 || 100;
    const skip = (page - 1) * limit;

    this.query = this.query.skip(skip).limit(limit);

    return this;
  }
}
module.exports = APIFeatures;

```

```javascript
exports.getAllTours = async (req, res) => {
  try {
    // EXECUTE QUERY
    const features = new APIFeatures(Tour.find(), req.query)
      .filter()
      .sort()
      .limitFields()
      .paginate();
    const tours = await features.query;

    // SEND RESPONSE
    res.status(200).json({
      status: 'success',
      results: tours.length,
      data: {
        tours
      }
    });
  } catch (err) {
    res.status(404).json({
      status: 'fail',
      message: err
    });
  }
};
```



## API Improvement: Aliasing

* API calls that would be useful. E.g. Top five blah blah
* Use middleware to prefill query string for user

```javascript
exports.aliasTopTours = (req, res, next) => {
  req.query.limit = '5';
  req.query.sort = '-ratingsAverage,price';
  req.query.fields = 'name,price,ratingsAverage,summary,difficulty';
  next();
};
```

```javascript
router
  .route('/top-5-cheap')
  .get(tourController.aliasTopTours, tourController.getAllTours);
```
