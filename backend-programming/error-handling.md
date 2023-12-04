# Error Handling

## NDB&#x20;

* node debugger

#### Installation

```
npm install ndb --global
```

```
npm install ndb --save-dev
```

#### Setup in package.json

```json
"scripts": {
    "start": "nodemon server.js",
    "debug": "ndb server.js"
  },
```

#### Launch

```json
npm run debug
```

#### Features

* Breakpoints



## Error Handling Middleware

```javascript
app.use((err, req,res, next)=>{
  // write error handling code
})
```
