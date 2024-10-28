# Inserting Documents in MongoDB

## Inserting Documents in MongoDB

### Introduction

In MongoDB, documents are inserted into collections, which are analogous to tables in relational databases. This tutorial will cover the different commands you can use to insert documents into MongoDB collections.

### Prerequisites

* MongoDB installed and running on your machine.
* Access to `mongosh`.

### Step 1: Start `mongosh`

1. **Open Terminal/Command Prompt:**
   * Launch your terminal (macOS/Linux) or command prompt (Windows).
2. **Start `mongosh`:**
   *   Type the following command and press Enter:

       ```bash
       mongosh
       ```

### Step 2: Switch to the Database

Switch to the desired database where you want to insert documents.

1.  **Use a Database:**

    ```javascript
    use myNewDatabase
    ```

### Step 3: Insertion Commands

#### 1. Inserting a Single Document

To insert a single document into a collection, use the `insertOne()` method.

```javascript
db.users.insertOne({ name: "Pankaj", age: 30, city: "Indore" })
```

#### 2. Inserting Multiple Documents

To insert multiple documents at once, use the `insertMany()` method.

```javascript
db.users.insertMany([
  { name: "Aditi", age: 25, city: "Mumbai" },
  { name: "Rahul", age: 28, city: "Delhi" },
  { name: "Sita", age: 32, city: "Bangalore" }
])
```

#### 3. Inserting a Document with a Specific `_id`

You can specify a unique `_id` for the document during insertion. If you do not specify it, MongoDB will automatically generate one.

```javascript
db.users.insertOne({ _id: 1, name: "Vikram", age: 27, city: "Pune" })
```

#### 4. Inserting Documents with Arrays

You can also insert documents that contain arrays.

```javascript
db.users.insertOne({
  name: "Riya",
  age: 24,
  city: "Kolkata",
  hobbies: ["reading", "travelling", "music"]
})
```

#### 5. Inserting Nested Documents

You can insert documents that contain other documents (nested documents).

```javascript
db.users.insertOne({
  name: "Anjali",
  age: 29,
  address: {
    street: "123 Main St",
    city: "Chennai",
    zip: "600001"
  }
})
```

### Conclusion

You have learned how to use various insertion commands in MongoDB using `mongosh`, including inserting single documents, multiple documents, documents with specific `_id`s, arrays, and nested documents. Feel free to experiment with these commands in your MongoDB environment!

If you have any questions or need further guidance, feel free to ask!

***

