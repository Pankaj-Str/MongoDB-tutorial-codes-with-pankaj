# MongoDB Aggregation $limit

### Introduction

The `$limit` stage in MongoDB's aggregation framework is used to restrict the number of documents passed to the next stage in the pipeline. This is particularly useful when you only want to retrieve a subset of documents, such as the top results based on certain criteria.

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
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2 }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1 }
{ "_id": 3, "item": "apple", "quantity": 2, "price": 2 }
{ "_id": 4, "item": "orange", "quantity": 7, "price": 3 }
{ "_id": 5, "item": "banana", "quantity": 3, "price": 1 }
{ "_id": 6, "item": "grapes", "quantity": 4, "price": 4 }
{ "_id": 7, "item": "mango", "quantity": 8, "price": 5 }
```

### Step 4: Using `$limit`

#### 1. Basic Usage of `$limit`

To limit the number of documents returned in the aggregation pipeline, you can use the `$limit` stage.

For example, to retrieve only the first three documents from the `sales` collection:

```javascript
db.sales.aggregate([
  { $limit: 3 }
])
```

**Output:**

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2 }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1 }
{ "_id": 3, "item": "apple", "quantity": 2, "price": 2 }
```

#### 2. Using `$limit` After Sorting

It is common to use `$limit` after sorting the results to get the top N documents based on a specific field. For example, if you want the top two items with the highest quantity sold:

```javascript
db.sales.aggregate([
  { $sort: { quantity: -1 } }, // Sort in descending order of quantity
  { $limit: 2 } // Limit to the top 2
])
```

**Output:**

```json
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1 }
{ "_id": 7, "item": "mango", "quantity": 8, "price": 5 }
```

#### 3. Combining `$limit` with Other Stages

You can combine `$limit` with other stages like `$match` and `$group`. For instance, if you want to find the top items sold, but only for those with a price greater than 1:

```javascript
db.sales.aggregate([
  { $match: { price: { $gt: 1 } } }, // Filter items with price greater than 1
  { $sort: { quantity: -1 } }, // Sort by quantity in descending order
  { $limit: 3 } // Limit to the top 3
])
```

**Output:**

```json
{ "_id": 7, "item": "mango", "quantity": 8, "price": 5 }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1 }
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2 }
```

### Conclusion

You have learned how to use the `$limit` stage in MongoDB's aggregation framework to restrict the number of documents returned in a query. By combining `$limit` with other stages like `$sort` and `$match`, you can refine your queries to retrieve specific subsets of data.

Feel free to reach out if you have any questions or need further guidance!

***

