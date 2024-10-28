# MongoDB Aggregation $project

### Introduction

The `$project` stage in MongoDB's aggregation framework is used to reshape documents in the pipeline by including, excluding, or adding fields. This stage allows you to control the output of your aggregation results, making it a powerful tool for data transformation.

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

### Step 4: Using `$project`

#### 1. Basic Usage of `$project`

To include specific fields in the output documents, you can use the `$project` stage. For example, if you only want to display the `item` and `quantity` fields:

```javascript
db.sales.aggregate([
  {
    $project: {
      _id: 0,             // Exclude the _id field
      item: 1,           // Include the item field
      quantity: 1        // Include the quantity field
    }
  }
])
```

**Output:**

```json
{ "item": "apple", "quantity": 5 }
{ "item": "banana", "quantity": 10 }
{ "item": "carrot", "quantity": 7 }
{ "item": "orange", "quantity": 3 }
{ "item": "broccoli", "quantity": 4 }
```

#### 2. Excluding Fields

You can also exclude specific fields from the output. For example, to exclude the `price` field:

```javascript
db.sales.aggregate([
  {
    $project: {
      _id: 0,             // Exclude the _id field
      item: 1,           // Include the item field
      quantity: 1,        // Include the quantity field
      price: 0            // Exclude the price field
    }
  }
])
```

**Output:**

```json
{ "item": "apple", "quantity": 5 }
{ "item": "banana", "quantity": 10 }
{ "item": "carrot", "quantity": 7 }
{ "item": "orange", "quantity": 3 }
{ "item": "broccoli", "quantity": 4 }
```

#### 3. Adding Computed Fields

You can also create new fields based on existing fields. For instance, if you want to calculate the total price for each item (quantity \* price), you can do so like this:

```javascript
db.sales.aggregate([
  {
    $project: {
      _id: 0,                        // Exclude the _id field
      item: 1,                      // Include the item field
      quantity: 1,                  // Include the quantity field
      totalPrice: {                 // Create a new field for total price
        $multiply: ["$quantity", "$price"]
      }
    }
  }
])
```

**Output:**

```json
{ "item": "apple", "quantity": 5, "totalPrice": 10 }
{ "item": "banana", "quantity": 10, "totalPrice": 10 }
{ "item": "carrot", "quantity": 7, "totalPrice": 10.5 }
{ "item": "orange", "quantity": 3, "totalPrice": 9 }
{ "item": "broccoli", "quantity": 4, "totalPrice": 10 }
```

#### 4. Reshaping Document Structure

You can change the structure of your documents. For example, to create a new document structure that groups item details:

```javascript
db.sales.aggregate([
  {
    $project: {
      _id: 0,                               // Exclude the _id field
      itemDetails: {                         // Create a new object for item details
        name: "$item",
        quantity: "$quantity",
        price: "$price"
      }
    }
  }
])
```

**Output:**

```json
{ "itemDetails": { "name": "apple", "quantity": 5, "price": 2 } }
{ "itemDetails": { "name": "banana", "quantity": 10, "price": 1 } }
{ "itemDetails": { "name": "carrot", "quantity": 7, "price": 1.5 } }
{ "itemDetails": { "name": "orange", "quantity": 3, "price": 3 } }
{ "itemDetails": { "name": "broccoli", "quantity": 4, "price": 2.5 } }
```

### Conclusion

You have learned how to use the `$project` stage in MongoDB's aggregation framework to reshape documents by including, excluding, or adding fields. This stage is essential for transforming your data into the desired format for analysis or reporting.

Feel free to reach out if you have any questions or need further guidance!

***

