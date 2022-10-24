# Mongodb & Mongoose

[TOC]

## MongoDB

- MongoDB will be our data store that we use for this part of the course
- It's a nosql database…
- Specifically, it's a document store
    - a single **record** in Mongo is a **document** (a *user*, a *bird* in the case of our homework!)
    - a document is a bunch of key value pairs…
    - hey… **that sounds like…** →
    - documents are similar to JSON objects (actually BSON?)

## Documents and Collections

A couple of terms to remember (yay, definitions again!)

- **key** - a field name - analogous to a column in a relational database
- **value** - obvs, a value
- **document** - a single object or record in our database,
    - consists of key value pairs
    - similar to a single row in a relational database
- **collection** - a group of documents
    - analogous to tables in relational databases

## Data Types

Although MongoDB doesn't require you to pre-define the types of values that your documents will have, it does have data types. These types **are inferred from the value**. Some available types include:

- **string** - an empty string or an ordered sequence characters
- **numeric types** - such as integer, double (float)
- **boolean** - true / false
- **array** - a list of values
- **timpestamp** - 64 bit value where first 32 bits are seconds since the Unix epoch
- **Object ID** every MongoDB object or document must have an Object ID which is unique


More about **Object ID**: a 12-byte value, consists of: a 4-byte timestamp (seconds since epoch), a 3-byte machine id, a 2-byte process id, and a 3-byte counter

## Some Commands

**The following commands can be used to navigate, create and remove databases and collections** →

- `show databases` - show available databases (remember, there can be more than one database)
- `use db` - work with a specific database (if unspecified, the default database connected to is test)
- `show collections` - once a db is selected, show the collections within the database
- `db.dropDatabase()` - drop (remove) the database that you're currently in
- `db.collectionName.drop()` - drop (remove) the collection named `collectionName`

To get some inline help:

- `help` - get help on available commands



## Starting Out

**To begin using the commandline client to inspect your data:** →

1. make sure that `mongod` is running in a different window (or running *in the background* or as a daemon)
2. start up the commandline client with `mongo`
3. type in `use databaseName` to switch to the database that you're looking through



From there, you can start querying for data, inserting documents, etc. These basic create, read, update, and delete operations are called **CRUD** operations…



## CRUD!?

**(C)reate, (R)ead, (U)pdate, and (D)elete operations:** →

- db.[collection].insert(obj)
    - `db.Person.insert({'first':'bob', 'last':'bob'})`
- db.[collection].find(queryObj)
    - `db.Person.find({'last':'bob'})`
    - `db.Person.find() // finds all!`
- db.[collection].update(queryObj, queryObj)
    - `db.Person.update({'first':'foo'}, {$set: {'last':'bar'}})`
- db.[collection].remove(queryObj)
    - `db.Person.remove({'last':'bob'})`


Where `queryObj` is a name value pair that represents the property you're searching on… with a value that matches the value you specify

## More Examples

**As prep for the next part, some insert and finds (with a test for greater than!)** →

Inserting, finding all, then finding by exact number of lives:

```javascript
> db.Cat.insert({name:'foo', lives:9})
WriteResult({ "nInserted" : 1 })
> db.Cat.find()
{ "_id" : ObjectId("57ff86a14639d0fd263f87a0"), "name" : "foo", "lives" : 9 }
> db.Cat.find({lives:9})
{ "_id" : ObjectId("57ff86a14639d0fd263f87a0"), "name" : "foo", "lives" : 9 }
```

Inserting more, then using greater than!

```javascript
> db.Cat.insert({name:'bar', lives:2})
WriteResult({ "nInserted" : 1 })
> db.Cat.insert({name:'qux', lives:5})
WriteResult({ "nInserted" : 1 })
> db.Cat.find({lives: {$gt: 4}})
{ "_id" : ObjectId("57ff86a14639d0fd263f87a0"), "name" : "foo", "lives" : 9 }
{ "_id" : ObjectId("57ff86c14639d0fd263f87a2"), "name" : "qux", "lives" : 5 }
```

## Using MongoDB in Express

As with everything else we've done in node, there's a module for our specific task. If we'd like to use MongoDB in our application, there are [a few options](http://docs.mongodb.org/ecosystem/drivers/node-js/):

- **mongodb** - the officially supported driver from MongoDB; optimized for simplicity
- **mongoose** - lots of features, more complex, based on mongodb
- **monk** - somewhere between mongoose and mongodb in terms of features and complexity (for example, no models)

We'll be using mongoose, as it seems to have the most traction out of the three. (But it's a bit more complicated than it needs to be).

## Mongoose Concepts

- **schema** - analogous to a collection
- **model** - the actual constructors that we use to create objects
- **object** - a single document

## Set Up Your Connection

For simplicity, we'll dump everything in a file called `[PROJECT ROOT]/db.js` for now. We'll see other ways of laying things out.


In `db.js`:

```javascript
// as always, require the module
const mongoose = require('mongoose'); 

// some extra stuff goes here...

// connect to the database (catdb)
mongoose.connect('mongodb://localhost/catdb');
```

## Create a Schema

Between your require and connect… create a **schema**. A schema represents a MongoDB collection. Here we're specifying a collection for Cats.

- the cat schema will allow us to read objects from the collection
- as well as modify and add objects to the collection

```javascript
// define the data in our collection
const Cat = new mongoose.Schema({
	name: String,
	updated_at: Date
});

// "register" it so that mongoose knows about it
mongoose.model('Cat', Cat);
```

## Using Our db Module

In `app.js`, simply:

```javascript
require( './db' );
```



- this will initialize our connection to the database when our application runs
- it also sets up our schemas, so we can use them in our routes

## Using Schemas

Ostensibly, we would want to create, update, read or delete data based on what page (path/url/etc.) we're on. **Let's start by adding some setup to our `index.js` routes.** →

```javascript
const mongoose = require('mongoose');
const Cat = mongoose.model('Cat');
```

## /cats

Use the schema's find method to read objects (of course, we have to define a callback that gets triggered when the read is done)!

```javascript
router.get('/cats', function(req, res) {
	Cat.find(function(err, cats, count) {
		res.render( 'cats', {
			cats: cats
		});
	});
});
```

## /cat/create

We'll also need a form. **We can handle this one pretty easily.** →

```javascript
router.get('/cat/create', function(req, res) {
  res.render('create');
});
```

## /cats/create

Let's accept posts to `/cat/create`. We'll use our schema to create an object:

- create a new Cat object
- set its properties
- call save
- tell save what to do when it finishes saving (callback, ftw)

```javascript
router.post('/cat/create', function(req, res) {
	console.log(req.body.catName);
	new Cat({
		name: req.body.catName,
		updated_at : Date.now()
	}).save(function(err, cat, count){
		res.redirect('/cats');
	});
});
```

## And Some Templates….

**Our is essentially the same as all of the previous forms we've had** →

```html
<form method="POST" action="">
cat name plz
<input type="text" name="catName">
<input type="submit">
</form>
```

## And a Template for the List

**As with our previous templates, we'll just loop through all of the objects that we retrieve.** →

- note that because we have a list of objects…
- we can reference each property name, rather than using this
- for our example, name is a property of each object

```html
<ul>
{{#each cats}}
<li>{{name}}</li>
{{/each}}
</ul>
```