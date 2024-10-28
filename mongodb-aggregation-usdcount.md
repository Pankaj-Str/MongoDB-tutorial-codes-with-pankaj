# MongoDB Aggregation $count

### Introduction

The `$count` stage in MongoDB's aggregation framework is used to count the number of documents that pass through the pipeline and returns the count as a document with a specified field name. This stage is useful for obtaining a total count of documents based on certain criteria or conditions after applying various stages of the aggregation pipeline.

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

### Step 4: Using `$count`

#### 1. Basic Usage of `$count`

To count the total number of documents in the `sales` collection, you can use the `$count` stage at the end of your aggregation pipeline. For example:

```javascript
db.sales.aggregate([
  { $count: "totalSales" } // Count all documents and label the output field as totalSales
])
```

**Output:**

```json
{ "totalSales": 5 }
```

#### 2. Counting After Filtering

You can also count the documents after applying certain conditions using `$match` followed by `$count`. For example, to count how many items are in the `fruit` category:

```javascript
db.sales.aggregate([
  { $match: { category: "fruit" } }, // Filter for items in the fruit category
  { $count: "totalFruits" } // Count the filtered documents
])
```

**Output:**

```json
{ "totalFruits": 3 }
```

#### 3. Counting with Multiple Conditions

You can use `$match` to filter documents based on multiple conditions before counting. For example, to count the number of fruits with a quantity greater than 5:

```javascript
db.sales.aggregate([
  { $match: { category: "fruit", quantity: { $gt: 5 } } }, // Filter for fruits with quantity greater than 5
  { $count: "highQuantityFruits" } // Count the filtered documents
])
```

**Output:**

```json
{ "highQuantityFruits": 1 }
```

#### 4. Combining `$count` with Other Stages

You can combine `$count` with other aggregation stages for more complex analyses. For example, if you want to group items by category and then count how many items are in each category, you can use `$group` followed by `$count`:

```javascript
db.sales.aggregate([
  { $group: { _id: "$category", totalItems: { $sum: 1 } } }, // Group by category and count items
  { $count: "categoryCount" } // Count the number of unique categories
])
```

**Output:**

```json
{ "categoryCount": 2 }
```

#### 5. Counting Documents in a Sub-Pipeline

You can also use `$count` in a sub-pipeline if you want to count documents at a certain stage of your aggregation. For example, to count the number of documents after some transformations:

```javascript
db.sales.aggregate([
  { $addFields: { totalPrice: { $multiply: ["$quantity", "$price"] } } }, // Add a totalPrice field
  { $count: "totalDocumentsAfterAddFields" } // Count the documents after the addFields stage
])
```

**Output:**

```json
{ "totalDocumentsAfterAddFields": 5 }
```

### Conclusion

You have learned how to use the `$count` stage in MongoDB's aggregation framework to count documents based on specified criteria and conditions. This stage is essential for analyzing data and obtaining aggregate counts that can be useful for reporting and data insights.

Feel free to reach out if you have any questions or need further guidance!

***

