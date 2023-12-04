# MongoDB

* NoSQL database
* Collections (tables) of documents (rows)



## Features

* Document based
* Scalable
* Flexible: no document data schema
* Performant
* Free and open-source



## Document Structure

* BSON
  * Like JSON, but values have types
  * field based
  * Embedded document: Document in a document
  * Each document has an unique ID (Auto-generated)



## Downloading MongoDB

* Download community edition MongoDB
  * Add bin file to system environment variables
  * To start MongoDB background process

```
mongod
```

* Download mongosh
  * Add bin file to system environment variables
  * To connect to MongoDB

```
mongosh
```



## CLI

#### Show databases

```
show dbs
```

#### Create/Switch to database

```
use {database_name}
```

#### Show collections in database

```
show collections
```

#### Exit MongoSH

```
quit()
```



## CRUD

### Create

#### Insert one document

```
db.{collection_name}.insertOne({name: "YJ"})
```

#### Insert multiple documents

```
db.{collection_name}.insertMany([{....}, {......}])
```

### Read

* Can also search with comparison, logical operators

#### Read all documents in collection

```
db.{collection_name}.find()
```

#### Reading documents that fit query

* Doesn't have to be full object, can just be a field-value pair

```
db.{collection_name}.find({...})
```

### Update

* Complete replacing data is also possible with replaceOne and replaceMany

#### Updating one document

```
db.{collection_name}.updateOne({search criteria}, {$set: {parameter to change}})
```

#### Update multiple documents

```
db.{collection_name}.updateMany({search criteria}, {$set: {parameter to change}})
```

### Delete

#### Delete one document

```
db.{collection_name}.deleteOne({delete criteria})
```

#### Delete multiple documents

```
db.{collection_name}.deleteMany({delete criteria})
```



## MongoDB Compass

* GUI for MongoDB



## MongoDB Atlas

* Cloud-based database
* Put password in dotenv file
* Generate cluster, create user, connect with Compass with provided URL
* Whitelist all IP addresses for easy development
* Connect with mongoSH

#### Connecting application to Mongo Atlas

* Copy URL to dotenv file
  * Make sure to put database name after /
* Copy password to file

#### Connecting application to local mongoDB server

```
DATABASE_LOCAL=mongodb://localhost:27017/{database_name}
```
