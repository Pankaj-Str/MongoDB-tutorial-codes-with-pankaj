# MongoDB Query Operators



***

##

### Introduction

MongoDB query operators are special symbols that help you to specify criteria for matching documents in your queries. This tutorial will cover the most commonly used query operators in MongoDB and provide examples of how to use them with `mongosh`.

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

### Step 3: Commonly Used Query Operators

#### 1. Comparison Operators

These operators are used to compare values:

*   **$eq**: Matches values that are equal to a specified value.

    ```javascript
    db.users.find({ age: { $eq: 30 } })
    ```
*   **$ne**: Matches values that are not equal to a specified value.

    ```javascript
    db.users.find({ city: { $ne: "Mumbai" } })
    ```
*   **$gt**: Matches values that are greater than a specified value.

    ```javascript
    db.users.find({ age: { $gt: 25 } })
    ```
*   **$gte**: Matches values that are greater than or equal to a specified value.

    ```javascript
    db.users.find({ age: { $gte: 30 } })
    ```
*   **$lt**: Matches values that are less than a specified value.

    ```javascript
    db.users.find({ age: { $lt: 30 } })
    ```
*   **$lte**: Matches values that are less than or equal to a specified value.

    ```javascript
    db.users.find({ age: { $lte: 25 } })
    ```

#### 2. Logical Operators

These operators are used to combine multiple criteria:

*   **$and**: Joins query clauses with a logical AND.

    ```javascript
    db.users.find({ $and: [{ age: { $gt: 25 } }, { city: "Delhi" }] })
    ```
*   **$or**: Joins query clauses with a logical OR.

    ```javascript
    db.users.find({ $or: [{ city: "Mumbai" }, { city: "Delhi" }] })
    ```
*   **$not**: Inverts the effect of a query expression.

    ```javascript
    db.users.find({ age: { $not: { $gte: 30 } } })
    ```
*   **$nor**: Joins query clauses with a logical NOR.

    ```javascript
    db.users.find({ $nor: [{ city: "Mumbai" }, { city: "Delhi" }] })
    ```

#### 3. Element Operators

These operators are used to query documents based on the existence of fields:

*   **$exists**: Matches documents that have a specified field.

    ```javascript
    db.users.find({ city: { $exists: true } })
    ```
*   **$type**: Selects documents with a specified field type.

    ```javascript
    db.users.find({ age: { $type: "int" } })
    ```

#### 4. Evaluation Operators

These operators are used for evaluating strings or arrays:

*   **$regex**: Matches documents with fields that match a specified regular expression.

    ```javascript
    db.users.find({ name: { $regex: /^P/, $options: "i" } }) // Case insensitive
    ```
*   **$where**: Allows the use of JavaScript expressions to specify queries.

    ```javascript
    db.users.find({ $where: "this.age > 25" })
    ```

#### 5. Array Operators

These operators are used to query documents containing arrays:

*   **$all**: Matches arrays that contain all elements specified in the query.

    ```javascript
    db.users.find({ hobbies: { $all: ["reading", "travelling"] } })
    ```
*   **$elemMatch**: Matches documents that contain an array field with at least one element that matches all the specified query criteria.

    ```javascript
    db.users.find({ hobbies: { $elemMatch: { $eq: "reading", $size: 1 } } })
    ```
*   **$size**: Matches any array with a specified number of elements.

    ```javascript
    db.users.find({ hobbies: { $size: 3 } })
    ```

### Step 4: Using Query Operators in Your Applications

You can combine multiple query operators to create complex queries that suit your needs.

#### Example:

To find users who are older than 25, live in either "Mumbai" or "Delhi", and have a hobby of "reading", you could write:

```javascript
db.users.find({
  $and: [
    { age: { $gt: 25 } },
    { $or: [{ city: "Mumbai" }, { city: "Delhi" }] },
    { hobbies: { $elemMatch: { $eq: "reading" } } }
  ]
})
```

### Conclusion

You have learned about various MongoDB query operators, including comparison, logical, element, evaluation, and array operators. These operators are essential for building complex queries and effectively managing data in your MongoDB collections.

If you have any questions or need further guidance, feel free to ask!

***

