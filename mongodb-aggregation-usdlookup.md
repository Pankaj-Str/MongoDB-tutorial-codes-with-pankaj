# MongoDB Aggregation $lookup

### Introduction

The `$lookup` stage in MongoDB's aggregation framework is used to perform left outer joins between two collections. This allows you to combine documents from different collections based on a shared field, enabling you to retrieve related data in a single query.

### Prerequisites

* MongoDB installed and running on your machine.
* Access to `mongosh` and two populated collections with sample data.

### Step 1: Start `mongosh`

1. **Open Terminal/Command Prompt:**
   * Launch your terminal (macOS/Linux) or command prompt (Windows).
2. **Start `mongosh`:**
   *   Type the following command and press Enter:

       ```bash
       mongosh
       ```

### Step 2: Switch to the Database

Switch to the database where your collections are located.

1.  **Use a Database:**

    ```javascript
    use myNewDatabase
    ```

### Step 3: Sample Data

Assume you have two collections, `sales` and `products`. The `sales` collection has documents that look like this:

**sales collection:**

```json
{ "_id": 1, "item_id": 101, "quantity": 5 }
{ "_id": 2, "item_id": 102, "quantity": 10 }
{ "_id": 3, "item_id": 103, "quantity": 7 }
```

The `products` collection has documents that look like this:

**products collection:**

```json
{ "_id": 101, "name": "Apple", "price": 2 }
{ "_id": 102, "name": "Banana", "price": 1 }
{ "_id": 103, "name": "Carrot", "price": 1.5 }
{ "_id": 104, "name": "Orange", "price": 3 }
```

### Step 4: Using `$lookup`

#### 1. Basic Usage of `$lookup`

To perform a left outer join and combine documents from the `sales` collection with those from the `products` collection based on the `item_id` field in `sales` and the `_id` field in `products`, use the following query:

```javascript
db.sales.aggregate([
  {
    $lookup: {
      from: "products",         // The target collection to join
      localField: "item_id",   // The field from the sales collection
      foreignField: "_id",     // The field from the products collection
      as: "productDetails"      // The name of the output array field
    }
  }
])
```

**Output:**

```json
{ "_id": 1, "item_id": 101, "quantity": 5, "productDetails": [{ "_id": 101, "name": "Apple", "price": 2 }] }
{ "_id": 2, "item_id": 102, "quantity": 10, "productDetails": [{ "_id": 102, "name": "Banana", "price": 1 }] }
{ "_id": 3, "item_id": 103, "quantity": 7, "productDetails": [{ "_id": 103, "name": "Carrot", "price": 1.5 }] }
```

#### 2. Unwinding the Joined Results

If you want to flatten the results so that each product detail is represented as a separate document, you can use the `$unwind` stage after `$lookup`:

```javascript
db.sales.aggregate([
  {
    $lookup: {
      from: "products",
      localField: "item_id",
      foreignField: "_id",
      as: "productDetails"
    }
  },
  { $unwind: "$productDetails" } // Flatten the productDetails array
])
```

**Output:**

```json
{ "_id": 1, "item_id": 101, "quantity": 5, "productDetails": { "_id": 101, "name": "Apple", "price": 2 } }
{ "_id": 2, "item_id": 102, "quantity": 10, "productDetails": { "_id": 102, "name": "Banana", "price": 1 } }
{ "_id": 3, "item_id": 103, "quantity": 7, "productDetails": { "_id": 103, "name": "Carrot", "price": 1.5 } }
```

#### 3. Handling Cases with No Matches

If there are documents in the `sales` collection that do not have a matching document in the `products` collection, the `productDetails` field will still be included, but it will be an empty array. You can use `$unwind` with the `preserveNullAndEmptyArrays` option to keep these documents in the output:

```javascript
db.sales.aggregate([
  {
    $lookup: {
      from: "products",
      localField: "item_id",
      foreignField: "_id",
      as: "productDetails"
    }
  },
  { $unwind: { path: "$productDetails", preserveNullAndEmptyArrays: true } } // Preserve sales without products
])
```

#### 4. Combining with Other Stages

You can combine `$lookup` with other stages for complex aggregations. For example, to calculate the total revenue for each sale, you can include a `$project` stage:

```javascript
db.sales.aggregate([
  {
    $lookup: {
      from: "products",
      localField: "item_id",
      foreignField: "_id",
      as: "productDetails"
    }
  },
  { $unwind: "$productDetails" },
  {
    $project: {
      item_id: 1,
      quantity: 1,
      totalRevenue: { $multiply: ["$quantity", "$productDetails.price"] } // Calculate total revenue
    }
  }
])
```

**Output:**

```json
{ "item_id": 101, "quantity": 5, "totalRevenue": 10 }
{ "item_id": 102, "quantity": 10, "totalRevenue": 10 }
{ "item_id": 103, "quantity": 7, "totalRevenue": 10.5 }
```

### Conclusion

You have learned how to use the `$lookup` stage in MongoDB's aggregation framework to perform left outer joins between collections. This stage is powerful for combining related data from multiple collections, allowing you to enrich your documents and perform more complex queries.

Feel free to reach out if you have any questions or need further guidance!
