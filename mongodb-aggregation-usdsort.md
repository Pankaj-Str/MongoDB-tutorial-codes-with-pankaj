# MongoDB Aggregation $sort



### Introduction

The `$sort` stage in MongoDB's aggregation framework is used to sort the documents that pass through the pipeline according to specified fields. Sorting can be done in ascending or descending order, and it helps in organizing the data for further processing.

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

### Step 4: Using `$sort`

#### 1. Basic Usage of `$sort`

To sort documents by a specific field, you can use the `$sort` stage. For example, to sort the documents by `item` in ascending order:

```javascript
db.sales.aggregate([
  { $sort: { item: 1 } } // 1 for ascending order
])
```

**Output:**

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "category": "fruit" }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 3, "item": "broccoli", "quantity": 4, "price": 2.5, "category": "vegetable" }
{ "_id": 4, "item": "carrot", "quantity": 7, "price": 1.5, "category": "vegetable" }
{ "_id": 5, "item": "orange", "quantity": 3, "price": 3, "category": "fruit" }
```

#### 2. Sorting in Descending Order

To sort documents in descending order, use `-1`. For instance, to sort the documents by `quantity` in descending order:

```javascript
db.sales.aggregate([
  { $sort: { quantity: -1 } } // -1 for descending order
])
```

**Output:**

```json
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "category": "vegetable" }
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "category": "fruit" }
{ "_id": 5, "item": "broccoli", "quantity": 4, "price": 2.5, "category": "vegetable" }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "category": "fruit" }
```

#### 3. Sorting by Multiple Fields

You can also sort by multiple fields. For instance, to sort by `category` in ascending order and then by `price` in descending order:

```javascript
db.sales.aggregate([
  { $sort: { category: 1, price: -1 } } // First sort by category, then by price
])
```

**Output:**

```json
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "category": "fruit" }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "category": "fruit" }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "category": "vegetable" }
{ "_id": 5, "item": "broccoli", "quantity": 4, "price": 2.5, "category": "vegetable" }
```

#### 4. Using `$sort` with Other Stages

You can combine `$sort` with other aggregation stages such as `$match` and `$limit`. For example, if you want to find the top 3 items with the highest quantity sold, you would first sort and then limit the results:

```javascript
db.sales.aggregate([
  { $sort: { quantity: -1 } }, // Sort by quantity in descending order
  { $limit: 3 } // Limit to the top 3
])
```

**Output:**

```json
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "category": "fruit" }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "category": "vegetable" }
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "category": "fruit" }
```

### Conclusion

You have learned how to use the `$sort` stage in MongoDB's aggregation framework to organize your data based on specified fields. Sorting data is crucial for analysis, reporting, and presentation, and the `$sort` stage is essential for achieving this in aggregation pipelines.

Feel free to reach out if you have any questions or need further guidance!

***

