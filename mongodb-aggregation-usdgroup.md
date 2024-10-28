# MongoDB Aggregation $group



***

##

### Introduction

The `$group` stage in MongoDB’s aggregation framework is used to group documents by specific fields and perform aggregate operations like counting, summing, or averaging. This tutorial will explain how to use the `$group` stage effectively.

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
```

### Step 4: Using `$group`

#### 1. Basic `$group` Example

To group documents by the `item` field and calculate the total quantity sold for each item:

```javascript
db.sales.aggregate([
  {
    $group: {
      _id: "$item",              // Group by 'item' field
      totalQuantity: { $sum: "$quantity" }, // Sum the 'quantity'
      totalPrice: { $sum: { $multiply: ["$quantity", "$price"] } } // Calculate total price
    }
  }
])
```

**Output:**

```json
{ "_id": "apple", "totalQuantity": 7, "totalPrice": 14 }
{ "_id": "banana", "totalQuantity": 13, "totalPrice": 13 }
{ "_id": "orange", "totalQuantity": 7, "totalPrice": 21 }
```

#### 2. Grouping with Multiple Fields

You can also group by multiple fields. For example, if you want to group by both `item` and `price`:

```javascript
db.sales.aggregate([
  {
    $group: {
      _id: { item: "$item", price: "$price" }, // Group by 'item' and 'price'
      totalQuantity: { $sum: "$quantity" }
    }
  }
])
```

**Output:**

```json
{ "_id": { "item": "apple", "price": 2 }, "totalQuantity": 7 }
{ "_id": { "item": "banana", "price": 1 }, "totalQuantity": 13 }
{ "_id": { "item": "orange", "price": 3 }, "totalQuantity": 7 }
```

#### 3. Counting Documents

To count the number of documents for each item:

```javascript
db.sales.aggregate([
  {
    $group: {
      _id: "$item",
      count: { $sum: 1 } // Count each document
    }
  }
])
```

**Output:**

```json
{ "_id": "apple", "count": 2 }
{ "_id": "banana", "count": 2 }
{ "_id": "orange", "count": 1 }
```

#### 4. Using `$group` with Other Stages

You can combine `$group` with other stages in the aggregation pipeline. For instance, if you want to filter documents before grouping:

```javascript
db.sales.aggregate([
  { $match: { price: { $gt: 1 } } }, // Filter items with price greater than 1
  {
    $group: {
      _id: "$item",
      totalQuantity: { $sum: "$quantity" }
    }
  }
])
```

**Output:**

```json
{ "_id": "apple", "totalQuantity": 7 }
{ "_id": "orange", "totalQuantity": 7 }
```

### Conclusion

You have learned how to use the `$group` stage in MongoDB's aggregation framework to perform various aggregate operations, including summing quantities, counting documents, and grouping by multiple fields.

Feel free to reach out if you have any questions or need further guidance!

***

