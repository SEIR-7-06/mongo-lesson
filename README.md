# Databases - Mongo

## Lesson Objectives
1. Describe what Mongo is
1. Get Mongo running
1. Diagram the structure of Mongo
1. List your databases
1. Choose a database as a target for your actions
1. Create a collection
1. Insert a document into a collection
1. Find a set of documents in a collection
1. Remove a set of documents from a collection
1. Update a set of documents in a collection
1. Drop a Collection or an entire database

## Describe what Mongo is

MongoDB is a database technology that holds javascript objects.  The database server itself is just an application that runs quietly in the background and waits for connections (just like a web server).  You can connect to it in the same way that you would connect to a website, but instead of viewing a page, you can save, retrieve, update, and delete javascript objects to/from/in the database.

## Get Mongo running

1. To install Mongodb please follow the install instructions on their site for your operating system.
	- [Install Instructions](https://docs.mongodb.com/manual/administration/install-community/)

1. In terminal type `mongo`

To quit `mongo`, type `quit()`.

## Diagram the structure of Mongo

The Mongo database server itself contains several databases.  Each database will usually be used for a different project or application.  Imagine you're Google, and you have lots of different applications.  You don't want the data for your mail application data mixed in with your maps application data.  These different databases allow you to keep information structured in a way that is logical.

## List your databases

To list the databases in your Mongo application, use the following command:

```
show dbs
```

## Choose a database as a target for your actions

In general, you won't be switching back and forth between different databases, since, presumably, you'll just be working on one application at a time.  Because of this, we "select" a database.  Once selected, all the actions we call will affect that database until we "select" another.

To choose (or create and choose) a database, use the following command:

```
use learn
```

If we later want to remind ourselves what database we're using, use the following command:

```
db
```


## Create a collection

Inside our each database, we can have various collections.  Each collection is a set of related JavaScript objects.  Imagine we're creating a mail application.  We could have a collection of users and a different collection for messages.  The purpose of the collection is similar to databases, in that it's purely for organizational purposes.

The syntax for creating a collection is:

```
db.createCollection('employees')
```

To show a collection, use:

```
show collections
```

## Insert a document into a collection

Now we're ready to start inserting JS objects into our collection.

```
db.employees.insert({
	name:'matt',
	age: 20
})
```

We can also insert an array of objects

```
db.employees.insert(
	[
		{
			name:'bob',
			age: 42		
		},
		{
			name:'jenny',
			age: 36		
		}
	]
)
```

If things get tough to read, we can break our command out onto multiple lines

## Find a set of documents in a collection

You'll notice that inserting doesn't show what's in the collection.  This is because it's writing to the database.  You can either read from or write to the database, but not both at the same time.

To examine what's in our collection, we run:

```
db.employees.find()
```

If you don't like how this is formatted, add `.pretty()` to the end

```
db.employees.find().pretty()
```

To find all the documents in our collection that have a gender property set to 'm', we run:

```
db.employees.find({age:20}).pretty()
```

## Remove a set of documents from a collection

Remove a document, just like you would find it

```
db.employees.remove({name:'bob'})
```

## Update a set of documents in a collection

Update is similar to insert, find, and remove, but it takes two parameters.  The first is a search criteria, like before, and the second is how to change the selected records.

```
db.employees.update(
	{name:'jenny'},
	{
		$set: {
			name:'jennifer',
			age: 37
		}
	}
)
```

`$set` is **critical**.  If you forget it, you will destroy your objects.

Update will update only one document by default.  To update many, pass in a third `{ multi:true }` param

Here is the list of [Update Operators](https://docs.mongodb.com/manual/reference/operator/update/) available.

```
db.employees.update(
	{name:'jennifer'},
	{
		$set: {
			name:'jennifer',
			age: 37
		}
	},
	{
		multi: true
	}
)
```

## Drop a Collection or an entire database

If you really screw up, you can drop a collection:

```
db.employees.drop()
```

If you really REALLY screw up, you can drop an entire database:

```
db.dropDatabase()
```
