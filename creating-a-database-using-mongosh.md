# Creating a Database using mongosh

## Creating a Database using mongosh

### Introduction

MongoDB Shell (`mongosh`) is an interactive JavaScript interface to MongoDB. It allows you to interact with your databases, collections, and documents. In this tutorial, we will cover how to create a database using `mongosh`.

### Prerequisites

* MongoDB installed on your machine.
* Access to `mongosh`. If you installed MongoDB correctly, `mongosh` should be available in your command line.

### Step 1: Start `mongosh`

1. **Open Terminal/Command Prompt:**
   * Launch your terminal (macOS/Linux) or command prompt (Windows).
2. **Start `mongosh`:**
   *   Type the following command and press Enter:

       ```bash
       mongosh
       ```
   *   You should see a welcome message and the `mongosh` prompt:

       ```
       Current Mongosh Log ID: ...
       Connecting to: mongodb://localhost:27017
       ```
   * This indicates that you are connected to your MongoDB instance.

### Step 2: Create a Database

In MongoDB, a database is created when you first store data in it. However, you can explicitly switch to a new database using the `use` command. Here's how:

1. **Use the `use` Command:**
   *   To create a new database (for example, `myNewDatabase`), type the following command:

       ```javascript
       use myNewDatabase
       ```
   *   After executing this command, you will see a message like:

       ```
       switched to db myNewDatabase
       ```
   * This indicates that you've switched to `myNewDatabase`, but it won’t actually exist until you create at least one collection within it.

### Step 3: Create a Collection

Collections in MongoDB are equivalent to tables in relational databases. To create a collection and thus confirm the existence of the database, you can insert a document.

1. **Create a Collection and Insert a Document:**
   *   Let’s create a collection named `users` and insert a document:

       ```javascript
       db.users.insertOne({ name: "Pankaj", age: 30, city: "Indore" })
       ```
   * This command does two things:
     * It creates a collection called `users`.
     * It inserts a document containing the user's details.
2. **Check the Database:**
   *   To see the databases available, use the following command:

       ```javascript
       show dbs
       ```
   * You should now see `myNewDatabase` in the list, provided it contains data.

### Step 4: Verify the Collection

1. **Show Collections:**
   *   To verify that the `users` collection was created, use:

       ```javascript
       show collections
       ```
   * You should see `users` listed as a collection in `myNewDatabase`.
2. **Find Documents in the Collection:**
   *   To view the documents within the `users` collection, run:

       ```javascript
       db.users.find()
       ```
   *   This command will display all documents in the `users` collection. You should see something like this:

       ```json
       { "_id": ObjectId("..."), "name": "Pankaj", "age": 30, "city": "Indore" }
       ```

### Step 5: Additional Operations

#### Creating More Collections

You can create additional collections in the same database. For example, create a `products` collection:

```javascript
db.products.insertOne({ productName: "Laptop", price: 50000 })
```

#### Viewing All Databases

To view all databases you have created, you can run:

```javascript
show dbs
```

#### Dropping a Database

If you want to delete a database, you can do so by first switching to it and then dropping it:

```javascript
use myNewDatabase
db.dropDatabase()
```

### Conclusion

You have successfully created a database using `mongosh`, created collections, and inserted documents. This process is fundamental for working with MongoDB. In future tutorials, we will explore more complex operations such as querying, updating, and deleting documents.

Feel free to reach out with any questions or for further guidance!

***

