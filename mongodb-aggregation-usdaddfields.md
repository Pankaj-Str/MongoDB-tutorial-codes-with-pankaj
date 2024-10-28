# MongoDB Aggregation $addFields

### Introduction

The `$addFields` stage in MongoDB's aggregation framework is used to add new fields to documents or modify existing fields within a pipeline. This stage is useful for transforming your data by calculating new values or altering the structure of your documents before they are passed to subsequent stages in the aggregation pipeline.

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
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5 }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3 }
{ "_id": 5, "item": "broccoli", "quantity": 4, "price": 2.5 }
```

### Step 4: Using `$addFields`

#### 1. Basic Usage of `$addFields`

To add a new field to each document, use the `$addFields` stage. For example, if you want to add a `totalPrice` field that calculates the total price for each item based on `quantity` and `price`:

```javascript
db.sales.aggregate([
  {
    $addFields: {
      totalPrice: { $multiply: ["$quantity", "$price"] } // Calculate totalPrice
    }
  }
])
```

**Output:**

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "totalPrice": 10 }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "totalPrice": 10 }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "totalPrice": 10.5 }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "totalPrice": 9 }
{ "_id": 5, "item": "broccoli", "quantity": 4, "price": 2.5, "totalPrice": 10 }
```

#### 2. Modifying Existing Fields

You can also use `$addFields` to modify existing fields. For instance, if you want to increase the price of each item by 10%:

```javascript
db.sales.aggregate([
  {
    $addFields: {
      price: { $multiply: ["$price", 1.1] } // Increase price by 10%
    }
  }
])
```

**Output:**

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2.2 }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1.1 }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.65 }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3.3 }
{ "_id": 5, "item": "broccoli", "quantity": 4, "price": 2.75 }
```

#### 3. Adding Multiple Fields

You can add multiple fields in a single `$addFields` stage. For example, to add both `totalPrice` and a new field called `status` based on the quantity:

```javascript
db.sales.aggregate([
  {
    $addFields: {
      totalPrice: { $multiply: ["$quantity", "$price"] },
      status: { $cond: { if: { $gte: ["$quantity", 5] }, then: "In Stock", else: "Low Stock" } }
    }
  }
])
```

**Output:**

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "totalPrice": 10, "status": "In Stock" }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "totalPrice": 10, "status": "In Stock" }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "totalPrice": 10.5, "status": "In Stock" }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "totalPrice": 9, "status": "Low Stock" }
{ "_id": 5, "item": "broccoli", "quantity": 4, "price": 2.5, "totalPrice": 10, "status": "Low Stock" }
```

#### 4. Combining `$addFields` with Other Stages

You can combine `$addFields` with other aggregation stages for more complex data transformations. For example, you can first filter items that are in stock and then add the `totalPrice`:

```javascript
db.sales.aggregate([
  { $match: { quantity: { $gt: 0 } } }, // Filter for items in stock
  {
    $addFields: {
      totalPrice: { $multiply: ["$quantity", "$price"] }
    }
  }
])
```

**Output:**

```json
{ "_id": 1, "item": "apple", "quantity": 5, "price": 2, "totalPrice": 10 }
{ "_id": 2, "item": "banana", "quantity": 10, "price": 1, "totalPrice": 10 }
{ "_id": 3, "item": "carrot", "quantity": 7, "price": 1.5, "totalPrice": 10.5 }
{ "_id": 4, "item": "orange", "quantity": 3, "price": 3, "totalPrice": 9 }
{ "_id": 5, "item": "broccoli", "quantity": 4, "price": 2.5, "totalPrice": 10 }
```

### Conclusion

You have learned how to use the `$addFields` stage in MongoDB's aggregation framework to add or modify fields in documents. This stage is essential for transforming your data, allowing you to perform calculations and create a more informative dataset for analysis and reporting.

Feel free to reach out if you have any questions or need further guidance!

***

