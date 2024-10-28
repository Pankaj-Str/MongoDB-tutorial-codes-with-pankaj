# Finding Documents in MongoDB

### Introduction

In MongoDB, finding documents is done using the `find()` method, which retrieves documents from a collection based on specified criteria. This tutorial will guide you through the various ways to find documents in a MongoDB collection using `mongosh`.

### Prerequisites

* MongoDB installed and running on your machine.
* Access to `mongosh` and a populated database.

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

### Step 3: Finding Documents

#### 1. Find All Documents

To retrieve all documents in a collection, use the `find()` method without any parameters.

```javascript
db.users.find()
```

* This will return all documents in the `users` collection.

#### 2. Find Documents with Criteria

You can specify criteria to filter the documents returned by the `find()` method.

1.  **Find Documents by Field Value:**

    * To find documents where the name is "Pankaj":

    ```javascript
    db.users.find({ name: "Pankaj" })
    ```
2.  **Find Documents by Multiple Fields:**

    * To find documents where the age is 30 and the city is "Indore":

    ```javascript
    db.users.find({ age: 30, city: "Indore" })
    ```

#### 3. Find Documents with Comparison Operators

MongoDB supports various comparison operators that you can use in your queries.

1.  **Find Documents with `$gt` (Greater Than):**

    * To find users older than 25:

    ```javascript
    db.users.find({ age: { $gt: 25 } })
    ```
2.  **Find Documents with `$lt` (Less Than):**

    * To find users younger than 30:

    ```javascript
    db.users.find({ age: { $lt: 30 } })
    ```
3.  **Find Documents with `$ne` (Not Equal):**

    * To find users not living in "Mumbai":

    ```javascript
    db.users.find({ city: { $ne: "Mumbai" } })
    ```

#### 4. Find Documents with Logical Operators

MongoDB allows you to combine multiple criteria using logical operators.

1.  **Using `$or`:**

    * To find users who are either from "Delhi" or "Mumbai":

    ```javascript
    db.users.find({ $or: [{ city: "Delhi" }, { city: "Mumbai" }] })
    ```
2.  **Using `$and`:**

    * To find users who are older than 25 and from "Indore":

    ```javascript
    db.users.find({ $and: [{ age: { $gt: 25 } }, { city: "Indore" }] })
    ```

#### 5. Find Documents with Projection

You can limit the fields returned by the query using projection.

1.  **Find Specific Fields:**

    * To find all users but only return their names and cities:

    ```javascript
    db.users.find({}, { name: 1, city: 1 })
    ```

#### 6. Find One Document

To find a single document that matches the criteria, use the `findOne()` method.

```javascript
db.users.findOne({ name: "Pankaj" })
```

* This will return the first document that matches the criteria.

### Step 4: Sort and Limit Results

You can sort and limit the results returned by your queries.

1.  **Sort Results:**

    * To find all users sorted by age in ascending order:

    ```javascript
    db.users.find().sort({ age: 1 })
    ```
2.  **Limit Results:**

    * To limit the results to the first 2 documents:

    ```javascript
    db.users.find().limit(2)
    ```

### Conclusion

You have learned how to find documents in MongoDB using `mongosh`. You can retrieve all documents, filter them based on specific criteria, use comparison and logical operators, project specific fields, and sort and limit the results.

Feel free to reach out with any questions or for further guidance!

***

