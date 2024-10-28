# Creating a Collection in MongoDB



## Creating a Collection in MongoDB

### Introduction

In MongoDB, collections are analogous to tables in relational databases. A collection is a grouping of MongoDB documents, and a database can contain multiple collections. This tutorial will guide you through the process of creating a collection using `mongosh`.

### Prerequisites

* MongoDB installed and running on your machine.
* Access to `mongosh`. If MongoDB is installed correctly, you can access `mongosh` from the command line.

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

### Step 2: Switch to the Database

Before creating a collection, you need to switch to the desired database. If you don’t have a specific database in mind, you can create a new one.

1. **Use an Existing Database or Create a New One:**
   *   To switch to an existing database or create a new one (e.g., `myNewDatabase`), type:

       ```javascript
       use myNewDatabase
       ```
   *   You will see:

       ```
       switched to db myNewDatabase
       ```

### Step 3: Create a Collection

You can create a collection in MongoDB by using the `db.createCollection()` method.

#### Creating a Collection

1. **Create a Collection:**
   *   To create a collection named `users`, run the following command:

       ```javascript
       db.createCollection("users")
       ```
   *   You should see:

       ```
       { "ok" : 1 }
       ```
   * This indicates that the collection `users` has been successfully created.

#### Automatic Collection Creation

MongoDB also allows automatic collection creation when you insert the first document into a collection. For example:

1. **Insert a Document to Create a Collection:**
   *   If you prefer to create a collection by inserting a document, use:

       ```javascript
       db.products.insertOne({ productName: "Laptop", price: 50000 })
       ```
   * This command will create a collection named `products` if it does not already exist.

### Step 4: Verify the Collection

1. **Show Collections:**
   *   To check if the collections were created successfully, use:

       ```javascript
       show collections
       ```
   * You should see `users` and `products` in the list of collections.

### Step 5: Insert Documents into the Collection

Now that you have created a collection, you can insert documents into it.

1. **Insert Multiple Documents:**
   *   To add multiple documents to the `users` collection, use the following command:

       ```javascript
       db.users.insertMany([
         { name: "Pankaj", age: 30, city: "Indore" },
         { name: "Aditi", age: 25, city: "Mumbai" },
         { name: "Rahul", age: 28, city: "Delhi" }
       ])
       ```
2. **Verify Inserted Documents:**
   *   To view the documents in the `users` collection, run:

       ```javascript
       db.users.find()
       ```
   * You should see the documents you just inserted.

### Step 6: Additional Operations

#### Dropping a Collection

If you want to delete a collection, you can do so with the `drop()` method.

1.  **Drop a Collection:**

    ```javascript
    db.users.drop()
    ```

    * This command will remove the `users` collection and all its documents.

#### Viewing Collection Statistics

You can also view statistics about a collection, such as the number of documents it contains.

1.  **Get Collection Stats:**

    ```javascript
    db.users.stats()
    ```

    * This command will return statistics about the `users` collection.

### Conclusion

You have successfully created a collection in MongoDB using `mongosh`, both explicitly and implicitly by inserting documents. You also learned how to verify the collection, insert documents, and perform basic operations. In future tutorials, we will explore querying, updating, and deleting documents within collections.

Feel free to reach out with any questions or for further guidance!

***

