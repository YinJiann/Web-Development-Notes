# Modern JavaScript Development

* Scripts are split into modules
* Modules can be found online in Node Package Manager (NPM)
* Before production, all modules are bundled and polyfilled (made understandable for older browsers)



## Import and Export Modules

* Need to declare type as module to import other modules

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

#### Exporting

```javascript
//Exporting variables
export const cart = [];

//Exporting functions
export const addToCart = function (product, quantity) {
  cart.push({ product, quantity });
  console.log(`${quantity} ${product} added to cart`);
};

//Exporting multiple variables and renaming variables in export
const totalPrice = 237;
const totalQuantity = 23;
export { totalPrice, totalQuantity as tq };

//No name export
export default function (product, quantity) {
  cart.push({ product, quantity });
  console.log(`${quantity} ${product} added to cart`);
}

```

#### Importing

* Name has to match when importing

```javascript
// Importing named variables from modules
 import { addToCart, totalPrice as price, tq } from './shoppingCart.js';

//Importing everything in a module as an object
import * as ShoppingCart from './shoppingCart.js';
 ShoppingCart.addToCart('bread', 5);

//Giving name to default export
import add from './shoppingCart.js';
```



## NPM

* Manage all dependencies
* At start of project, npm init
  * package.json file will be created
* parcel
  * Developer tool to help package all dependencies into one script
  * Removes dead code
  * Compresses all code
