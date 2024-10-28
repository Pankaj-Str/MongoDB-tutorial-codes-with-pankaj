# Updating Documents in MongoDB



***

##

### Introduction

Updating documents in MongoDB allows you to modify existing data within your collections. This tutorial will guide you through various update operations using `mongosh`.

### Prerequisites

* MongoDB installed and running on your machine.
* Access to `mongosh` and a populated database with some documents to update.

### Step 1: Start `mongosh`

1. **Open Terminal/Command Prompt:**
   * Launch your terminal (macOS/Linux) or command prompt (Windows).
2. **Start `mongosh`:**
   *   Type the following command and press Enter:

       ```bash
       mongosh
       ```

### Step 2: Switch to the Database

Switch to the database where your collection is located.

1.  **Use a Database:**

    ```javascript
    use myNewDatabase
    ```

### Step 3: Updating Documents

#### 1. Update a Single Document

To update a single document in a collection, use the `updateOne()` method.

```javascript
db.users.updateOne(
  { name: "Pankaj" }, // Filter to select the document
  { $set: { age: 31 } } // Update operation
)
```

* This will update the first document with the name "Pankaj", setting the age to 31.

#### 2. Update Multiple Documents

To update multiple documents at once, use the `updateMany()` method.

```javascript
db.users.updateMany(
  { city: "Indore" }, // Filter to select documents
  { $set: { city: "Mumbai" } } // Update operation
)
```

* This will update all documents where the city is "Indore", changing it to "Mumbai".

#### 3. Update Specific Fields

You can update specific fields in a document. If the field does not exist, it will be created.

```javascript
db.users.updateOne(
  { name: "Aditi" },
  { $set: { hobbies: ["reading", "travelling"] } }
)
```

* This will add the `hobbies` field to the document with the name "Aditi".

#### 4. Use Operators to Update Values

You can use operators to modify values during the update. Here are a few examples:

*   **Increment a Value:**

    ```javascript
    db.users.updateOne(
      { name: "Rahul" },
      { $inc: { age: 1 } } // Increment age by 1
    )
    ```
*   **Rename a Field:**

    ```javascript
    db.users.updateMany(
      {},
      { $rename: { city: "location" } } // Rename 'city' to 'location'
    )
    ```

#### 5. Upsert Operation

An upsert operation allows you to insert a new document if no documents match the query criteria.

```javascript
db.users.updateOne(
  { name: "Anil" }, // Filter
  { $set: { age: 26, city: "Jaipur" } }, // Update
  { upsert: true } // Create the document if it doesn't exist
)
```

* If there is no document with the name "Anil", it will create a new one with the specified fields.

### Step 4: Verify Updates

To verify that the updates were successful, you can query the collection.

```javascript
db.users.find()
```

* This will display all documents in the `users` collection, allowing you to see the changes made.

### Conclusion

You have learned how to update documents in MongoDB using `mongosh`. You can update single and multiple documents, specify fields, use operators for modifications, and perform upsert operations.

If you have any questions or need further guidance, feel free to ask!

***

