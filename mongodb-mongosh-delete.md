# MongoDB mongosh Delete



### Introduction

In MongoDB, deleting documents allows you to remove unwanted data from your collections. This tutorial will guide you through the various delete operations using `mongosh`.

### Prerequisites

* MongoDB installed and running on your machine.
* Access to `mongosh` and a populated database with some documents to delete.

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

### Step 3: Deleting Documents

#### 1. Delete a Single Document

To delete a single document from a collection, use the `deleteOne()` method.

```javascript
db.users.deleteOne({ name: "Pankaj" })
```

* This will delete the first document that matches the filter where the name is "Pankaj".

#### 2. Delete Multiple Documents

To delete multiple documents that match the specified criteria, use the `deleteMany()` method.

```javascript
db.users.deleteMany({ city: "Mumbai" })
```

* This will delete all documents where the city is "Mumbai".

#### 3. Delete All Documents in a Collection

If you want to remove all documents from a collection but keep the collection itself, use `deleteMany()` with an empty filter.

```javascript
db.users.deleteMany({})
```

* This will delete all documents in the `users` collection.

#### 4. Deleting by ObjectId

If you want to delete a document using its unique `_id`, you can use the following command.

```javascript
db.users.deleteOne({ _id: ObjectId("yourObjectIdHere") })
```

* Replace `"yourObjectIdHere"` with the actual ObjectId of the document you want to delete.

#### 5. Verify Deletion

To verify that the deletion was successful, you can query the collection to check if the documents have been removed.

```javascript
db.users.find()
```

* This will display all remaining documents in the `users` collection.

### Conclusion

You have learned how to delete documents in MongoDB using `mongosh`. You can delete single or multiple documents, remove all documents in a collection, and delete by specific `_id`.

If you have any questions or need further guidance, feel free to ask!

***

