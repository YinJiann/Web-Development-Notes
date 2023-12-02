# NPM

* Node package manager

#### Creating a package

* package.json&#x20;

```
npm init
```

#### Install packages

* Production dependencies
  * slugify: To manipulate URL to more readable parameters

```
npm install {package_name}
```

* Development dependencies
  * nodemon: Automatically restart server whenever changes to the code

```
npm install {package_name} --save-dev
```

* Global installation

```
npm i {package_name} --global
```

#### Uninstall packages

```json
npm uninstall {package_name}
```

#### Executing scripts in NPM

* Change "scripts" in package.json

```json
"scripts": {
  "start": "nodemon index.js"
},

npm run start
```

#### Sharing development

* Do not share node\_modules file
* Share package.json and package-lock.json to let others reconstruct project

```json
npm install
```
