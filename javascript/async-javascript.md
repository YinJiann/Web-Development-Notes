# Async JavaScript

## What is synchronous code?

* Executed line by line
* Each line waits for the previous line to finish
* Bad: Long running operations will block subsequent code



## What is asynchronous code?

* Code executed after a task that runs in background finishes
  * E.g. setTimeout(function(), 1000);
* non-blocking



## AJAX (Asynchronous JavaScript And XML)

* Connect with remote web servers in an async way
* Instead of XML, we use JSON format
* API

#### Old Method for AJAX call

```javascript
//Getting geo information from an API
const request = new XMLHttpRequest();
request.open('GET', `https://restcountries.eu/rest/v2/name/${country}`);
request.send();

//When response arrives
request.addEventListener('load', function () {
  const [data] = JSON.parse(this.responseText);
  console.log(data);
```

#### What if we want a sequence of AJAX calls which follows the order

* Putting AJAX call inside the callback function of another AJAX call
* Basically nested AJAX calls
* Callback hell

```javascript
setTimeout(() => {
  console.log('1 second passed');
  setTimeout(() => {
    console.log('2 seconds passed');
    setTimeout(() => {
      console.log('3 second passed');
      setTimeout(() => {
        console.log('4 second passed');
      }, 1000);
    }, 1000);
  }, 1000);
}, 1000);
```



## Promises

* An object used as a placeholder for future result of an async operation
* Lifecycle of a promise
  * Pending: Waiting for result
  * Settled
    * Fulfilled: Data received
    * Rejected: Error
* fetch()

#### To consume a promise

* .then()

```javascript
const getCountryData = function (country) {
  fetch(`https://restcountries.eu/rest/v2/name/${country}`)
    .then(function (response) {
      //To access data in JSON, also an async
      return response.json();
    })
    .then(function (data) {
      //Consuming promise of .json()
      console.log(data);
      renderCountry(data[0]);
    });
};
```

#### Avoiding callback hell

```javascript
const getCountryData = function (country) {
  // Country 1
  // Fetching in JSON and handling error
  getJSON(
    `https://restcountries.eu/rest/v2/name/${country}`,
    'Country not found'
  )
    .then(data => {
      renderCountry(data[0]);
      const neighbour = data[0].borders[0];

      if (!neighbour) throw new Error('No neighbour found!');

      // Country 2
      return getJSON(
        `https://restcountries.eu/rest/v2/alpha/${neighbour}`,
        'Country not found'
      );
    })
    .then(data => renderCountry(data, 'neighbour'))
    
    //Error catching. This catches error for all callback functions above
    .catch(err => {
      console.error(`${err} 💥💥💥`);
      renderError(`Something went wrong 💥💥 ${err.message}. Try again!`);
    })
    .finally(() => {
      countriesContainer.style.opacity = 1;
    });
};
```

#### Building a promise

* Promise object receives a function
* That function must contain resolve and reject parameters

```javascript
// Building a Simple Promise
const lotteryPromise = new Promise(function (resolve, reject) {
  setTimeout(function () {
    if (Math.random() >= 0.5) {
      resolve('You WIN ');
    } else {
      reject('You lost your money ');
    }
  }, 2000);
});

lotteryPromise.then(res => console.log(res)).catch(err => console.error(err));
```

#### Creating already resolved/rejected promise immediately

```javascript
Promise.resolve('abc').then(x => console.log(x));
Promise.reject(new Error('Problem!')).catch(x => console.error(x));
```

#### async-await functions

* replacement for .then()

```javascript
const whereAmI = async function () {
    const pos = await getPosition();
    const { latitude: lat, longitude: lng } = pos.coords;
};
```

#### Running concurrent promises

```javascript
// Running Promises in Parallel
const get3Countries = async function (c1, c2, c3) {
  try {
    // const [data1] = await getJSON(
    //   `https://restcountries.eu/rest/v2/name/${c1}`
    // );
    // const [data2] = await getJSON(
    //   `https://restcountries.eu/rest/v2/name/${c2}`
    // );
    // const [data3] = await getJSON(
    //   `https://restcountries.eu/rest/v2/name/${c3}`
    // );
    // console.log([data1.capital, data2.capital, data3.capital]);

    //Create new promise from other promises
    const data = await Promise.all([
      getJSON(`https://restcountries.eu/rest/v2/name/${c1}`),
      getJSON(`https://restcountries.eu/rest/v2/name/${c2}`),
      getJSON(`https://restcountries.eu/rest/v2/name/${c3}`),
    ]);
    console.log(data.map(d => d[0].capital));
  } catch (err) {
    console.error(err);
  }
};
get3Countries('portugal', 'canada', 'tanzania');
```

#### Promise methods

* .all: when all promises are fulfilled, stops if one get rejected
* .race: when one promise is settled
* .allSettled: when all promises are settled, returns array regardless of outcome
* .any(): returns first fulfilled promise, rejected promises are ignored

```javascript
// Promise.race
(async function () {
  const res = await Promise.race([
    getJSON(`https://restcountries.eu/rest/v2/name/italy`),
    getJSON(`https://restcountries.eu/rest/v2/name/egypt`),
    getJSON(`https://restcountries.eu/rest/v2/name/mexico`),
  ]);
  console.log(res[0]);
})();

const timeout = function (sec) {
  return new Promise(function (_, reject) {
    setTimeout(function () {
      reject(new Error('Request took too long!'));
    }, sec * 1000);
  });
};

//If promise take too long, just timeout
Promise.race([
  getJSON(`https://restcountries.eu/rest/v2/name/tanzania`),
  timeout(5),
])
  .then(res => console.log(res[0]))
  .catch(err => console.error(err));

// Promise.allSettled
Promise.allSettled([
  Promise.resolve('Success'),
  Promise.reject('ERROR'),
  Promise.resolve('Another success'),
]).then(res => console.log(res));

Promise.all([
  Promise.resolve('Success'),
  Promise.reject('ERROR'),
  Promise.resolve('Another success'),
])
  .then(res => console.log(res))
  .catch(err => console.error(err));

// Promise.any [ES2021]
Promise.any([
  Promise.resolve('Success'),
  Promise.reject('ERROR'),
  Promise.resolve('Another success'),
])
  .then(res => console.log(res))
  .catch(err => console.error(err));
```

## JavaScript Event loop

* Microtask queue has priority over callback queue
* Microtasks: promises, etc
* Callback: normal callback functions

