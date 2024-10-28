# MongoDB Aggregation $match

### Introduction

The `$match` stage in MongoDB's aggregation framework is used to filter documents based on specified criteria. It is similar to the `find` operation in MongoDB but is used within the context of an aggregation pipeline. The `$match` stage helps you narrow down the dataset before further processing, making your aggregation queries more efficient.

### Prerequisites

* MongoDB installed and running on your machine.
* Access to `mongosh` and a populated database with sample data.

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

### Step 3: Sample Data

Let’s assume you have a collection named `sales` with documents that look like this:

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "category": "fruit" }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "category": "vegetable" }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "category": "fruit" }
{ "_id": 5, "item": "broccoli", "quantity": 4, "price": 2.5, "category": "vegetable" }
```

### Step 4: Using `$match`

#### 1. Basic Usage of `$match`

To filter documents based on a specific condition, you can use the `$match` stage. For example, if you want to find all items in the `fruit` category:

```javascript
db.sales.aggregate([
  { $match: { category: "fruit" } }
])
```

**Output:**

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "category": "fruit" }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "category": "fruit" }
```

#### 2. Using Comparison Operators

You can use various comparison operators in the `$match` stage. For example, to find items with a quantity greater than 5:

```javascript
db.sales.aggregate([
  { $match: { quantity: { $gt: 5 } } } // $gt is the greater than operator
])
```

**Output:**

```json
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "category": "vegetable" }
```

#### 3. Using Logical Operators

Logical operators like `$and`, `$or`, and `$not` can be used to combine multiple conditions. For example, to find items that are either in the `fruit` category or have a price less than 2:

```javascript
db.sales.aggregate([
  { 
    $match: { 
      $or: [
        { category: "fruit" },
        { price: { $lt: 2 } }
      ] 
    } 
  }
])
```

**Output:**

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "category": "fruit" }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "category": "vegetable" }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "category": "fruit" }
```

#### 4. Combining `$match` with Other Stages

The `$match` stage can be combined with other aggregation stages for more complex queries. For example, if you want to find items in the `fruit` category and then sort them by `price`:

```javascript
db.sales.aggregate([
  { $match: { category: "fruit" } }, // Filter by category
  { $sort: { price: 1 } } // Sort by price in ascending order
])
```

**Output:**

```json
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "category": "fruit" }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "category": "fruit" }
```

### Conclusion

You have learned how to use the `$match` stage in MongoDB's aggregation framework to filter documents based on specified criteria. The `$match` stage is essential for refining your dataset and can be used in combination with other stages to create complex aggregation queries.

Feel free to reach out if you have any questions or need further guidance!
